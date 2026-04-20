---
tags: [meta, process]
cssclasses: [meta-doc]
---
# Migration Checklist Template

Copy this checklist into the project's `changelog.md` at the top when beginning a migration. Complete each item and mark it done. Do not skip items — mark as N/A if not applicable.

**Participants**: [[Agents/Mind]] completes Brain Indexing and Synapses sections. [[Agents/Body]] handles Runtime Setup. Results recorded in [[Meta/migration-log]].

---

## Checklist: [Project Name]
**Migration Date**: [YYYY-MM-DD]
**Migrated By**: Body

### Files Received
- [ ] Project source files copied to `<workspace-root>/<ProjectName>/`
- [ ] File count and structure documented in `architecture.md`
- [ ] Any non-essential files identified and excluded (build artifacts, node_modules, caches)

### Brain Indexing
- [ ] `Projects/<ProjectName>/<ProjectName>_overview.md` created — status, summary, goals, stack
- [ ] `Projects/<ProjectName>/<ProjectName>_architecture.md` created — design, structure, file layout
- [ ] `Projects/<ProjectName>/<ProjectName>_requirements.md` created — dependencies, credential refs, setup
- [ ] `Projects/<ProjectName>/<ProjectName>_decisions.md` created — key decisions and rationale
- [ ] `Projects/<ProjectName>/<ProjectName>_changelog.md` created — this checklist + migration notes

### Technical Assessment
- [ ] **Typing status** documented in `architecture.md` (strongly typed / untyped / mixed)
- [ ] **Language(s)** and **framework(s)** recorded
- [ ] **External dependencies** listed (npm packages, pip packages, system tools)
- [ ] **API integrations** identified and linked to `Knowledge/APIs/` entries
- [ ] **MCP server requirements** identified and linked to `Agents/` entries

### Credential Audit
- [ ] All required credentials identified by **name only** in `requirements.md`
- [ ] No credential values stored anywhere in the vault (verified)
- [ ] Credentials added to `<workspace-root>/credentials.env` template (names only if values not yet available)

### Synapses
- [ ] Links to related projects created (if any exist)
- [ ] Links to relevant agent profiles created
- [ ] Links to relevant `Knowledge/` entries created
- [ ] Links to relevant `Knowledge/Patterns/` entries created
- [ ] No unnecessary or vague connections added

### Registry Updates
- [ ] Entry added to `Meta/migration-log.md`
- [ ] Entry added to `_Index.md`

### Runtime Setup (Body's Responsibility)
- [ ] Project-level `CLAUDE.md` created in project directory
- [ ] Project-level `requirements.md` duplicated to project directory
- [ ] External dependencies installable (package.json / requirements.txt / etc.)
- [ ] Credentials populated in `credentials.env` (or gaps reported to user)
- [ ] Project runs or clear error reported to user

### Gaps & Follow-ups
- [ ] Missing information documented (what the Body needs to provide later)
- [ ] Known issues or broken functionality noted
- [ ] User notified of all gaps and required manual setup steps
