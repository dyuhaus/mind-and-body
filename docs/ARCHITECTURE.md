# Architecture

Deeper design notes for the Mind/Body harness.

---

## Two agents, two identities

Claude Code loads a `CLAUDE.md` file based on its working directory. This harness exploits that:

- `CLAUDE.md` at the workspace root → Body rules (build, research, execute).
- `AI_Brain/CLAUDE.md` → Mind rules (markdown-only, no external actions, no hallucinations).

When the Body runs `claude -p "..." --cwd "./AI_Brain"`, the sub-session loads the Mind's identity instead of the Body's. Two personalities, same model, clean separation.

---

## Why split them

A single agent doing both jobs will eventually either:

1. **Forget things** because its context window is full of work it also did, or
2. **Fabricate things** because remembering feels close enough to reasoning.

Splitting the jobs lets each agent be narrow and strict:

- The Body is allowed to act, forbidden from assuming.
- The Mind is allowed to index, forbidden from inventing.

Both agents are equally capable of hallucinating if their rules are loose. The rules in their `CLAUDE.md` files are load-bearing.

---

## Markdown-only vault

The vault is a plain Obsidian vault: markdown files, `[[wiki-style-links]]`, YAML frontmatter. This is a deliberate constraint:

- **Human-auditable.** You can grep, read, and edit the vault without the agent.
- **Tool-agnostic.** Obsidian is convenient but not required; any markdown viewer works.
- **Portable.** No database, no proprietary format, no migration risk.
- **Version-controllable.** Git tracks the vault. Diffs are human-readable.

Non-markdown files are forbidden inside `AI_Brain/`. If you need binaries (PDFs, audio, datasets), store them outside and reference them by path.

---

## Project file convention

Every migrated project gets exactly five files in `AI_Brain/Projects/<ProjectName>/`:

| File | Purpose |
|------|---------|
| `<Name>_overview.md` | Status, summary, goals, stack. First file to read. |
| `<Name>_architecture.md` | Technical design, layout, typing status. |
| `<Name>_requirements.md` | Dependencies, credential *names*, setup steps. |
| `<Name>_decisions.md` | Decision log: what, why, alternatives rejected. |
| `<Name>_changelog.md` | Notable changes over time. |

Five files, consistently named, so agents (and humans) always know where to look. Extra project-specific files use the same `<Name>_<topic>.md` prefix convention.

---

## Synapses

Obsidian links (`[[target]]`) are called **Synapses** in this system. The rules for when to create them are in `AI_Brain/Meta/connection-policy.md`. The short version:

- Link on **direct dependency**, **shared agent/credential**, or **decision influence**.
- Do not link on **shared language**, **temporal coincidence**, or **cosmetic similarity**.
- If a file has 10+ outgoing links, most are probably noise.

Good Synapses let the Mind answer "what else is affected if I change X?" without hallucinating.

---

## Credential boundary

The only file that ever touches real secrets is `credentials.env` at the workspace root. It is:

- `.gitignore`d.
- Outside the vault.
- Referenced inside the vault by **name only** (e.g., `OPENROUTER_API_KEY`).

The Mind's rules explicitly forbid storing credential values. If the Body attempts to send one, the Mind must refuse.

This is enforcement by convention, not by sandbox — so if you ever see a secret in the vault, treat it as a leak: rotate immediately.

---

## Session lifecycle

The Mind has no memory between invocations; each `claude -p "..." --cwd "./AI_Brain"` is a fresh session. The warm-up protocol (`AI_Brain/Meta/warmup-protocol.md`) exists to re-orient the Mind at the start of a multi-step operation, by passing recent-actions context explicitly.

The Body has the usual Claude Code session lifecycle. Its long-term memory is entirely the vault.

---

## Scaling

The harness works well up to somewhere in the tens of projects. Beyond that:

- The master `_Index.md` gets noisy — consider hierarchical indexes per project category.
- Cross-vault queries become slow — consider splitting into multiple vaults (one per domain).
- Decision logs get long — consider a yearly archive pattern (`decisions-2026.md`, etc.).

None of these are architectural changes; they're scaling patterns within the same convention.
