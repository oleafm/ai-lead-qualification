# Implementation plan

**Workflow status: Planned.** This is a build plan, not setup instructions for a runnable integration. No API connections, workflow exports or deployment have been completed.

## Suggested build sequence

1. Choose a sandbox CRM, enrichment provider and durable event store. Agree contact normalisation and merge rules.
2. Build authenticated intake, input limits and event claims; store the accepted event before acknowledging delivery.
3. Resolve contacts and enrich only the approved company fields. Label enrichment failures and preserve field provenance.
4. Define an extraction schema and prompt, then implement explicit scoring configuration with documented missing-data behaviour.
5. Build reusable CRM, scheduling and proposal sub-scenarios. Keep proposal sending behind human approval.
6. Build a separate contract-event handler that verifies authenticity, refetches the contract and checks business approval.
7. Track folder, task and notification steps independently so a retry resumes without repeating completed actions.
8. Run duplicate, partial-failure and out-of-order-event tests before adding real Make exports and measured evidence.

## Prerequisites to choose or configure

- **Contact resolution:** Choose CRM unique identifiers and normalisation rules; company domain alone must not merge individuals.
- **Enrichment provider:** Select permitted fields, provenance and fallback behaviour; do not invent unavailable company information.
- **Scoring policy:** Agree inputs, weights, cutoffs and missing-value handling; no production scoring policy is claimed.
- **Contract approval:** Define acceptable provider states, internal approval and replay rules before any onboarding.
- **Tasks and notifications:** Select providers and a project template after the CRM and contract path is working.

Keep credentials in the selected platform's credential store. Use synthetic records and sandbox accounts when building the showcase. No secret values belong in this repository.

## Implementation record — placeholder

| Item | Current record |
| --- | --- |
| Workflow/export version | Not implemented |
| Platform and tool versions | To be recorded after selection |
| Configured API connections | None documented |
| Running environment | None documented |
| Verified scope | None |
| Known gaps | All planned capabilities remain unimplemented |
| Results | Not measured |

Replace these rows with actual versions and evidence as work progresses. Keep the [README checklist](../README.md) and [architecture](architecture.md) consistent. Follow the [maintenance guide](maintenance.md) when adding real artifacts.
