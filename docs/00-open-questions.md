# Decisions and open questions

## Decided

| Topic | Decision |
|-------|----------|
| Name | **SMIS** (School Management Information System). The GitHub repository is still named `UMIS` until the owner renames it |
| Scope | **Junior high and senior high only** (Grades 7–12), DepEd rules. Changed from university scope |
| School type | **Public or private, as a setting** (public: no tuition, no-collection policy; private: tuition, cashiering, ESC / SHS Voucher) |
| Number of schools | **One school** (campuses can be added later) |
| Country | Philippines (DepEd, Data Privacy Act, BIR) |
| Grading and terms | Versioned configuration; DepEd rules (DO 8 s.2015 legacy, DO 015 s.2026) as defaults |
| Stack | Laravel 13 + PostgreSQL 16 + Inertia/Vue 3/TypeScript + Tailwind 4; Redis; Pest, Vitest, Playwright |
| Specification | Researched by Claude (the earlier ChatGPT-written spec is not used) |
| Skills | Nine skill repos installed at project level; see `01-development-environment.md` |
| Pace | Pause for review after each phase; push after every working piece |

## Defaults (used unless overridden)

| Topic | Default |
|-------|---------|
| Roles/permissions | Scoped role assignments (custom table), separation of duties |
| Payments | Manual cashier posting plus one gateway (PayMongo) |
| Email / SMS / files | Email to log, SMS provider chosen later, files on local disk |
| Branching | One branch and pull request per phase |
| FinDesk | Separate codebase; no code copied |

## Open

| Question | Status |
|----------|--------|
| Review of the SMIS master specification | Pending |
| Items in the specification's verification register (DepEd orders read via secondary sources, BIR e-invoicing coverage) | Pending |
| Optional hooks (Superpowers, Taste, Impeccable engine, REA MCP) | Pending approval |
