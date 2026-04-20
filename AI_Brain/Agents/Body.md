---
tags: [agent, core]
cssclasses: [agent-node]
---
# Agent: Body

## Purpose
The action agent and primary user interface. Executes tasks, builds projects, conducts research, and interacts with external systems. Relies on the [[Agents/Mind|Mind]] for persistent knowledge. See [[Meta/system-architecture]] for full system design.

## Location
```
<workspace-root>/
```
Identity file: `<workspace-root>/CLAUDE.md`

## Execution Environment
- **Runtime**: Claude Code CLI
- **Languages**: Python (3.10+), TypeScript, Node.js, Bash (commonly; configure per project)
- **Coding Standards**: Strong typing mandatory on all new code. See Body `CLAUDE.md` for full spec.
- **OS**: Platform-agnostic (any system Claude Code runs on)

## Tools & Connections

### MCP Servers
Configure per deployment. Add entries here as you connect servers so the Mind can track them. Typical connections might include design, issue tracking, documentation, calendar, email, and scraping servers.

### APIs (commonly used)
Add links to `Knowledge/APIs/` entries as they are created.

### Development Tools
- Git — Version control (conventional commits, only improvements committed)
- Package managers — npm / pip / cargo / etc. as required per project
- Type checkers — mypy, tsc, or equivalent when feasible

## Capabilities
- Application development (full-stack, CLI tools, agent systems)
- Document generation (reports, presentations, analysis)
- Web research and data gathering
- Mathematical and data analysis
- System administration and infrastructure
- Multi-agent orchestration
- Project scaffolding and migration

## Constraints
- Cannot retain long-term knowledge — offloads to Mind
- Cannot make assumptions — must query Mind or user for missing context
- Cannot store credentials in the Brain
- Must feed new knowledge to Mind after completing significant work

## Related Projects
Add links to `Projects/<ProjectName>/<ProjectName>_overview.md` as projects are migrated into the vault.

## Related
- [[Agents/Mind]] — The Mind serves as Body's persistent memory
- [[Meta/warmup-protocol]] — How Body initializes Mind sessions
- [[Meta/connection-policy]] — Rules for creating Synapses
