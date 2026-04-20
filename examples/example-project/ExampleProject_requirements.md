# ExampleProject — Requirements

## Runtime
- Python 3.11+ / Node.js 20+ / etc.

## Package Dependencies
- [lib A — purpose]
- [lib B — purpose]

## External Services
- [[Knowledge/APIs/<api-name>]]

## Credential References
> Only credential **names** live here. Values live in `<workspace-root>/credentials.env`.

- `OPENAI_API_KEY` — LLM calls
- `DATABASE_URL` — Postgres connection string

## Setup Steps
1. `cp credentials.env.example credentials.env` (at workspace root).
2. Populate the credentials listed above.
3. Install dependencies: `pip install -r requirements.txt` / `npm install` / etc.
4. Run: `[command]`.

## Known Gaps / Follow-ups
- [missing credential or dependency the user still needs to provide]
