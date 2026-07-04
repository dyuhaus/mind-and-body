---
tags: [meta, reference]
cssclasses: [meta-doc]
---
# Dictionary

Definitions of terms used within the AI_Brain system.

---

| Term | Definition |
|------|-----------|
| **Synapse** | An Obsidian link (`[[target]]`) representing a meaningful connection between two knowledge entries. |
| **Connected Thought** | Reasoning across multiple Synapses to surface relationships and dependencies between knowledge areas. |
| **Hallucination** | Information fabricated by the Mind without source data from the Body. Strictly prohibited. |
| **Brain / Vault** | The AI_Brain Obsidian vault — the sole persistent knowledge store. |
| **Mind** | The agent that operates inside the vault. Stores, retrieves, and connects information. |
| **Body** | The agent that operates outside the vault. Executes tasks and interacts with the user. |
| **Migration** | The process of importing an existing project into the workspace and indexing its context in the Brain. |
| **Credential Reference** | A credential name (e.g., `OPENROUTER_API_KEY`) stored in the Brain. The actual value lives only in `credentials.env`. |

## Related
- [[Agents/Mind]] — The Mind agent defined above
- [[Agents/Body]] — The Body agent defined above
- [[Meta/system-architecture]] — Full system design using these terms
- [[Meta/connection-policy]] — Governs Synapse creation rules
- [[Meta/migration-checklist]] — Defines the Migration process
