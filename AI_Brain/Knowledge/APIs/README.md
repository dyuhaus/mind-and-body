# APIs

One file per external API the system integrates with. File naming: lowercase, hyphenated (e.g., `openai.md`, `stripe.md`, `financial-modeling-prep.md`).

## Template

```markdown
# <API Name>

## Purpose
[What this API provides]

## Credentials
- Required environment variables: [NAME_1, NAME_2]

## Endpoints Used
- [endpoint 1] — [what it's used for]
- [endpoint 2] — [what it's used for]

## Rate Limits / Quotas
- [limits observed]

## Notes
- [gotchas, edge cases, version-specific behavior]

## Related Projects
- [[Projects/ProjectName/ProjectName_overview]]
```
