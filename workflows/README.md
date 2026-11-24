# Workflow exports

**Placeholder — no workflow export exists yet.** The project is Planned.

Add actual Make.com blueprint JSON files for intake, qualification and approved onboarding here after building and reviewing the workflow. Use descriptive, versioned filenames and identify which scenario each file represents. Do not create a hand-written JSON file that could be mistaken for a real platform export.

Before committing an export, remove secrets, connection/account IDs, private webhook URLs, destination identifiers, embedded records and execution history. Keep unreviewed exports in ignored `raw-exports/`. Record required connection remapping rather than credentials.

When a real export is available, document its platform/tool version, export date, scope, sandbox import steps, required permissions and configuration. Import the sanitised export into a clean sandbox and record any manual repairs or unsupported features. Never describe an export as runnable until that import has been checked.

See the [implementation plan](../docs/implementation.md) and [maintenance guide](../docs/maintenance.md).
