# Open questions and decisions

Tracks what must be settled before Phase 1 planning. Answers are recorded here as they arrive.

## Blocking (required before planning)

| # | Question | Answer |
|---|----------|--------|
| 1 | Master specification sections 1–29 (only section 30, skills/tooling, has been provided) | _pending_ |
| 2 | Module scope (admissions, enrollment, curriculum, scheduling, grading/transcripts, fees, scholarships, faculty loading, HR/payroll, library, clinic, dormitory, alumni, public site, portals) | _pending_ |
| 3 | Roles, and whether one user may hold several | _pending_ |
| 4 | Country/regulatory context, grading scale, term structure, government reports | _pending_ |
| 13 | Approval to install the nine skill repos at project level under the review conditions below | _pending_ |

## Defaults (used unless overridden)

| # | Topic | Default |
|---|-------|---------|
| 5 | Stack | Laravel 13 + Vue 3 + Bootstrap 5, server-rendered pages with Vue islands |
| 6 | Database | MySQL in production, SQLite for tests |
| 7 | Roles/permissions | `spatie/laravel-permission` |
| 8 | Tenancy | One university, several campuses |
| 9 | Payments | Cashier-recorded manually; gateway can be added later |
| 10 | Email / SMS / files | Email to log, no SMS, files on local disk |
| 11 | Pace | Push after every working piece |
| 12 | Branching | One branch and pull request per phase |
| 14 | FinDesk | Separate codebase; reuse patterns (toasts, strict CSP, test setup), no business code |

## Skill installation conditions (item 13)

- Install into this repo's `.claude/` only; no global changes.
- Read each repo (hooks, scripts, MCP servers, permissions) before enabling it.
- Never run an unreviewed remote install script.
- Ask before enabling any hook that runs code automatically.
- Mark a skill "not usable here" if it needs binaries or tools on the user's own machine (possible for REA, Graphify).
- New skills load at session start, so they take effect from the next session.
