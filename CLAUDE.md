# pi-monorepo

TypeScript monorepo for the pi agent tooling. Packages live under `packages/`, and `apps/` holds applications.

## Project Structure

- `packages/` — Workspace packages (ai, agent, tui, coding-agent, and others)
- `apps/` — Applications outside the root check
- `scripts/` — Build and maintenance scripts
- `.github/` — CI workflows and templates

## Development

- Full checks: `npm run check` (no tests)
- Non-e2e tests: `./test.sh`
- Build output: `npm run build`

## Guidelines

The authoritative rules are in `AGENTS.md`. Read it before making changes. Do not duplicate them here.

## Reference

- Contributing: `CONTRIBUTING.md`
- Security policy: `SECURITY.md`

---

*Keep this file concise. Reference documentation files instead of copying content.*
