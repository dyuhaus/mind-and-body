# Cowork Bootstrap — Brain Access Guide

This file provides the context every teammate or subagent needs to operate within the Brain system. Use it as the onboarding document when spawning subagents that must read/write both the workspace and the Brain.

---

## System Architecture

This workspace uses a **Mind/Body architecture**:
- **Body** (workspace root) — The action agent. Builds, executes, researches.
- **Mind** (vault: `<workspace-root>/AI_Brain/`) — The knowledge agent. Stores, organizes, retrieves information.
- **Teammates/Subagents** — Specialized roles that can read and write to both the workspace and the Brain.

## Brain Vault Structure

```
AI_Brain/
├── _Index.md              ← Master index of all knowledge areas
├── _Inbox.md              ← Incoming info queue
├── cowork-bootstrap.md    ← THIS FILE
├── Projects/              ← One folder per project
│   └── <ProjectName>/
│       ├── <ProjectName>_overview.md        ← Summary, status, goals
│       ├── <ProjectName>_architecture.md    ← Technical design, stack
│       ├── <ProjectName>_requirements.md    ← Dependencies, setup needs
│       ├── <ProjectName>_decisions.md       ← Key decisions + rationale
│       ├── <ProjectName>_changelog.md       ← Notable changes
│       └── <ProjectName>_<custom>.md        ← Project-specific files
├── Agents/                ← Agent profiles
├── Knowledge/             ← Domain knowledge
│   ├── Patterns/          ← Reusable technical patterns
│   ├── APIs/              ← API references
│   └── Tools/             ← Tool/framework notes + discoveries
└── Meta/                  ← Vault maintenance docs
```

## Active Projects

Populate this table as projects are migrated into the vault.

| Project | Brain Path | Workspace Path | Description |
|---------|-----------|----------------|-------------|
| | | | |

All paths are relative to the workspace root.

## Reading Brain Files

To get context for any project, read these files (all may not exist):
```
AI_Brain/Projects/<ProjectName>/<ProjectName>_overview.md
AI_Brain/Projects/<ProjectName>/<ProjectName>_architecture.md
AI_Brain/Projects/<ProjectName>/<ProjectName>_requirements.md
AI_Brain/Projects/<ProjectName>/<ProjectName>_decisions.md
AI_Brain/Projects/<ProjectName>/<ProjectName>_changelog.md
```

For cross-project knowledge:
```
AI_Brain/Knowledge/APIs/<api-name>.md
AI_Brain/Knowledge/Patterns/<pattern-name>.md
AI_Brain/Knowledge/Tools/<tool-name>.md
```

## Writing to the Brain

When updating Brain files:
1. **Markdown only** — no other file types permitted.
2. **No credentials** — never store API keys, passwords, or tokens. Only reference names.
3. **Prefix filenames** — `<ProjectName>_<topic>.md`.
4. **Use Obsidian links** — `[[Target]]` or `[[Target|Display Text]]` for cross-references.
5. **Update `_Index.md`** if creating new top-level entries.
6. **Be specific** — link to sections when possible: `[[ProjectName/architecture#Stack]]`.

## Credential Policy

Credentials live ONLY in `<workspace-root>/credentials.env`.
- Never read, display, or copy credential values into Brain files.
- Reference by name only (e.g., "requires OPENROUTER_API_KEY").
- If a teammate needs a credential, ask the team lead to provide the env var name.

## Coding Standards (All New Code)

- **Strong typing mandatory** — Python: type hints everywhere. TypeScript: explicit interfaces, no `any`.
- **Immutability preferred** — `const`/`Final`/`readonly`, new objects over mutation.
- **Naming** — Python: `snake_case`. JS/TS: `camelCase` vars, `PascalCase` types. Classes: `PascalCase` everywhere.
- **Error handling** — Always explicit, never swallowed. Log or propagate meaningfully.
- **File limits** — Functions < 50 lines. Files < 800 lines.
- **No magic values** — Use named constants or enums.
