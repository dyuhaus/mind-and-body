---
tags: [meta, policy]
cssclasses: [meta-doc]
---
# Connection Policy

Rules governing when Synapses (Obsidian links) should be created between knowledge entries.

---

## Create a Synapse When

- **Direct dependency**: Project A uses API B → link `overview.md` to `Knowledge/APIs/B.md`.
- **Shared agent**: Two projects use the same agent → both link to `Agents/AgentName.md`.
- **Decision influence**: A decision in Project A was informed by a pattern or outcome in Project B.
- **Prerequisite knowledge**: Understanding topic A requires context from topic B.
- **Credential sharing**: Multiple projects reference the same credential name.

## Do NOT Create a Synapse When

- The connection is superficial (e.g., "both are Python projects").
- The link would be one of 10+ outgoing links on a single file (sign of noise).
- The target file doesn't exist and isn't planned for creation.
- The relationship is temporal only ("worked on these the same week").
- The connection requires explanation to justify — if it's not obvious, it's probably not meaningful.

## Maintenance

- When editing a file, audit its outgoing Synapses. Remove any that are stale or broken.
- Prefer specific section links: `[[Projects/<ProjectName>/<ProjectName>_architecture#Stack]]` over generic file links.
- If a Synapse is removed, check the target file — does it still link back? Clean up both sides.

## Related
- [[Agents/Mind]] — Responsible for implementing this policy
- [[Meta/dictionary#Synapse]] — Definition of what a Synapse is
- [[Meta/system-architecture]] — System context for vault connectivity
