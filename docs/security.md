# Proposed security and reliability controls

**Workflow status: Planned.** The controls below are design requirements to implement and test, not verified protections.

## Project-specific trust boundaries

- Verify webhooks and bound all form fields. Treat project descriptions and enrichment data as untrusted input to extraction.
- Limit enrichment to agreed business data and use the minimum information required by the model. Record the source and retrieval time.
- Use OAuth or provider-approved authentication with minimum scopes. Separate sandbox CRM, proposal and storage connections.
- Do not use an LLM result, score or scheduling event as contractual approval. Refetch contract status and validate the authorised approval reference.
- Keep generated proposals as drafts until a person approves recipients and content. Sandbox tests must not contact real leads.
- Use explicit Drive parent folders and destination IDs. Do not let free-form lead text determine file paths or external API destinations.

## Authentication and secrets

Verify webhook signatures and timestamps when supported, including replay handling. If the source lacks signing, choose an authenticated gateway or another provider-supported verification method before exposing intake. Store credentials in the orchestrator's credential store, use minimum permissions and rotate or revoke them when needed.

Keep tokens, OAuth refresh material, connection identifiers, private webhook URLs and service credentials out of exports, prompts, screenshots and logs. Use sandbox connections for demonstrations. A public repository must contain only reviewed documentation and sanitised artifacts.

## Human review and authorisation

Bind reviewer decisions to an authenticated actor, the exact record revision, proposed action and expiry time. Reject stale or replayed decisions and record approval/rejection reasons. Notifications are pointers to the review process; a message, extracted phrase or model flag alone does not authorise action.

## Data minimisation and retention

Define what data each provider receives before configuration. Review provider retention and processing settings against the intended use. Select retention periods for source inputs, model payloads, execution logs and review records; these periods are not yet decided. Restrict access and document deletion handling before processing any real data.

Only clearly labelled synthetic inputs may be committed. Do not include real customer, lead, supplier or invoice information even when demonstrating a failure case.

## Reliability and publication review

Implement the [durable execution and retry design](architecture.md). Test authorisation, duplicate delivery, partial failure and injection attempts using the [test matrix](testing.md). Record the observed limits instead of claiming complete protection.

The [maintenance guide](maintenance.md) describes artifact sanitisation. `.gitignore` is a convenience, not a security control; inspect tracked files and image contents before publishing.
