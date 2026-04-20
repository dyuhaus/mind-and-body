# Projects

This directory holds one folder per project. Each project's folder contains the Mind's record of that project: overview, architecture, requirements, decisions, and changelog.

## Structure

```
Projects/
├── <ProjectName>/
│   ├── <ProjectName>_overview.md        ← Summary, status, goals, stack
│   ├── <ProjectName>_architecture.md    ← Technical design, structure, typing status
│   ├── <ProjectName>_requirements.md    ← Dependencies, credential references, setup
│   ├── <ProjectName>_decisions.md       ← Key decisions and rationale
│   ├── <ProjectName>_changelog.md       ← Migration notes and subsequent changes
│   └── <ProjectName>_<custom>.md        ← Project-specific files (prefixed)
```

## How Projects Get Here

1. The user asks the Body to migrate a project.
2. The Body sends project context to the Mind.
3. The Mind creates the folder and files above using the templates in `Meta/migration-checklist.md`.
4. The Mind logs the import in `Meta/migration-log.md` and updates `_Index.md`.

## Example Project Template

See `examples/example-project/` in the repository root for a blank template you can copy into this directory as a starting point.
