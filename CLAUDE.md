# SMIS — School Management Information System

Single Philippine JHS–SHS school (Grades 7–12, DepEd); public or private mode is a setting. Pre-planning.
Master spec: `docs/research/reports/DepEd JHS SHS school system spec.md`. Decisions: `docs/00-open-questions.md`.
The university-scope `UMIS master specification.md` is superseded; use it only for platform/security/ledger/API patterns.

- Stack: Laravel 13 + PostgreSQL 16 + Inertia/Vue 3/TypeScript + Tailwind 4; Redis; Pest, Vitest, Playwright.
- Grading rules, terms, weights, transmutation tables and fee rules are versioned configuration, never code constants.
- Project skills live in `.claude/skills/`. Choose skills per task using `docs/01-development-environment.md` §8.
- Conflicting guidance is resolved by: accessibility, usability, consistency, maintainability, then the project design system.
- No plugin hooks or MCP servers are enabled; do not enable any without the user's approval.
- Graphify CLI is not part of the repo: `uv tool install graphifyy==0.9.114`. Keep `graphify-out/` out of git.
- Do not move to a dependent module until its prerequisites pass their tests. Pause for review after each phase.
