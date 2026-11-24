# Proposed architecture

**Workflow status: Planned.** No services, database or connections have been provisioned for this showcase.

## Scope and boundaries

Use Make.com to normalise submissions, resolve contacts, enrich company information and extract requirements with AI. Versioned rules would score leads, while a separate verified contract event would authorise onboarding.

A lead score would prioritise agency follow-up; it would not approve a deal or authorise onboarding. Proposal generation would produce a draft. Only a verified contract event, the current provider-side contract state and the agreed business approval would permit project creation.

The [README diagram](../README.md) and [Mermaid source](../diagrams/architecture.mmd) describe the same proposed flow. The orchestrator would coordinate calls; it would not treat model output as execution authority.

## Proposed data contracts

| Contract | Proposed fields and constraints |
| --- | --- |
| Lead event | `schema_version`, `event_id`, `submitted_at`, `contact_email`, `company_domain`, bounded project text and consent metadata |
| Extracted requirements | `service_type`, `budget_range`, `timeline`, `requirements`, `missing_fields`, source-field references; unknown values remain null |
| Qualification | Lead ID, scoring-rule version, per-rule contributions, score band and review reason |
| Contract event | Provider event ID, provider contract ID, event type and timestamp; current state fetched independently |
| Onboarding state | Contract and project IDs, approval reference, per-step status and external resource IDs |

The schemas and field mappings remain to be implemented. Enrichment and model output must carry provenance and must not overwrite verified CRM fields without an explicit mapping rule.

## Decision rules

| Condition | Proposed deterministic action |
| --- | --- |
| Known contact with matching verified identity | Update allowed CRM fields; preserve ownership and verified values |
| Conflicting contact match or incomplete required data | Hold for human qualification |
| Valid extracted fields | Apply a versioned rule table for service fit, budget and timing; weights and cutoffs remain to be defined |
| Qualified lead | Schedule or follow up according to agreed consent and contact policy |
| High score without a verified approved contract | Do not start onboarding |
| Verified approved contract with no completed onboarding | Claim onboarding by contract and template version, then create assets |

The LLM would extract requirements, not assign the score. Missing values would remain unknown; they must not be treated as evidence that a lead qualifies.

## Proposed recovery and observability

Use a durable execution record with `received`, `processing`, `awaiting_review`, `completed`, `rejected` and `failed` states. Claim a stable source/event key atomically; a read-then-write duplicate check alone is insufficient under concurrency. Define leases and recovery for abandoned processing before implementation.

Persist per-action state and external resource IDs. For a timeout after an external write, reconcile provider state before retrying; do not assume a timeout means the write failed. Use provider idempotency keys where available. Exactly-once delivery across independent APIs is not assumed.

Retry transient failures such as rate limits and network/server errors with bounded backoff and jitter, respecting provider retry guidance. Invalid data, authentication failures and unauthorised actions require correction or review. After the retry limit, retain a failure record for deliberate replay from the failed stage.

Log correlation ID, stage, attempt, duration, outcome, rule/prompt version and a redacted error category. Keep payload bodies, credentials and personal information out of routine logs. A status must not become completed if required persistence fails. Surface persistence/claim failures operationally rather than continuing without duplicate protection.

These are proposed requirements; no recovery mechanism, dashboard or operational guarantee is implemented yet.

## Decisions still open

- **Contact resolution:** Choose CRM unique identifiers and normalisation rules; company domain alone must not merge individuals.
- **Enrichment provider:** Select permitted fields, provenance and fallback behaviour; do not invent unavailable company information.
- **Scoring policy:** Agree inputs, weights, cutoffs and missing-value handling; no production scoring policy is claimed.
- **Contract approval:** Define acceptable provider states, internal approval and replay rules before any onboarding.
- **Tasks and notifications:** Select providers and a project template after the CRM and contract path is working.

See the [implementation plan](implementation.md), [security design](security.md) and [test matrix](testing.md).
