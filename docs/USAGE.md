# Usage

Common workflows once the harness is installed.

---

## Talking to the Body

Launch `claude` from the workspace root. Everything you type in that session goes to the Body. The Body loads `CLAUDE.md` from the workspace root (its identity) and decides when to query/update the Mind.

---

## Querying the Mind directly

You can invoke the Mind yourself without going through the Body:

```bash
claude -p "Query: What is the architecture of <ProjectName>?" --cwd "./AI_Brain"
claude -p "Store: <ProjectName> switched from REST to WebSocket on 2026-01-15 for latency reasons." --cwd "./AI_Brain"
```

The `--cwd` flag tells Claude Code to load `AI_Brain/CLAUDE.md` (the Mind identity) instead of the Body's.

---

## Migrating a project

Tell the Body something like:

> Migrate the project at `C:/projects/MyThing` into the workspace. Here's the context: it's a Python FastAPI service that calls the Stripe API and writes to Postgres.

The Body should:

1. Copy files into `<workspace-root>/MyThing/`.
2. Dispatch a store command that creates five files in `AI_Brain/Projects/MyThing/`:
   - `MyThing_overview.md`
   - `MyThing_architecture.md`
   - `MyThing_requirements.md`
   - `MyThing_decisions.md`
   - `MyThing_changelog.md`
3. Log the migration in `AI_Brain/Meta/migration-log.md`.
4. Update `AI_Brain/_Index.md`.
5. Create a runtime `CLAUDE.md` inside `MyThing/` with project-specific instructions.
6. List any credentials still missing from `credentials.env`.

If the Body skips steps, remind it of the migration checklist in `AI_Brain/Meta/migration-checklist.md`.

---

## Storing new knowledge

Any time you tell the Body something with lasting value — a design decision, an API quirk, a new environment variable — ask it to send the update to the Mind. Example:

> Send this to the Brain: Stripe's `charges.list` endpoint has a 100-row cap; use `auto_pagination_iter` in the SDK to stream larger ranges.

The Body will store this under `AI_Brain/Knowledge/APIs/stripe.md` (or create the file if it doesn't exist) and add a Synapse from the relevant project.

---

## Querying for context

Before you do work on an existing project, ask the Body for the relevant context:

> Before I change the billing module, pull up everything the Brain has on MyThing's Stripe integration.

The Body dispatches a query, the Mind returns structured results, and the Body summarizes. If the Mind reports gaps, the Body will ask you to fill them in.

---

## Browsing the vault directly

The vault is just markdown. Any of these work:

- Open `AI_Brain/` in Obsidian for graph and backlinks view.
- Use `grep`/`rg` from the command line.
- `ls AI_Brain/Projects/` to see every indexed project.
- Read `AI_Brain/_Index.md` as a starting point.

You are never locked in to agent-mediated reads.

---

## When the Body is wrong

If the Body ever:

- Claims something that isn't in the Brain → the Mind is hallucinating. Check `AI_Brain/Meta/system-architecture.md` → Hallucination Policy. Usually means the Mind's `CLAUDE.md` wasn't loaded (wrong `--cwd`).
- Forgets something you told it earlier → the Body didn't persist it. Ask: "Did you send that to the Brain?" If not, have it do so now.
- Stores a credential value in a markdown file → stop, rotate the credential, `git rm` the file, and file a bug against your own workflow. The rules in both `CLAUDE.md` files forbid this.

---

## Teaming up with subagents

If you spawn teammate subagents (via the Claude Code Agent tool), point them at `AI_Brain/cowork-bootstrap.md`. That file is the onboarding doc: it describes the vault layout, the write rules, and the credential policy.
