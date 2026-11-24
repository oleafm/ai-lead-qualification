# Testing and evaluation plan

**Workflow status: Planned. Tests not executed.** Expected outcomes below are specifications, not test results. No fixture files, benchmark scores or runtime evidence exist yet.

## Test environment and data

Use sandbox connections, synthetic records, a controlled model configuration and isolated notification destinations. Stub external failures first, then verify behaviour against actual sandbox APIs. Record provider/tool versions, prompt version, rule/schema versions and export revision.

Create each case with a stable case ID, labelled input, expected decision, expected external side effects and expected state transition. Keep [synthetic fixtures](../sample-data/README.md) separate from measured outputs. Repeat delivery and concurrency tests with overlapping runs.

## Planned test matrix

| Case | Synthetic input or failure | Expected outcome |
| --- | --- | --- |
| L01 | Complete synthetic enquiry | Validated extraction, explainable score and one CRM operation |
| L02 | Duplicate form events and existing contacts | No duplicate lead or unintended contact merge |
| L03 | Missing budget, conflicting identity or enrichment outage | Unknown values preserved and documented review/fallback path |
| L04 | Prompt injection in project requirements | Data stays within extraction; no destination or approval changes |
| L05 | Score boundaries and missing fields | Expected result from the versioned rule table |
| L06 | Forged, duplicate or out-of-order contract event | No unauthorised or repeated onboarding |
| L07 | Folder created, task provider fails | Retry resumes tasks using stored folder ID |
| L08 | Rate limit, expired OAuth or invalid model output | Bounded retry or review; no false success |
| L09 | Proposal draft and follow-up in sandbox | No unintended recipient contacted |

## Evaluation method

Record extraction agreement per field, deterministic score assertions, contact-resolution outcomes, duplicate resource counts and recovery behaviour. Include dataset size, rule version, model/prompt version and failing cases. No conversion uplift or time-saving results have been measured.

Critical safety cases must show no unauthorised action; replay tests must show no duplicate side effects. These are acceptance requirements, not passed assertions. Version the labelled set before testing and retain an evaluation subset when tuning prompts.

## Results — placeholder

| Evidence | Current state |
| --- | --- |
| Synthetic dataset and expected outputs | Not prepared |
| Test execution date/environment | Not available |
| Cases run / pass / fail | Not measured |
| Extraction or classification quality | Not measured |
| Reliability and recovery evidence | Not measured |
| Latency and API usage | Not measured |
| Known limitations | Implementation and evaluation still pending |

After execution, add a per-case result with run date, workflow/export revision, expected/actual behaviour and sanitised evidence. Report failures and dataset limitations alongside successes. Do not mark the project Tested until the documented tests have actually run.

See [implementation](implementation.md) and [maintenance](maintenance.md).
