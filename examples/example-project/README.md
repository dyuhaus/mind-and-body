# Example Project — Starter Template

This is a blank project template demonstrating the five-file structure every migrated project gets in the Brain:

1. `<ProjectName>_overview.md` — summary, status, goals, stack
2. `<ProjectName>_architecture.md` — technical design, file layout, typing
3. `<ProjectName>_requirements.md` — dependencies, credential names, setup
4. `<ProjectName>_decisions.md` — decision log
5. `<ProjectName>_changelog.md` — change history

## How to Use

1. Copy this folder into `AI_Brain/Projects/<YourProjectName>/` in the Mind's vault.
2. Rename every file prefix from `ExampleProject_` to `<YourProjectName>_`.
3. Populate the placeholders with your project's real details.
4. Create the runtime copy of `<YourProjectName>_requirements.md` in your project's workspace folder so agents working on the project see it without querying the Mind.
5. Tell the Mind to update `_Index.md` and add a row to `Meta/migration-log.md`.

See `docs/INSTALL.md` for the full setup flow and `AI_Brain/Meta/migration-checklist.md` for the full migration protocol.
