---
tags: [meta, system]
cssclasses: [meta-doc]
---
# AI_Brain — System Architecture

## Purpose
A markdown-only Obsidian vault that serves as persistent memory for an AI agent system. Information is indexed for agent consumption, not human browsing. Two agents interact with this vault: the **Mind** (internal) and the **Body** (external).

---

## Agents

### [[Agents/Mind|Mind]]
- **Domain**: `<workspace-root>/AI_Brain/` (vault only)
- **Role**: Store, organize, retrieve, and connect information
- **Capabilities**: Create/edit `.md` files, manage Synapses, answer queries
- **Constraints**:
  - Cannot take actions outside the vault
  - Cannot create non-markdown files
  - Cannot fabricate information (see: Hallucination Policy)
  - Cannot store credentials

### [[Agents/Body|Body]]
- **Domain**: `<workspace-root>/` (everything outside the vault)
- **Role**: Execute tasks, interact with user, build projects, conduct research
- **Capabilities**: Full development toolchain, MCP servers, web access, file I/O
- **Constraints**:
  - Cannot retain long-term knowledge (offloads to Mind)
  - Cannot make assumptions — must query Mind or ask user
  - Cannot store credentials in the Brain
  - Must feed new knowledge to the Mind after task completion

---

## Information Flow

```
User ←→ Body ←→ Mind ←→ AI_Brain (vault)
                  ↑
            Credentials live outside
            (<workspace-root>/credentials.env)
```

- User talks to Body. Body queries Mind when knowledge is needed.
- Body sends new information to Mind for indexing after completing work.
- Mind never interacts with the user directly.
- Credentials never enter the vault. Only credential *names* are referenced.

---

## Mind Invocation

The Body invokes the Mind via **Claude Code subcommand dispatch**:

```bash
# Query
claude -p "Query: [question]" --cwd "<workspace-root>/AI_Brain"

# Store
claude -p "Store: [information to index]" --cwd "<workspace-root>/AI_Brain"

# Batch
claude -p "Process all entries in _Inbox.md, then clear processed items." --cwd "<workspace-root>/AI_Brain"
```

Async fallback: write to `_Inbox.md`, then invoke the Mind to process.

---

## Terminology

| Term | Definition |
|------|-----------|
| **Synapse** | An Obsidian link (`[[target]]`) connecting two knowledge entries. Represents a meaningful relationship. |
| **Connected Thought** | The process of reasoning across Synapses to surface relationships between knowledge areas. |
| **Hallucination** | Information fabricated by the Mind that was never provided by the Body. Strictly prohibited — corrupts the vault. |
| **Brain** | The AI_Brain Obsidian vault — the sole repository of persistent knowledge. |

---

## Hallucination Policy

The Mind must never create information that wasn't explicitly provided by the Body.

**Allowed**: Storing information the Body provides, creating Synapses between existing entries, reorganizing content for clarity, reporting that information is missing.

**Prohibited**: Inferring facts, filling gaps with assumptions, generating content based on general knowledge, answering queries with information not found in the vault.

**When information is missing**:
1. Report exactly what was searched and not found.
2. Ask the Body for clarifying details that might help locate it.
3. If still not found → State clearly: "Not in the Brain. Body must provide."
4. A missing-information response is always valid — it identifies what the Body needs to supply.

---

## Credential Security

- Master credentials file: `<workspace-root>/credentials.env` (outside vault).
- Projects reference credentials by environment variable name, never by value.
- The Mind stores only credential *names* in `requirements.md` files (e.g., "Requires: OPENAI_API_KEY").
- If the Body attempts to send a credential value to the Mind, the Mind must refuse and redirect.

---

## Coding Standards

All new code must use **strong typing** and follow industry standard practices. See the Body's `CLAUDE.md` for full details. The Mind tracks the typing status of each project in `architecture.md` to flag technical debt.

---

## Migration Protocol

Projects are imported one at a time. For each project:

1. Body provides project files + context to the Mind.
2. Mind creates project folder under `Projects/` with:
   - `overview.md` — summary, status, goals, stack
   - `architecture.md` — technical design, structure, typing status
   - `requirements.md` — dependencies, credential refs (names only), setup steps
   - `decisions.md` — key decisions and their rationale
   - `changelog.md` — migration notes and subsequent changes
3. Mind completes the migration checklist (`Meta/migration-checklist.md`).
4. Mind creates Synapses to related projects, agents, and knowledge areas.
5. Mind logs the import in `Meta/migration-log.md`.
6. Mind updates `_Index.md`.
7. Body creates runtime copies of `CLAUDE.md` and `requirements.md` in the project directory.
8. Body reports to user: what was migrated, what's missing, what setup is needed.

## Related
- [[Meta/dictionary]] — Terminology definitions used throughout this document
- [[Meta/connection-policy]] — Rules governing Synapse creation
- [[Meta/warmup-protocol]] — How Body initializes Mind sessions
- [[Meta/migration-checklist]] — Detailed checklist for step 3-6 above
- [[Meta/migration-log]] — Record of completed migrations
