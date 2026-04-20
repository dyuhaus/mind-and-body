# Mind and Body — A Two-Agent Harness for Claude Code

A persistent-memory harness for Claude Code built on a **Mind/Body split**:

- The **Body** is the agent you talk to. It builds, executes, and researches.
- The **Mind** is a separate Claude Code agent whose only job is to store, index, and retrieve knowledge from a markdown Obsidian vault.

The Body offloads long-term context to the Mind so you don't lose project knowledge across sessions. Credentials never enter the vault — they live in a single `credentials.env` file at the workspace root.

---

## Why use it

- **Persistence across sessions.** Claude Code has no long-term memory by default. The Mind gives it one, in a form you can read, grep, and version-control yourself.
- **Separation of concerns.** The Body does not hoard state; it asks the Mind. The Mind does not take actions; it only indexes. Each agent is narrow and auditable.
- **No hidden credentials.** Secrets live in one external file. The vault only stores names (e.g., `OPENAI_API_KEY`), never values.
- **Obsidian-compatible.** The vault is a plain markdown Obsidian vault. You can browse, search, and edit it with any tool that reads markdown — no proprietary format.
- **Project-scoped structure.** Every project migrated in gets five standard files (overview, architecture, requirements, decisions, changelog), so context is predictable.

---

## How it works

```
User ──► Body ──► Mind ──► AI_Brain (markdown vault)
                    ▲
              credentials.env lives
              OUTSIDE the vault
```

1. The user interacts with the **Body** (the Claude Code session running in the workspace root).
2. When the Body needs stored context, it dispatches a Claude Code subcommand with `--cwd` pointing at `AI_Brain/`. That sub-session is the **Mind**.
3. The Mind reads/writes markdown files inside `AI_Brain/` and replies with a structured response.
4. The Body uses that response to continue the task and reports back to the user.
5. New knowledge produced during the task is sent back to the Mind for indexing.

The rules each agent follows are encoded in two `CLAUDE.md` files:

- `CLAUDE.md` at the workspace root → Body identity.
- `AI_Brain/CLAUDE.md` → Mind identity.

Claude Code picks these up automatically based on the working directory.

---

## Repository layout

```
MindAndBody/
├── CLAUDE.md                  ← Body identity (loaded when cwd is workspace root)
├── credentials.env.example    ← Template; copy to credentials.env locally
├── .gitignore                 ← Keeps credentials and machine-specific files out of git
├── README.md                  ← This file
├── LICENSE
├── AI_Brain/                  ← The Mind's vault (Obsidian)
│   ├── CLAUDE.md              ← Mind identity (loaded when cwd is AI_Brain/)
│   ├── _Index.md              ← Master index of all knowledge
│   ├── _Inbox.md              ← Async message queue from Body → Mind
│   ├── cowork-bootstrap.md    ← Onboarding doc for teammate subagents
│   ├── Agents/                ← Agent profiles (Body.md, Mind.md)
│   ├── Meta/                  ← System docs: architecture, dictionary, migration checklist, etc.
│   ├── Projects/              ← One folder per migrated project (starts empty)
│   ├── Knowledge/             ← APIs, Patterns, Tools (starts empty)
│   └── .obsidian/             ← Minimal default Obsidian config
├── docs/
│   ├── INSTALL.md             ← Step-by-step setup
│   ├── USAGE.md               ← Everyday workflows
│   └── ARCHITECTURE.md        ← Deeper design notes
└── examples/
    └── example-project/       ← Blank project template showing the 5-file structure
```

---

## Quick start

Prerequisites: [Claude Code](https://docs.claude.com/en/docs/claude-code) installed and authenticated.

```bash
# 1. Clone into your machine's agent workspace
git clone <your-fork-url> MindAndBody
cd MindAndBody

# 2. Create your credentials file (never committed)
cp credentials.env.example credentials.env
# edit credentials.env and fill in any secrets you'll use

# 3. Start the Body from the workspace root
claude

# 4. From inside the Body session, invoke the Mind when you need knowledge:
#    claude -p "Query: <your question>" --cwd "./AI_Brain"
```

Full setup: see [`docs/INSTALL.md`](docs/INSTALL.md).

---

## Using the system

- **Migrating a project**: tell the Body "migrate the project at `<path>` into the workspace." The Body copies files, sends context to the Mind, and reports what's indexed.
- **Querying memory**: ask the Body "what do we know about `<topic>`?" The Body dispatches a query to the Mind.
- **Storing new knowledge**: after any non-trivial work, tell the Body "send this to the Brain." The Body packages and forwards the update.
- **Browsing the vault**: open `AI_Brain/` in Obsidian for a graph view, or just read the markdown files directly.

See [`docs/USAGE.md`](docs/USAGE.md) for more patterns.

---

## What's not included

This harness is intentionally minimal. It does not ship with:

- Any specific project, code, or domain logic.
- API keys or credentials (you provide your own).
- MCP server configurations (configure per deployment).
- Third-party skills, plugins, or subagent libraries (bring your own).

The goal is a clean, reproducible starting point. Everything beyond the harness is your content.

---

## License

[MIT](LICENSE).
