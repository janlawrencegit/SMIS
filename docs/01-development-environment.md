# Development environment and skills report

Covers section 30.F of the master specification. Generated 2026-11-21.

## 1. Development environment

| Component | Version | Notes |
|-----------|---------|-------|
| OS | Ubuntu 24.04.5 LTS, Linux 6.18 x86_64 | Ephemeral cloud container; everything worth keeping is committed |
| Claude Code | 2.1.330 | |
| PHP | 8.3.6 | Extensions present: pdo_pgsql, pgsql, redis, intl, gd, zip. **Missing: bcmath** (money is stored as integer cents, so not required) |
| Composer | 2.8.12 | |
| Node.js / npm | 22.23.5 / 10.9.9 | |
| Git | 2.43.0 | |
| PostgreSQL | 16 (client and server) | Primary database |
| Redis | installed | Queues and cache |
| Python / uv | 3.13.18 / 0.11.32 | Used by the UI UX Pro Max scripts and the Graphify CLI |
| Chromium + Playwright | pre-installed | End-to-end tests and the webapp-testing skill |

Claude Code configuration before this work: no project `.claude/` folder; no user-level skills except the
environment's built-in `session-start-hook`; built-in plugins `anthropic-skills`, `design`, `productivity`.
Nothing was changed at the global level apart from the Graphify CLI (see §4).

## 2. Chosen stack

| Layer | Choice | Why |
|-------|--------|-----|
| Backend | Laravel 13 (PHP 8.3) | Mature queues, policies, PDF generation, migrations; known to the team from FinDesk |
| Database | PostgreSQL 16 | Check/exclusion constraints (no double-booked rooms or overlapping terms), JSONB for configurable grading schemes, strong transactional guarantees |
| Frontend | Inertia.js + Vue 3 + TypeScript | Single-page behaviour without a separate token API for the portals; typed reusable components |
| Styling | Tailwind CSS 4 with a custom design system | A distinct university identity instead of stock Bootstrap |
| Integrations | Versioned REST API `/api/v1` (Sanctum tokens) | Mobile and third-party systems |
| Auth/permissions | Laravel session auth + `spatie/laravel-permission` | Users can hold several roles; permissions are scoped |
| Queue/cache | Redis | |
| Tests | Pest (backend), Vitest (frontend), Playwright (end to end) | |

## 3. Installed skills inventory

All skills are installed at **project level** in `.claude/skills/` (copied files, pinned to the commit below).
No plugin was enabled, so **no plugin hooks and no MCP servers are active**.

| Skill(s) | Source repository @ commit | Upstream version | Scope | Status | Purpose here |
|----------|----------------------------|------------------|-------|--------|--------------|
| brainstorming, writing-plans, executing-plans, subagent-driven-development, dispatching-parallel-agents, test-driven-development, systematic-debugging, verification-before-completion, requesting-code-review, receiving-code-review, using-git-worktrees, finishing-a-development-branch, writing-skills, using-superpowers, diagnosing-superpowers | obra/superpowers @ 22f0b46 | see repo | project | installed (15) | Development workflow |
| impeccable | pbakaus/impeccable @ b49177d | see `scripts/VERSION` | project | installed; engine binary **not downloaded** | Interface critique and refinement |
| design-taste-frontend | Leonxlnx/taste-skill @ f6b7657 | 2.5.1 | project | installed; **its Stop hook removed** (pending approval) | Visual quality of the public site and dashboards |
| ui-ux-pro-max, design-system | nextlevelbuilder/ui-ux-pro-max-skill @ 2de1134 | 2.15.0 | project | installed; search script tested | Design-system research |
| reverse-engineer-anything | morluto/rea @ e94475b | 6.10.1 | project | installed (skill only); **MCP server not enabled** | Analysing reference applications |
| graphify | safishamsi/graphify @ b582ad4 (PyPI `graphifyy` 0.9.114) | 0.9.114 | skill: project; CLI: user (`uv tool`) | installed; CLI tested | Architecture and dependency graphs |
| frontend-design, webapp-testing | anthropics/skills @ e4bb5d9 | — | project | installed | Official frontend guidance; Playwright app testing |
| laravel-patterns, laravel-security, laravel-tdd, laravel-verification, postgres-patterns, database-migrations, api-design, vue-patterns, typescript-patterns, frontend-a11y, e2e-testing, architecture-decision-records | affaan-m/everything-claude-code @ 4adeee6 | see `VERSION` | project | installed (12 of 328) | Stack-specific engineering practice |
| karpathy-guidelines | multica-ai/andrej-karpathy-skills @ 2c60614 | — | project | installed | Simplicity and verification discipline |

Total: 36 skills.

**Recognition by Claude Code.** Claude Code reads project skills when a session starts. They are expected to
appear in the next session opened on this repository; this document will be updated once that is confirmed.
Copying files is not the same as "recognized", and no skill is marked verified until then.

### Not installed, and why

| Item | Reason |
|------|--------|
| anthropics/skills `docx`, `pdf`, `xlsx`, `pptx` | Already available in this environment through the built-in `anthropic-skills` plugin; installing them again would create duplicates |
| ECC `security-review` | Would shadow Claude Code's built-in `/security-review` |
| ECC `tdd-workflow`, `verification-loop`, `coding-standards` | Duplicate Superpowers' TDD and verification skills |
| The other 316 ECC skills | Not relevant to this stack (other languages, trading, scientific databases, …) |
| ui-ux-pro-max `slides`, `banner-design`, `brand`, `ui-styling` | Not needed for UMIS |
| REA maintenance skills (`rea-changelog-update`, `rea-ci-tests-audit`, …) | They maintain the REA repo itself |

## 4. Plugin, hook and permission report

| Source | What it would add | Current state | Risk notes |
|--------|-------------------|---------------|------------|
| Superpowers plugin | SessionStart hook that injects `using-superpowers` into every session | **Not enabled.** The skill is installed and loads when relevant | Script only reads a local file; low risk. Could be enabled later |
| Impeccable plugin | SessionStart, PostToolUse (every Edit/Write) and Stop hooks running its engine | **Not enabled** | The engine is a native binary downloaded from GitHub releases (checksum-verified against `engine-checksums.txt`). Runs on every edit |
| Taste skill | Stop hook in the skill header: runs `node scripts/gate.mjs` (up to 600 s) while the skill is active | **Removed**; original saved in `.claude/skills/design-taste-frontend/SKILL.md.upstream-hooks.yaml` | Opens a real browser to check pages; slow |
| REA plugin | MCP server via `npx rea-agents@6.10.1` | **Not enabled** | Pulls an npm package at run time; binary-analysis engines are heavy and mostly not needed for a web project |
| ECC plugin | Many hooks (`hooks/hooks.json`, memory persistence) and an `.mcp.json` | **Not enabled** | Broad; only selected skills copied |
| UI UX Pro Max `stack/.mcp.json` | Playwright, Chrome DevTools, shadcn MCP servers (`@latest`, unpinned) | **Not enabled** | Unpinned versions; Playwright is already available directly |
| Graphify CLI | `graphify`, `graphify-mcp` executables in `~/.local/bin` | Installed with `uv tool install graphifyy==0.9.114`; MCP **not** registered; `graphify install` (which edits CLAUDE.md) **not** run | Lives outside the repo, so it disappears with the container; reinstall with the same command |

No permissions were added to any `settings.json`.

## 5. Changes made to upstream files

| File | Change | Reason |
|------|--------|--------|
| `design-taste-frontend/SKILL.md` | Removed the `hooks:` block from the header | Hooks need explicit approval |
| `ui-ux-pro-max/SKILL.md` | `${CLAUDE_PLUGIN_ROOT}/.claude/skills/ui-ux-pro-max` → `.claude/skills/ui-ux-pro-max` | The variable only exists for plugins; commands now run from the repo root |
| `graphify/SKILL.md` | Copied from `graphify/skill.md`; the `references/` folder from `graphify/skills/claude/` | Matches what `graphify install` would place, without editing CLAUDE.md |
| `taste-skill/` → `design-taste-frontend/` | Folder renamed | Must match the skill's declared name |

## 6. Verification performed

| Check | Result |
|-------|--------|
| Every `SKILL.md` declares a `name` that matches its folder | Pass (after the Taste rename) |
| Skills declaring hooks or tool permissions in their header | Only Taste, now removed |
| `ui-ux-pro-max` search script, run from the repo root | Pass: returned style results for "university education dashboard" |
| `graphify update` on a sample codebase | Pass: produced graph.json, graph.html, GRAPH_REPORT.md (sample output deleted afterwards) |
| Skills recognised by Claude Code | **Pending**: needs a new session |

## 7. Skill conflicts and resolutions

| Overlap | Resolution |
|---------|------------|
| Frontend design: `frontend-design` (Anthropic), `design-taste-frontend` (Taste), `impeccable`, `ui-ux-pro-max` | Each has one job. UI UX Pro Max researches and proposes the design system; Anthropic `frontend-design` sets the build approach; Taste is used for the **public website** and visual polish; Impeccable **critiques** finished screens. If they disagree, accessibility and usability come first, then consistency with `docs/design-system.md` once it exists |
| Taste targets marketing sites ("one section per screen", shader effects) | Applied only to the public website, never to data-heavy portal screens |
| TDD: Superpowers `test-driven-development` vs ECC `laravel-tdd` | Superpowers sets the cycle (red, green, refactor); ECC supplies the Laravel/Pest specifics |
| Verification: Superpowers `verification-before-completion` vs ECC `laravel-verification` | Same split: general rule from Superpowers, concrete commands from ECC |
| Planning: Superpowers `writing-plans` vs Karpathy "simplicity" | Plans are detailed; each step's code is minimal |
| Accessibility: ECC `frontend-a11y`, Impeccable, design plugin's `accessibility-review` | WCAG 2.1 AA is the bar; `frontend-a11y` during build, `accessibility-review` as the audit |

## 8. Recommended skill workflow

| Task | Skills to use |
|------|---------------|
| Start a module | `brainstorming` → `writing-plans`, plus `architecture-decision-records` for decisions |
| Database work | `postgres-patterns`, `database-migrations` |
| Backend features | `test-driven-development` + `laravel-tdd`, `laravel-patterns`, `api-design`, `laravel-security` |
| Frontend components | `vue-patterns`, `typescript-patterns`, `frontend-design`, `frontend-a11y` |
| Design system | `ui-ux-pro-max`, `design-system` |
| Public website | `design-taste-frontend`, then `impeccable` critique |
| Portal screens | `frontend-design`, then `impeccable` critique and an accessibility audit |
| Bugs | `systematic-debugging` |
| Before saying "done" | `verification-before-completion` + `laravel-verification`, `e2e-testing` / `webapp-testing` |
| Understanding the codebase | `graphify` |
| Studying a reference system | `reverse-engineer-anything` |
| Always | `karpathy-guidelines`: smallest change that works, verify it |

## 9. Reinstalling

Project skills come with the repository. In a fresh container, only the Graphify CLI needs reinstalling:

```bash
uv tool install graphifyy==0.9.114
```

## 10. Awaiting approval

- Enable the Superpowers SessionStart hook?
- Enable the Taste Stop hook (restore from `SKILL.md.upstream-hooks.yaml`)?
- Download the Impeccable engine and enable its hooks?
- Enable the REA MCP server?
