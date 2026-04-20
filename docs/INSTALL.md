# Installation

Step-by-step setup for the Mind/Body harness.

## Prerequisites

- [Claude Code](https://docs.claude.com/en/docs/claude-code) installed and signed in on your machine. Verify with `claude --version`.
- `git` available on your PATH.
- (Optional) [Obsidian](https://obsidian.md/) if you want a graph view of the vault. Not required — the vault is plain markdown.

## 1. Clone the repo

Pick a stable location on your filesystem. That folder is the **workspace root**.

```bash
git clone <your-fork-url> MindAndBody
cd MindAndBody
```

On Windows, pick something short like `C:\agents\MindAndBody` or `F:\agents\MindAndBody` to avoid path-length issues.

## 2. Create your credentials file

Copy the example and fill in only the credentials you'll actually use.

```bash
cp credentials.env.example credentials.env
```

Open `credentials.env` and paste values. This file is gitignored — never commit it, never share it.

If you want to standardize credential loading across projects, source it from whatever your project entrypoints use (e.g., `python-dotenv`, `direnv`, or a shell hook). This harness does not prescribe a loader.

## 3. (Optional) Open the vault in Obsidian

1. Launch Obsidian.
2. Choose **Open folder as vault**.
3. Select `MindAndBody/AI_Brain/`.

Obsidian will read the bundled minimal `.obsidian/` config. Your personal workspace state (which file is open, layout, etc.) is gitignored.

## 4. Start the Body

From the workspace root, launch Claude Code:

```bash
cd /path/to/MindAndBody
claude
```

Claude Code will load `CLAUDE.md` from the workspace root — that's the Body's identity. You are now talking to the Body.

## 5. First interaction with the Mind

Ask the Body something that requires stored knowledge. Example:

```
migrate the project at <path/to/some/project> into the workspace
```

The Body should:
1. Copy project files into a new folder at the workspace root.
2. Dispatch a store command to the Mind (`claude -p "Store: ..." --cwd "./AI_Brain"`).
3. Report what got indexed and what's still missing.

You can now query:

```
what do we know about <ProjectName>?
```

The Body will dispatch a query to the Mind and return structured results.

## 6. Verify the setup

From the workspace root:

```bash
# Body identity is present
cat CLAUDE.md | head -5

# Mind identity is present
cat AI_Brain/CLAUDE.md | head -5

# Dry-run a Mind invocation
claude -p "Query: list the contents of _Index.md" --cwd "./AI_Brain"
```

If the last command returns the contents of `AI_Brain/_Index.md`, the harness is working.

## Troubleshooting

- **"Claude Code can't find a CLAUDE.md"** — make sure you're launching `claude` from the workspace root (where `CLAUDE.md` lives), not a subdirectory.
- **The Mind returns information that wasn't stored** — check the Hallucination Policy in `AI_Brain/Meta/system-architecture.md` and the Mind's `CLAUDE.md`. Both forbid fabrication; if you're seeing it, the Mind's rules aren't being loaded (usually because `--cwd` is wrong).
- **Credentials leaked into a Brain file** — `git rm` the offending file, rotate the credential, and re-migrate the project using credential *names only*.
