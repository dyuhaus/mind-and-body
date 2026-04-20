---
tags: [agent, core]
cssclasses: [agent-node]
---
# Agent: Mind

## Purpose
The knowledge agent that manages the AI_Brain Obsidian vault. Stores, organizes, retrieves, and connects information. Serves the [[Agents/Body|Body]] as its persistent memory.

## Location
```
<workspace-root>/AI_Brain/
```
Identity file: `<workspace-root>/AI_Brain/CLAUDE.md`

## Invocation
The Body invokes the Mind via Claude Code subcommand dispatch:
```bash
claude -p "[instruction]" --cwd "<workspace-root>/AI_Brain"
```

## Tools & Connections
- File creation and editing (`.md` only, within vault)
- File search and reading (within vault)
- No external tools, APIs, or MCP servers

## Capabilities
- Index and organize project information
- Create and maintain Synapses (Obsidian links)
- Answer structured queries from the Body
- Track migration status and vault health
- Maintain the `_Index.md` master registry

## Constraints
- Cannot act outside the vault
- Cannot create non-markdown files
- Cannot fabricate information ([[Meta/system-architecture#Hallucination Policy|Hallucination Policy]])
- Cannot store credentials
- Cannot interact with the user directly

## Related
- [[Agents/Body]] — The agent the Mind serves
- [[Meta/system-architecture]] — Full system design
- [[Meta/connection-policy]] — Synapse creation rules
- [[Meta/migration-checklist]] — Import workflow template
- [[Meta/migration-log]] — Record of completed imports (Mind maintains)
- [[Meta/dictionary]] — Vault terminology definitions
- [[Meta/warmup-protocol]] — How the Body initializes Mind sessions
