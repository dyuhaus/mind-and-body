---
tags: [meta, protocol]
cssclasses: [meta-doc]
---
# Mind Warm-Up Protocol

The [[Agents/Mind|Mind]] has no memory between invocations. At the start of each work session (or before a complex multi-step operation), the [[Agents/Body|Body]] should send a warm-up prompt to orient the Mind.

---

## Template

```
Warm-Up: Session Context

### Current Session
- Date: [YYYY-MM-DD]
- Active Project: [project name or "general"]
- Task: [brief description of what the Body is working on]

### Recent Actions (last session)
- [Action 1]
- [Action 2]
- [Action 3]

### What I Need From You
- [Specific query or instruction]
- [Or: "I have new information to store about <Project> and its decision to <change>"]

### Notes
- [Any context that helps — e.g., "User wants to add a new MCP server"]
```

---

## When to Use

- **Always** at the start of a new work session involving Brain queries.
- **Before** complex migrations or multi-file updates.
- **After** long gaps between Mind invocations (the Mind has zero session continuity).
- **Optional** for simple one-shot queries where the context is self-contained.

---

## Example Invocation

```bash
claude -p "Warm-Up: Session Context

### Current Session
- Date: 2026-01-15
- Active Project: <ProjectName>
- Task: Adding a new feature to the project

### Recent Actions
- Completed initial <ProjectName> migration yesterday
- Fixed a rate-limiting issue in the data pipeline
- User provided new credential: <CREDENTIAL_NAME> (name only)

### What I Need From You
- Pull up <ProjectName> architecture and current feature list
- Add <CREDENTIAL_NAME> to <ProjectName> requirements
- Check if any other projects also use similar dependencies
" --cwd "<workspace-root>/AI_Brain"
```

---

## Body Implementation Note

The Body should build the warm-up prompt programmatically when possible. Keep a lightweight session log (last 3-5 actions) in the Body's working memory to populate the "Recent Actions" section. This log does not persist — it only covers the current session.

## Related
- [[Meta/system-architecture#Mind Invocation]] — Subcommand dispatch details
- [[Meta/migration-checklist]] — Complex migrations benefit from warm-up
- [[Agents/Mind]] — Receives warm-up prompts
- [[Agents/Body]] — Sends warm-up prompts
