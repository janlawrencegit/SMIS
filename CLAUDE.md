# UMIS — University Management Information System

Status: pre-planning. See `docs/00-open-questions.md` and `docs/01-development-environment.md`.

- Stack: Laravel 13 + PostgreSQL 16 + Inertia/Vue 3/TypeScript + Tailwind 4; Redis; Pest, Vitest, Playwright.
- Project skills live in `.claude/skills/`. Choose skills per task using the workflow table in
  `docs/01-development-environment.md` §8; do not apply every skill to every task.
- Conflicting guidance is resolved by: accessibility, usability, consistency, maintainability, then the project design system.
- No plugin hooks or MCP servers are enabled; do not enable any without the user's approval.
- Graphify CLI is not part of the repo: `uv tool install graphifyy==0.9.114`. Keep `graphify-out/` out of git.
- Do not move to a dependent module until its prerequisites pass their tests. Pause for review after each phase.
