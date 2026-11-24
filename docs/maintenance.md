# Maintenance guide

The current workflow status is **Planned**. Documentation preparation does not mean implementation or architecture verification is complete.

## Status definitions

| Status | Evidence required |
| --- | --- |
| Planned | Proposed scope and design; workflow implementation has not started |
| In Progress | Real implementation has started; record the working scope and remaining gaps |
| MVP Complete | The documented minimum path works in a sandbox; export and evidence describe its limits |
| Tested | The documented test suite has been executed; dataset, results and failures are recorded |
| Published | A reviewed, sanitised case study, workflow export and demo are publicly available |

Public repository visibility does not make a workflow Published. Change the current-status row in the project README and the matching project status in `oleafm/oleafm`. Tick a progress box only when its evidence exists; incomplete steps stay unchecked even at MVP Complete.

## After a workflow is built

1. Export the actual Make blueprint or n8n workflow into `workflows/` after removing credentials, account/connection IDs, webhook URLs, private destinations, embedded payloads and execution history. Keep an unreviewed export only in ignored `raw-exports/`.
2. Document the export filename, tool version, export date, connection remapping and sandbox import steps in the workflows README. Sanitisation can break imports, so test the sanitised version and state any required repair.
3. Add redacted screenshots from the real scenario to `screenshots/` with captions and version references. Do not substitute mockups for implementation evidence.
4. Compare the running workflow with `diagrams/architecture.mmd`. Update both that source and the README Mermaid block. Use **Verified Architecture** only after checking the real implementation; explain remaining gaps.
5. Add actual prompt files to `prompts/` with schema, model/settings, version and known limitations. Remove secrets and private examples.
6. Add clearly labelled synthetic inputs and expected outputs to `sample-data/`. Execute the testing plan and record results, sample size, environment, versions and failures in the testing document.
7. Replace the demo placeholder with a working video URL showing a synthetic run. Keep unrecorded demos labelled as unavailable.
8. Update implementation decisions, current status and the progress checklist. Finalise the case study using only observed behaviour and measured results.
9. Update the profile project description, stack, status, diagram link and demo reference to match the showcase.

## Review before each public update

- Review every changed file and the staged diff, including export JSON and image contents. `.gitignore` does not remove already tracked files or sanitise exports.
- Check for tokens, keys, authorisation headers, OAuth material, webhook URLs, customer records and private account metadata. Automated scanning supplements manual review.
- Follow relative links, preview the README and Mermaid diagram on GitHub, and confirm both diagram copies match.
- Create a `codex/` branch or another chosen working branch for later changes and review a pull request before merging.
- If sensitive content was committed, stop publication, revoke affected credentials and remove the material from history before resuming.

No particular project completion date, performance result or operational guarantee should be added without supporting evidence.
