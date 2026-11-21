# Build SMIS on versioned DepEd rules

SMIS should be built as one codebase with a single school-mode switch (public or private) and a versioned rules store. Every DepEd grading scheme, term structure, weight matrix, transmutation table, fee schedule, subsidy rate and deadline is dated configuration data, not code. The reason is concrete. Learners in one building, in one school year, now fall under different rule sets. **DepEd Order No. 015, s. 2026 (signed 4 June 2026) repealed DO 8 s.2015 and DO 36 s.2016** ([Philstar](https://www.philstar.com/headlines/2026/06/22/2537040/deped-starts-phaseout-grade-transmutation-policy)). It brings three terms, new weights, an adjusted transmutation table for SY 2026–27 (initial grade 70 → 75) and no transmutation from SY 2027–28. In SY 2026–27 Grade 11 is on the Strengthened SHS curriculum while most Grade 12 learners stay on the legacy track/strand curriculum. **DO 017, s. 2025 replaced the 2018 enrollment policy** ([DO 017 reproduction](https://eduknasyon.blogspot.com/2025/06/deped-order-017-s-2025-revised-basic.html)). DO 009, s. 2026 sets a three-term calendar that public schools must use and private schools may use ([GMA](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/)). DepEd's Learner Information System (LIS) stays the official enrollment record, so SMIS is a single-entry local source of truth that produces LIS-ready data and the School Forms. It does not replace the LIS. Private mode adds what public mode must never have: tuition under DO 88 s.2010, cashiering, holds on credentials (allowed, but with obligations to accommodate the learner under DepEd Memorandum 023 s.2026), ESC and SHS Voucher sponsor billing under the new E-GASTPE order (DO 11 s.2026), and BIR invoicing. The BIR e-invoicing deadline of **31 Dec 2026** falls before any realistic go-live. Phase 1 should therefore target SY 2027–28. That year runs entirely on zero-based DO 15 grading, and the legacy and transition schemes are needed for history import and summer remediation. Most 2026 DepEd orders were read only through secondary or division-level reproductions because deped.gov.ph returned HTTP 403. The verification register at the end is a gating checklist, not an appendix.

## How to read this specification

### Six evidence tags keep primary text apart from summaries and design

The specification is synthesized from five research notes compiled on 21 Nov 2026, with reuse from the earlier UMIS university specification and its public-website notes. Each requirement row carries a basis tag:

| Tag | Meaning | Treat as |
|---|---|---|
| **[P]** | Primary text read in the session: DepEd issuance or LIS Support page, Official Gazette/LawPhil, NPC, W3C, web.dev, a vendor's own pricing page | Reliable; still re-check section numbers |
| **[D]** | Full-text reproduction of a primary issuance by a DepEd regional or division office, or a faithful full-text blog reproduction (e.g., DO 017 s.2025, DM 023 s.2026) | Probably accurate; confirm against the signed PDF before hard rules |
| **[N]** | Reputable news or professional-firm reporting of an issuance (GMA, Philstar, Manila Bulletin, PwC, KPMG, Grant Thornton) | Headline facts reliable, detail may be lost |
| **[S]** | Secondary summary: teacher portals (DepEdClub, SchoolFinderPH, tchersden, TeachPinas), law-firm commentary, vendor blogs | Never seed as final values without confirmation |
| **[K]** | Prior knowledge of a statute or order, not re-fetched in the session (DO 8 s.2015 tables, DO 36 s.2016, RA 4670, RA 10627, EOPT invoicing) | High likelihood; verify before quoting |
| **[I]** | Design inference: a proposed SMIS requirement drawn from the evidence, not stated by any source | Product decision, open to change |

A requirement can carry two tags, such as "[S]; [I]", when an inferred design rests on a secondary-sourced value. Everything tagged [D], [S] or [K] that drives a rule reappears in the verification register.

### Four project constraints override anything in the notes

The repository is still named UMIS. SMIS is the working product name for a single Philippine JHS–SHS school (Grades 7–12). The stack is Laravel 13, PostgreSQL 16, Inertia + Vue 3 + TypeScript, Tailwind 4 and Redis, tested with Pest, Vitest and Playwright. **Grading rules, terms, weights, transmutation tables, descriptors, promotion thresholds, award criteria, fee rules, subsidy rates and statutory windows are versioned configuration**, keyed by school year and effective date. DepEd values are seed data only. SMIS defines its own double-entry ledger and its own Vue notification layer; no code from other projects (such as FinDesk's ledger or toasts) is reused. The earlier UMIS specification contributes only its platform layer, scoped roles with separation of duties, append-only audit log, double-entry ledger with reversals, API conventions and security baselines. Its CHED, HEMIS, RA 10931, Special Order, degree-audit and university-scheduling content is dropped.

### DepEd reuses issuance numbers every year, so cite number plus series

Several 2024–2026 issuances share numbers with unrelated orders. Mixing them up is a real risk in configuration and documentation, so SMIS configuration records must always store the full citation (type, number, series, date).

| Number | Issuance | Topic |
|---|---|---|
| DO 017 | s. 2025 (13 Jun 2025) | Revised Basic Education Enrollment Policy |
| DO 017 | s. 2026 (4 Jun 2026) | Strengthened SHS Curriculum (number unverified) |
| DO 015 | s. 2026 (4 Jun 2026) | Classroom assessment, grading, awards |
| DO 012 | s. 2024 | MATATAG flexible time-allotment amendment (number unverified) |
| DO 012 | s. 2025 | Multi-year school calendar |
| DO 012 | s. 2026 | Government Recognition for private SHS |
| DO 011 | s. 2018 | Checking of school forms |
| DO 011 | s. 2026 | Revised E-GASTPE (ESC, SHS VP, TSS) |
| DO 007 | s. 2024 | Revised School-Based Management |
| DO 007 | s. 2026 | Media Management Guidelines |
| DO 006 | s. 2026 | Safe and Motivating Learning Environment (ESMLE) |
| DO 006 | s. 2025 | Cited by one blog as a forms-streamlining order (unverified) |
| DO 005 | s. 2024 | Teacher workload rationalization |

## Three regulatory clocks set the Phase 1 target year

### SY 2026–27 runs three grading regimes side by side

The grading engine is the clearest case for versioned rules. DO 15 s.2026 applies to public schools from SY 2026–27. Private schools are "encouraged" to adopt it and may modify it with DepEd Regional Office approval ([SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-new-grading-system-2026)) [S]. The transition year uses an **adjusted transmutation table** where initial grade (IG) 70.00 maps to 75. Under the old table IG 60 mapped to 75, so IG 60 now transmutes to 72 and fails. From SY 2027–28 there is no transmutation for Grades 4–12, a report-card floor of 60 and a passing mark of 75 ([GMA](https://www.gmanetwork.com/news/topstories/nation/992328/deped-phase-out-grade-transmutation-schools/story/); [DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/)) [N]/[S]. Grade 12 learners on the legacy curriculum in SY 2026–27 use **DO 8 weights with the adjusted table** ([DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/)) [S], a hybrid that no single order describes in full.

| School year | Grades 7–10 | Grade 11 | Grade 12 |
|---|---|---|---|
| ≤ 2025–26 | MATATAG phasing in (G7 2024–25, G8 2025–26). DO 8 s.2015: 4 quarters, WW/PT/QA, legacy transmutation. DO 36 honors tiers | Legacy track/strand. SSHS pilot in ~800–891 schools | Legacy track/strand, 2 semesters × 2 quarters |
| 2026–27 | DO 15 weights, **3 terms**, adjusted table. G9 on MATATAG; G10 rollout year disputed | **SSHS for all schools**, DO 15 SHS subject-group weights, adjusted table | **Legacy curriculum + DO 8 weights + adjusted table** (pilot-school G12: SSHS) |
| ≥ 2027–28 | DO 15 zero-based, no transmutation | DO 15 zero-based | First full SSHS Grade 12 cohort, zero-based |

Sources: [Manila Bulletin](https://mb.com.ph/2024/7/28/dep-ed-releases-policy-guidelines-for-matatag-curriculum-implementation-for-sy-2024-2025) [N]; [SchoolFinderPH](https://www.schoolfinderph.com/blog/strengthened-shs-curriculum) [S]; [LIS PPS Advisory](https://support.lis.deped.gov.ph/support/Manuals/ADVISORY-SHS-Pilot.pdf) [P]; [LIS Support bulletin](https://support.lis.deped.gov.ph/support/) [P].

The curriculum version must therefore attach to the **learner-section enrollment**, not to the grade level. Pilot-school Grade 12 learners and retained learners break any grade-level shortcut [I]. The LIS confirms the split: from 30 Sep 2026 "all Grade 11 learners shall be enrolled under the Strengthened Senior High School (SSHS) program, including Grade 12 learners under the SSHS pilot schools", while other Grade 12 learners stay on the regular program ([LIS Support](https://support.lis.deped.gov.ph/support/)) [P].

### The tax clock runs out before any realistic go-live

BIR RR 26-2025 moved the e-invoicing deadline for covered taxpayers to **31 Dec 2026**, and RMC 98-2026 (22 Sep 2026) kept it ([Grant Thornton](https://www.grantthornton.com.ph/technical-alerts/tax-alert/2026/bir-issues-guidelines-on-electronic-invoicing-retains-31-dec-2026-deadline/)) [N]. Coverage in secondary sources is large taxpayers, e-commerce, exporters and **CAS/CBA users**, with micro taxpayers excluded ([KPMG](https://kpmg.com/us/en/taxnewsflash/news/2026/09/philippines-e-invoicing-required-dec-31-2026.html)) [N]. A private school that prints invoices from a computerized system is likely a CAS/CBA user [I]. No source addressed schools directly. As of 14 Sep 2026 no e-invoicing service provider was BIR-accredited ([KPMG PH](https://kpmg.com/ph/en/insights/2026/09/special-intax-september-2026-issue-1-volume-2.html)) [N]. A private-mode school therefore needs a coverage determination from its RDO now. If it is covered, it must comply through its current system or a provider before SMIS exists, and SMIS's invoicing must be EIS-ready on day one.

### Go-live for SY 2027–28 simplifies the live engine and complicates migration

SY 2026–27 is well under way: classes opened 8 June 2026 and close 8 April 2027 ([GMA](https://www.gmanetwork.com/news/topstories/nation/984611/deped-classes-to-start-june-8-end-april-8-under-3-term-calendar/story/)) [N]. The next natural cut-over is SY 2027–28. Its public-school early registration runs from the last Saturday of January to the last Friday of February 2027 ([DO 017 reproduction](https://eduknasyon.blogspot.com/2025/06/deped-order-017-s-2025-revised-basic.html)) [D], and its classes probably open in June 2027 (no calendar order found). A SY 2027–28 go-live means **every live grade runs the zero-based DO 15 scheme**. The legacy DO 8 scheme and the transition scheme are still needed for three things: importing SF10 history, computing summer remedial classes for SY 2026–27 (which run between April and June 2027), and generating certified copies of past records [I]. That cuts live-engine risk sharply but makes historical data migration a Phase 1 deliverable in its own right.

## A twenty-step dependency chain fixes the build order

The dependencies follow the same foundation-first logic as university systems. Configuration and calendar come before curriculum. Curriculum comes before sections. Enrollment comes before attendance and grades. Grades come before promotion, awards and the School Forms. Finance in private mode depends on enrollment and approved fee schedules. The phase proposals are design recommendations [I].

| Step | Module(s) | Hard dependencies | Proposed phase |
|---|---|---|---|
| 1 | Platform: identity/SSO, scoped RBAC, audit log, numbering, workflow, notifications, document generation, import/export, holds framework | — | Phase 0 |
| 2 | Rules store and school profile: school mode (public/private), School ID, tax profile, location tier (NCR/HUC/other), versioned policy sets | 1 | Phase 0 |
| 3 | School year, calendar, grading periods (quarter/semester/term), class days, suspensions | 2 | Phase 0 |
| 4 | Curriculum: learning areas/subjects (versioned), subject groups, MATATAG and legacy JHS, SSHS and legacy SHS programs, time allotments | 2–3 | Phase 0 |
| 5 | Grading-scheme library: DO 8 legacy, DO 15 transition, DO 15 zero-based seeds; descriptors; promotion and award rule sets | 2–4 | Phase 0 (configured), Phase 1 (live) |
| 6 | Person, learner, guardian, LRN, documents, consents | 1 | Phase 1 |
| 7 | Personnel (minimal): teachers, advisers, counselors, staff; licences; designations | 1, 6 | Phase 1 (minimal); full HR Phase 3 |
| 8 | Historical migration: learners, SF10 history, grades under legacy and transition schemes, balances (private) | 4–6 | Phase 1 |
| 9 | Enrollment: early registration, BEEF, confirmation slips, document checklist, statuses, LIS worksheets | 3, 4, 6 | Phase 1 |
| 10 | Class programs, sections, rooms, teacher loading | 4, 7, 9 | Phase 1 |
| 11 | Fee schedules, payment plans, ledger, subsidy programs (private) | 2–4 | Phase 1 (private mode) |
| 12 | Assessment, cashiering, invoicing, promissory notes, credential holds (private) | 9, 11 | Phase 1 (private mode) |
| 13 | Attendance (daily, SF2/SF4, at-risk alerts) | 9, 10 | Phase 1 |
| 14 | Class records and grading, term grades, SF9 | 5, 10, 13 | Phase 1 |
| 15 | Promotion, remedial, retention, awards, SF5/SF6, SF10, certificates, records release | 14 | Phase 1 |
| 16 | Parent and learner portal, SMS/email notifications | 9, 13, 14, 12 | Phase 1 (core views); messaging Phase 2 |
| 17 | Public website and CMS, inquiry/early-registration funnel, QR verification | 4, 9, 15 | Phase 1 (core site, verification); funnel CRM Phase 2 |
| 18 | Learner welfare: incidents (DO 006), CPC case timelines, guidance, health (SF8) | 6, 9 | Phase 1 (incident database and deadlines); guidance/health depth Phase 2 |
| 19 | Integrations: payment gateway, Google Workspace/Classroom, SMS gateway, ESC IMS/VMS billing exports, BIR EIS | 12, 14, 16 | Gateway + SMS Phase 1; Classroom and subsidy exports Phase 2; EIS per coverage finding |
| 20 | DepEd reporting and planning: LIS exports, BEIS profile, SBM/SIP evidence (public), MOOE (public), analytics | All | Phase 1 (LIS/SF exports); SBM/MOOE Phase 2; analytics Phase 3 |

Every Phase 1 module must work end to end for one full school-year cycle: register, enroll, section, attend, grade, promote, report and, in private mode, bill and collect. A partial cut-over would leave a critical calculation in Excel, and the duplicate LIS-plus-Excel encoding is exactly the pain teachers already report ([TeachPinas](https://www.teachpinas.com/deped-school-forms-sf-1-10/)) [S].

## Module-by-module functional requirements

IDs are stable handles for backlog planning. A requirement marked (Pub) or (Pvt) applies only in that mode. Unmarked requirements apply in both.

### Platform and rules store: every DepEd value is a dated policy row

The platform layer is carried over from the UMIS specification with basic-education adjustments. The earlier design's key patterns were configurable holds with impacts and append-only histories, a draft → submitted → approved workflow routed to role and scope, and a policy store resolved most-specific-first with a mandatory default. They came from PeopleSoft service indicators, Workday business processes and Koha's rule matrix ([Oracle](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lscc/htm/lscc39.htm); [Workday](https://doc.workday.com/workday-education/en-us/course-manuals/security-for-administrators/security-policy-configuration-and-activation.html); [Koha](https://koha-community.org/manual/22.05/en/html/circulation.html)) [P]. For a single school the scope hierarchy collapses to school → key stage → grade level → program/track → section. The school-year dimension becomes the main version key.

| ID | Requirement / business rule | Basis |
|---|---|---|
| PLT-01 | One `Person` per human with an internal ULID. A person may hold several roles: learner, guardian, employee, applicant, alumnus. Public identifiers (LRN, employee no.) are attributes, never keys | UMIS spec; [I] |
| PLT-02 | `SchoolProfile` holds mode (`public`/`private`), School ID (6 digits), region/division, location tier for subsidies (NCR/HUC/other), tax profile (Pvt: non-stock non-profit vs proprietary), Government Recognition status per SY (Pvt SHS). Mode changes are a controlled migration, not a toggle | School ID: [Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf) [P]; [I] |
| PLT-03 | `PolicySet` versioning: every configurable rule (grading scheme, calendar, fee schedule, subsidy table, promotion rule, award rule, refund rule, LIS window, SLA timer) is a row set carrying `effective_sy`, `effective_from/to`, a source citation (issuance type, number, series, date), a verification status (`verified`/`secondary`/`prior_knowledge`/`school_policy`) and an approver. Rows lock once used by a finalized record. Changes create a new version | Project constraint; [I] |
| PLT-04 | The policy resolver picks the most specific scope (section > program > grade level > key stage > school) for a school year. Every policy type needs a school-level default | Koha pattern [P]; [I] |
| PLT-05 | Mode guards are enforced in the domain layer and the database. In public mode, finance tables, holds of type `financial` and fee-related policies cannot be written. Tests assert that no public-mode path can block enrollment, promotion, SF9/SF10 release or clearance on money | [DO 41 s.2012 coverage](https://www.pna.gov.ph/articles/1071316) [N]; [I] |
| PLT-06 | Configurable `HoldType` with `HoldImpact`s (release original SF10, release SF9, issue certificate, issue diploma, official promotion/graduation in system). Each hold records reason, office, placed-by, validity and release, with append-only history. Only the placing office or a delegate releases it. Holds can never impact exams, class attendance, EOSY rites or LIS transfer responses | Oracle [P]; RA 11984 [P]; DM 023 s.2026 [D] |
| PLT-07 | Workflow engine: versioned definitions, steps routed to role + scope, SLA timers with escalation, initiator ≠ approver where configured. Used for grade locking, grade changes, fee schedules, refunds, records release, incident cases | UMIS spec; [I] |
| PLT-08 | Gap-free numbering per series (certificate numbers, invoice series per terminal, record-release log numbers, incident numbers) | [I] |
| PLT-09 | Document generation: versioned templates (SF layouts per issuing memo), serial numbers, issuance log, signatory blocks, optional QR verification token (see WEB-10) | [I] |
| PLT-10 | Import/export framework (CSV/XLSX, validated, idempotent, logged) for LIS worksheets, legacy ECR spreadsheets, SF templates, bank and gateway settlements, ESC IMS/VMS billing | [I] |
| PLT-11 | Checklists, communication templates with logged sends, and categorized comments attachable to any learner record | PeopleSoft 3Cs [P] |
| PLT-12 | Offline tolerance: class-record entry works on an intermittent connection (local draft with conflict-checked sync) or via official-layout Excel import. Pages are small enough for low-bandwidth mobile use | Connectivity: [PhilStar](https://www.philstar.com/headlines/2025/07/28/2461427/marcos-vows-internet-access-all-public-schools-end-2025) [N]; [I] |

The API follows the conventions of the UMIS specification [K, ref not fetched]: plural resources with ULIDs and the LRN as a lookup key, explicit workflow actions (`POST /grade-sheets/{id}/lock`), URI versioning (`/api/v1`), cursor pagination with `updated_since`, RFC 9457 problem+json errors, a required `Idempotency-Key` on payments, refunds and enrollments, ETag/If-Match on grade sheets, and a transactional outbox emitting HMAC-signed webhooks (`learner.enrolled`, `grade.locked`, `payment.posted`, `incident.reported`). Sanctum serves the first-party Inertia SPA and Passport serves machine clients, with token scopes intersected with the service account's role ([RFC 9457](https://www.rfc-editor.org/rfc/rfc9457); [Standard Webhooks](https://www.standardwebhooks.com/)).

### School calendar: terms are configured per year, not assumed

SY 2025–26 ran 16 June 2025 to 31 March 2026 with 197 class days under DO 12 s.2025 ([Manila Bulletin](https://mb.com.ph/2025/4/18/deped-class-opening-sy-2025-2026-june-16)) [N]. SY 2026–27 runs 8 June 2026 to 8 April 2027 with **201 class days in three terms** under DO 009 s.2026 ([GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/)) [N]. Each term has an opening block, an instruction period and end-of-term activities. Term 1 instruction runs 15 June–1 September with end-of-term activities 2–15 September. Term 2 instruction runs 16 September–4 December with activities 7–18 December. Term 3 instruction runs 4 January–23 March 2027, followed by final assessments and closing activities 24 March–8 April. Private schools "may also adopt" the three-term calendar if they meet the required class days ([GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/)) [N]. In the LIS they must set their own school calendar before creating classes ([LIS Support](https://support.lis.deped.gov.ph/support/)) [P]. The LIS still keeps SHS semester facilities (SHS BOSY, second-semester enrollment), so how SSHS subjects map onto three terms is unresolved.

| ID | Requirement / business rule | Basis |
|---|---|---|
| CAL-01 | `SchoolYear` with a configurable list of `GradingPeriod`s per program family (JHS, SHS): N = 4 quarters, 2 semesters × 2 quarters, or 3 terms. Each period has sub-blocks (opening, instruction, end-of-term), and periods can differ between JHS and SHS in the same year | DO 009 s.2026 [N]; [I] |
| CAL-02 | Calendar events: holidays, INSET, breaks, class suspensions (typhoon/heat, with scope and source advisory), make-up days. The computed class-day count per period and per year is compared with the configured DepEd minimum (seed: 201 for SY 2026–27) | [N]; [I] |
| CAL-03 | (Pvt) Own opening/closing dates and period structure (semestral or three-term), with a compliance check against the minimum class days | [N]; [I] |
| CAL-04 | Grading, SF9 reporting, attendance summaries, subsidy billing and LIS windows all key off configured periods and dates, never off month names | [I] |
| CAL-05 | `LISWindow` per SY: Early Registration, Quick Count, BOSY K–10, SHS BOSY, SHS second semester, EOSY updating, transfer window (1st Friday to end of Q3/term equivalent). Dates are editable because DepEd extends them repeatedly | [LIS Support](https://support.lis.deped.gov.ph/support/) [P] |
| CAL-06 | `ProgramCalendarDeadline`s for DepEd/PEAC external dates (e.g., SHS VP redemption 3 Aug–3 Nov 2026; ESC/VP billing creation 1 Aug–7 Oct 2026), seeded from the yearly memo | [SDO Muntinlupa NUM-2026-223](https://deped-muntinlupa.com/wp-content/uploads/2026/05/NUM-2026-223.pdf) [D] |

### Curriculum: MATATAG and two SHS models coexist through SY 2026–27

MATATAG JHS has eight learning areas: Filipino, English, Mathematics, Science, Araling Panlipunan, Values Education (GMRC), MAPEH and TLE. The base allotment is **45 minutes × 5 days each**, plus a reading/math program slot and **Homeroom Guidance at 45 minutes once a week** ([DepEd MATATAG FAQ](https://deped.gov.ph/wp-content/uploads/FAQs-ON-THE-MATATAG-CURRICULUM.pdf) [P]; [SDO Muntinlupa NUM-2026-190](https://deped-muntinlupa.com/wp-content/uploads/2026/05/NUM-2026-190.pdf) [D]). The September 2024 amendment allows uniform 50/55/60-minute slots or other combinations, provided contact time is at least 5 h 30 min a day. Weekly minimums are **225 minutes for English, Mathematics, Science and GMRC/VE** and **200 minutes for Filipino, AP, MAPEH and TLE** ([Manila Bulletin](https://mb.com.ph/2024/9/19/flexible-matatag-curriculum-guidelines-set-for-implementation-in-q2-of-sy-2024-2025-dep-ed)) [N]. Special Program in Technical-Vocational Education schools keep their existing curriculum unless directed otherwise ([NUM-2026-190](https://deped-muntinlupa.com/wp-content/uploads/2026/05/NUM-2026-190.pdf)) [D].

The Strengthened SHS curriculum has two tracks, **Academic and Technical-Professional (TechPro)**, and schools need not offer both ([Manila Bulletin](https://mb.com.ph/2025/06/07/depeds-2025-revised-senior-high-school-curriculum-what-has-changed-and-why)) [N]. There are five core subjects of **160 hours each** in Grade 11: Effective Communication/Mabisang Komunikasyon, Life and Career Skills, General Mathematics, General Science, and Pag-aaral ng Kasaysayan at Lipunang Pilipino. Academic electives run 80 hours per semester and TechPro electives 320 hours per year ([SchoolFinderPH](https://www.schoolfinderph.com/blog/strengthened-shs-curriculum) [S]; [Manila Bulletin](https://mb.com.ph/2025/06/07/depeds-2025-revised-senior-high-school-curriculum-what-has-changed-and-why) [N]). Academic elective clusters are Arts, Social Sciences & Humanities; Business & Entrepreneurship; STEM; Sports, Health & Wellness; and Field Experience [S]. In Quick Count, SSHS Academic reports under GAS and TechPro under TVL ([LIS Support](https://support.lis.deped.gov.ph/support/)) [P]. The legacy SHS model (Core/Applied/Specialized subjects; Academic strands ABM, HUMSS, STEM and GAS; TVL, Sports, Arts & Design) [K] stays live for Grade 12 in SY 2026–27 and is permanent for historical records.

| ID | Requirement / business rule | Basis |
|---|---|---|
| CUR-01 | `CurriculumFramework` (MATATAG K–10; K to 12 legacy JHS; K to 12 legacy SHS; Strengthened SHS) with versions and a per-grade-level "framework start SY" setting. The G10 MATATAG year is configurable because sources conflict (SY 2026–27 vs 2027–28) | [PNA](https://www.pna.gov.ph/articles/1207588) [N]; [DepEdClub](https://depedclub.com/policy-guidelines-on-the-implementation-of-the-matatag-curriculum-d-o-no-010-s-2024/) [S] |
| CUR-02 | `Subject` (versioned) with learning area, key stage, grade level(s), hours, `grading_category` (DO 15 groups: JHS core areas; EPP/TLE+MAPEH; SHS Core; Other Academic Electives; Field Exposure; Arts Apprenticeship; Creative Production & Innovation; Arts/Sports/Health & Wellness Electives; Research Electives; Design & Innovation; TechPro Electives; Work Immersion) and the legacy `core/applied/specialized` type | [DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/) [S]; [K] |
| CUR-03 | Multi-component learning areas (MAPEH; Mabisang Komunikasyon) are modelled as a parent subject with weighted or averaged components | [S] |
| CUR-04 | SHS program structure: SSHS track → elective cluster → electives; legacy track → strand → subjects. Both are stored with LIS reporting codes (GAS/TVL mapping for Quick Count) | [LIS PPS Advisory](https://support.lis.deped.gov.ph/support/Manuals/ADVISORY-SHS-Pilot.pdf) [P] |
| CUR-05 | Curriculum version binds to the learner's section enrollment per SY (pilot G12 and retained learners) | [I] |
| CUR-06 | Time-allotment model (minutes × sessions/week) validated against configurable weekly minimums (seed 225/200), daily contact-time minimum (seed 330 min) and Homeroom Guidance ≥ 45 min/week | [N]; [I] |
| CUR-07 | Prerequisite links for SHS subjects (legacy rule: a failed prerequisite must be passed before the dependent subject) | DO 8 s.2015 [K] |
| CUR-08 | Subject hours drive the SHS general-average weighting once DepEd issues its "equivalent units" rule. Until then, the weighting method is a pending policy | [S] |

### Enrollment: DO 017 s.2025 makes the LIS official and SMIS the worksheet

DO 017 s.2025 repealed DO 3 s.2018 and governs SY 2025–26 onward for public schools, private schools and ALS centers. Private schools "may impose other admission conditions" ([DO 017 reproduction](https://eduknasyon.blogspot.com/2025/06/deped-order-017-s-2025-revised-basic.html); [LIS PPS Advisory](https://support.lis.deped.gov.ph/support/Manuals/ADVISORY-SHS-Pilot.pdf)) [D]/[P]. Early registration covers incoming Grades 7 and 11 and transferees into public schools. It runs from the last Saturday of January to the last Friday of February, and continuing learners in Grades 8–10 and 12 count as pre-registered. Documents are shown for verification, not collected [D]. In-person enrollment is preferred. For minors the parent or guardian completes the **Basic Education Enrollment Form (BEEF)**. Continuing learners with LRNs submit only a **Confirmation Slip**. Remote submission by official email, messaging or dropbox is allowed, after which advisers encode in the LIS BOSY facility [D]. The **PSA birth certificate is submitted once in K–12**, and listed secondary documents are accepted until **31 October** ([GMA](https://www.gmanetwork.com/news/topstories/nation/949408/deped-submit-once-child-birth-certificate-entire-k-12/story)) [N]. **Grade 7, 8–10, 11 and 12 entrants need the prior grade's SF9**, or a PEPT/A&E certificate of rating. Balik-Aral learners (back after at least a year out) qualify with PEPT/A&E or prior SF9/SF10. Late enrollees are accepted if they can still meet 80% of school days [D]. **No fee may be collected as a condition of early registration or enrollment**, and forms are not for sale [D].

The **LRN is a permanent 12-digit number** ([Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf)) [P]. It is created in the LIS only after the Division Planning Officer confirms that no record exists [D]. One slide deck reads the first six digits as the issuing School ID and the next two as the year, but no official digit specification was found ([SlideShare](https://pt.slideshare.net/jaredram55/learner-information-system)) [S]. In the LIS, a transfer is a request from the receiving school that the originating school confirms. **If it is still unconfirmed at EOSY, the learner is tagged a dropout at the originating school** ([LIS Support, previous updates](https://support.lis.deped.gov.ph/support/previous-updates.html)) [P]. "Temporarily enrolled" means a learner not officially enrolled because documents are missing. A private school notified through LIS has **30 calendar days** to confirm a transfer of a learner with unsettled accounts, after which the learner is tagged temporarily enrolled on an affidavit of undertaking [D].

| ID | Requirement / business rule | Basis |
|---|---|---|
| ENR-01 | Enrollment state machine per learner per SY: `prospect` → `early_registered` / `pre_registered` (continuing) → `enrolled` or `temporarily_enrolled` → in-year statuses mirroring LIS (`transferred_in`, `transferred_out`, `dropped`/NLPA with reason, `completed`, `promoted`, `retained`, `irregular`) | DO 017 [D]; [LIS](https://support.lis.deped.gov.ph/support/) [P]; [I] |
| ENR-02 | Early registration capture (online form, walk-in, dropbox) for incoming G7, G11 and transferees within the configured window. It states that registration "does not guarantee official enrollment". (Pub) A daily encode worksheet for the school-head LIS account | DO 017 Sec. V [D]; [LIS](https://support.lis.deped.gov.ph/support/previous-updates.html) [P] |
| ENR-03 | Versioned BEEF and Confirmation Slip forms (field set as configurable schema, because DepEd revises them by memo). One-click re-enrollment confirmation for continuing learners in the guardian portal | DO 017 Sec. VIII [D]; [I] |
| ENR-04 | Eligibility checks by entry grade (prior SF9, PEPT/A&E certificate, ALS PPA certificate, Balik-Aral path, international/foreign records needing apostille or PEPT). Late-enrollment check against 80% of remaining school days, with a school-head discretionary override that records catch-up interventions | DO 017 Sec. VI [D] |
| ENR-05 | Document checklist per learner with due dates: PSA birth certificate (once in K–12; secondary document accepted until 31 Oct), SF9, special-case documents. A missing item past its due date keeps the learner `temporarily_enrolled` and raises a task | DO 017 Sec. VII [D]; [I] |
| ENR-06 | LRN stored as a 12-char digit string with format validation. SMIS never generates LRNs. New learners carry "LRN pending LIS creation" until the LIS assigns one. Duplicate-candidate detection (name + birth date + sex + mother's name) before LIS encoding | [Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf) [P]; [TeacherPH LIS FAQ](https://www.teacherph.com/deped-lis-data-issues-and-frequently-asked-questions/) [S]; [I] |
| ENR-07 | Pre-LIS data validation: names exactly as on the birth certificate, date of birth, sex, address with ZIP, citizenship, IP ethnicity, disability classification, 4Ps Household ID (≥ 12 chars), modality. LIS corrections are slow and are counted against the encoding account | [LIS Support](https://support.lis.deped.gov.ph/support/) [P]; [TeacherPH](https://www.teacherph.com/deped-lis-data-issues-and-frequently-asked-questions/) [S] |
| ENR-08 | Quick Count tally: daily enrollment by grade level and sex in the LIS Quick Count window, plus a variance report against the previous SY (divisions demand justifications below 100%) | [LIS](https://support.lis.deped.gov.ph/support/) [P]; [SDO Muntinlupa](https://deped-muntinlupa.com/wp-content/uploads/2026/07/UN-2026-264.pdf) [D] |
| ENR-09 | LIS tagging worksheets: ADM, BMI, SBFP, ESC and SHS voucher IDs (Pvt), CCT/4Ps, LWD, IP, SSHS electives, ARAL, Grade 12 SHS exit choices, honors (G7–10) | [LIS Support](https://support.lis.deped.gov.ph/support/) [P] |
| ENR-10 | Transfer tracking: incoming requests created on enrollment; outgoing requests answered within the configured SLA; an alert before EOSY for any unconfirmed transfer, because it becomes a dropout tag | [LIS](https://support.lis.deped.gov.ph/support/previous-updates.html) [P] |
| ENR-11 | Transferee-with-arrears path: (Pub) accept, capture the Affidavit of Undertaking, start a 30-day timer from LIS notice, then tag `temporarily_enrolled`. (Pvt as originating school) respond within 30 days; a finance hold may withhold credentials but never the LIS response | DO 017 Sec. IX [D]; DM 023 s.2026 [D] |
| ENR-12 | (Pub) Hard block: no fee, contribution or purchase can be a prerequisite of early registration or enrollment | DO 017 Sec. VI.C [D] |
| ENR-13 | (Pvt) Admission conditions: entrance test scheduling and results, interview, reservation fee, enrollment contract acceptance (including any interest clause, see FEE-07) | DO 017 Sec. II [D]; [I] |
| ENR-14 | Learner-group fields treated as sensitive: IP group (RA 8371 definition), mother tongue, religion, disability (PWD ID optional), 4Ps, chronic illness; collected only with a stated purpose | DO 017 Sec. IV, X [D] |
| ENR-15 | ALS-to-formal entry (temporary enrollment facility for G7/G11 from ALS) and A&E passers' path into Grade 11 and SHS voucher screening | [LIS](https://support.lis.deped.gov.ph/support/) [P]; DM 031 s.2026 [D] |
| ENR-16 | Retention: BEEF and confirmation-slip images are destroyed one year after collection, with a disposal log | DO 017 Sec. X [D] |

### Learner records and credentials: withhold-but-accommodate replaces the old myth of a blanket ban

Records move **school to school only**. "Learners and parents may not be compelled to carry records." Records transfer before the end of the first grading period, and mid-year transfers are secured within 30 days of first attendance. Scanned SF9/SF10 sent by official email through LIS tracking is allowed for Grade 6→7 and Grade 10→11, and receiving schools "cannot require physical copies" ([DO 017 Sec. IX.B](https://eduknasyon.blogspot.com/2025/06/deped-order-017-s-2025-revised-basic.html)) [D]. The originating school must send the documents "as soon as a request is made, or at least respond" ([LIS Support](https://support.lis.deped.gov.ph/support/previous-updates.html)) [P].

**DepEd Memorandum 023 s.2026 (27 Mar 2026)** settles the private-school question ([full text via SDO Muntinlupa](https://deped-muntinlupa.com/wp-content/uploads/2026/03/NUM-2026-135.pdf)) [D]. Under DO 88 s.2010, private schools "maintain the legal right to withhold official transfer credentials until all such debts are fully settled". The receiving school tags the transferee Temporarily Enrolled on an Affidavit of Undertaking, "a binding guarantee of future payment". Until the original credentials arrive, the learner "cannot be officially promoted to a higher grade level nor officially graduate in the Department's systems", and receiving schools are "strictly prohibited from issuing official permanent records or final progress reports". Yet "no learner shall be denied participation in EOSY rites on the basis of unsettled financial or property obligations", and credentials must be released "immediately once all obligations are satisfied". Commentary ties the withholding right to DO 88 Sec. 128, while another source cites Secs. 139–141. The numbers conflict and are unverified ([FOI reply](https://foi.gov.ph/requests/lrn-and-form-137); [Respicio](https://www.respicio.ph/commentaries/can-a-private-school-withhold-report-cards-for-unpaid-tuition)) [S]. Only SHS completers receive diplomas and graduation rites. Grade 10 completers receive a certificate at a moving-up ceremony ([GMA](https://www.gmanetwork.com/news/news/nation/686621/deped-limits-diplomas-graduation-rites-to-grade-12-finishers/story/)) [N]. DM 015 s.2026 bars collecting contributions for rites and making proms or field trips completion requirements ([BusinessWorld](https://www.bworldonline.com/education/2026/03/24/738248/deped-field-trip-prom-not-required-for-graduation/)) [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| REC-01 | Learner master keyed by Person + LRN, with effective-dated name/address/guardian history. Corrections to name, birth date or sex follow the LIS Learner Profile route, and SF10 must match SF1 | [SlideShare](https://www.slideshare.net/slideshow/preparation-and-checking-of-school-forms-sy2022-2023-as-of-june-22-2023-1-1-pptx/270583191) [S] |
| REC-02 | Records-request queue (inbound and outbound) linked to LIS transfer requests, with SLA timers (end of first grading period; 30 days after first attendance for mid-year), dispatch method (authorized courier, official-email scan for G7/G11), and decline reasons | DO 017 [D]; LIS [P] |
| REC-03 | Release can only go to a school or authorized personnel; release to a parent or learner as carrier is blocked, except the learner's own SF9 copy | DO 017 [D] |
| REC-04 | SF10 single-original model: the originating school sends the original and keeps a certified true copy. Every CTC is logged with serial, seal and school-head signatory. Erasures need school-head ink validation (captured as a correction record) | DO 58 s.2017 [S] |
| REC-05 | Temporarily-enrolled guard: blocks final SF9, SF10, the Grade 10 certificate, the SHS diploma and system promotion/graduation until the original credentials are received. Rites eligibility stays allowed | DM 023 s.2026 [D] |
| REC-06 | (Pvt) Financial credential hold: blocks release of the original SF10, SF9 and certificate of eligibility to transfer, diploma and certificates. It never blocks exams (RA 11984), class participation, EOSY rites or the LIS transfer response. Release is automatic within one business day of settlement or an approved settlement plan. Override requires principal + finance approval with a reason | DM 023 [D]; [RA 11984](https://lawphil.net/statutes/repacts/ra2024/ra_11984_2024.html) [P]; [I] |
| REC-07 | Holds cannot be justified by voluntary contributions, PTA dues or property such as books unless school policy and law allow, and in public mode never | [Respicio](https://www.respicio.ph/commentaries/can-a-school-withhold-student-records-over-unpaid-contributions) [S]; DO 41 [N] |
| REC-08 | Certificate templates (versioned, serialized, logged): Certificate of Enrollment, Good Moral Character, Grade 10 Certificate of Completion, SHS Diploma, Form 137 request letter, certificate of eligibility to transfer (Pvt). No national format was found for school-issued certificates | [I]; gap noted |
| REC-09 | External assessment records keyed by LRN (NAT G10/G12, ALS A&E, PEPT) with type, SY, scores/proficiency and passed flag. They never feed the GA or promotion | [Curriculum notes / OECD](https://www.oecd.org/en/publications/developing-a-national-student-assessment-framework-for-the-philippines_786bff30-en/full-report/component-5.html) [P]; [I] |
| REC-10 | Permanent-record retention: SF10 and attached birth-certificate copy are permanent. No auto-deletion of academic records. Disposal of other classes follows a configurable retention schedule (National Archives schedules not yet retrieved) | DO 017 Sec. XI [D]; [I] |

### School Forms: reconcile with the LIS and own SF9 and SF10

DO 4 s.2014 adopted SF1–SF7. DO 58 s.2017 added SF8, SF9 and SF10 plus SHS-specific SF5A/SF5B ([Annex A](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf) [P]; [DO 58 reproduction](https://eduknasyon.blogspot.com/2018/11/deped-order-no-58-s-2017-adoption-of.html) [S]). The LIS generates SF1, SF4, SF5 and SF6. These cannot be edited outside the system, and only SF1, SF4, SF5, SF6 and SF10 are subject to division checking ([SlideShare](https://www.slideshare.net/slideshow/preparation-and-checking-of-school-forms-sy2022-2023-as-of-june-22-2023-1-1-pptx/270583191)) [S]. **SF9 and SF10 are still school-prepared** from official templates. DepEd issued an SSHS SF10 and E-Class Record in March 2026 and corrected files five days later ([LIS Support](https://support.lis.deped.gov.ph/support/); [DM 020 s.2026 title](https://www.deped.gov.ph/2026/03/13/march-13-2026-dm-020-s-2026-modified-electronic-class-record-and-school-form-10-for-strengthened-senior-high-school-pilot-implementers-in-school-year-2025-2026/)) [P]. DO 58 says no other forms are official unless approved. One deck calls forms from unauthorized "solutions" null and void, which is stronger wording than the order excerpt [S]. SMIS output must therefore replicate official layouts exactly and present itself as a preparation tool, not as an alternative form.

| Form | Content (per Annex B and DO 58) | SMIS role | ID |
|---|---|---|---|
| SF1 School Register | School ID, SY, section; LRN, name per birth certificate, sex, birth date, birthplace, age by 1st Friday of June, mother tongue, IP group, religion, address, parents/guardian, contact, remarks | Generate for reconciliation; LIS version is official | SF-01 |
| SF2 Daily Attendance | Daily marks, absences, tardies, enrollment as of 1st Friday of June, late enrollment, ADA, % attendance, learners with 5 consecutive absences, dropouts, transfers in/out (M/F/T). Updated daily, submitted by the 5th of the next month | Primary output from ATT | SF-02 |
| SF3 Books Issued and Returned | Title/subject, dates; loss codes FM/TDO/NEG; action codes LLTR/TLTR/PTL | Textbook module enums | SF-03 |
| SF4 Monthly Movement and Attendance | Lifted from SF2; by the 10th of the next month | Generate, reconcile | SF-04 |
| SF5 / SF5A / SF5B Promotion and Proficiency | EOSY promotion status and proficiency per learner (SHS variants) | Generate from PRM; reconcile | SF-05 |
| SF6 Summarized Promotion | Summary of SF5; SHS version signed by school head and division representative | Generate, reconcile | SF-06 |
| SF7 Personnel Assignment List | Personnel, assignments, basic profile (fields unverified) | Generate from personnel/loading | SF-07 |
| SF8 Health and Nutrition | Height/weight at start of SY → BMI and weight status; adviser, MAPEH teacher or nurse | Restricted health data | SF-08 |
| SF9 Learner Progress Report Card | Grades per period, attendance; core-values section under DO 8 (DO 15 layout unconfirmed) | Core output; versioned templates | SF-09 |
| SF10 Permanent Academic Record | JHS (started by G7 adviser) and SHS versions; SSHS 2026 template | Core output; single original + CTC log | SF-10 |

Sources: [Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf) [P]; [DO 58 reproduction](https://eduknasyon.blogspot.com/2018/11/deped-order-no-58-s-2017-adoption-of.html) [S].

| ID | Requirement / business rule | Basis |
|---|---|---|
| SF-11 | Each form is a versioned template bound to its issuing memo (e.g., "SF1 updated 28 Sep 2022", "SSHS SF10 v2026_corrected"). Old versions remain renderable for historical years | [LIS Support](https://support.lis.deped.gov.ph/support/) [P] |
| SF-12 | Reconciliation reports: SF1 vs SF2 vs SF4 per section (leavers, transfers, end-of-year counts), SMIS vs LIS-exported SF1/SF5 differences flagged before EOSY | [TeacherPH](https://www.teacherph.com/guidelines-checking-school-forms/) [S]; [I] |
| SF-13 | SF9 and SF10 sign-off workflow: adviser prepares and signs, school head certifies (dry seal captured as an attestation event) | DO 58 [S] |
| SF-14 | The SSHS FAQ case where a "Final Average Grade" shows "Passed" despite a failing subject is a test fixture: subject-level failures must always surface on SF9/SF10 | [LIS Support](https://support.lis.deped.gov.ph/support/) [P] |
| SF-15 | Clerical form preparation is routed to designated non-teaching roles where staffing allows, consistent with DO 2 s.2024's removal of administrative tasks from teachers | [DO 2 s.2024 PDF](https://www.deped.gov.ph/wp-content/uploads/DO_s2024_002.pdf) [P] |

### Class programs and sectioning: validate minutes, sizes and rooms live

DM 048 s.2025 sets an SHS class-size target of **40 learners, or 25 for laboratory and workshop electives**, and allows larger classes with quality safeguards where schools cannot comply ([SlideShare deck of DM 048](https://www.slideshare.net/slideshow/deped_memo_048_2025_strenthening-senior-high-school-final-pptx/282577759)) [S]. No current binding JHS class-size standard was found. A 2018 planning parameter of 1:40 is the best available default ([PNA](https://www.pna.gov.ph/articles/1029281)) [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| CLS-01 | `Section` per SY: grade level, program/track/cluster (SHS), curriculum version, adviser, home room, capacity (seed 40; 25 for SHS lab/workshop electives), with an over-capacity override carrying a reason and safeguard note | DM 048 [S]; [I] |
| CLS-02 | Class program builder: periods per day with DO 12 s.2024 Option A (45-min) or Option B (uniform 50/55/60-min) templates; live validation of weekly minutes per learning area, Homeroom Guidance and daily contact time; room, teacher and section clash detection | [Inquirer](https://newsinfo.inquirer.net/1984864/deped-issues-new-guidelines-for-matatag-curriculum-implementation) [N]; [I] |
| CLS-03 | SHS elective sections cut across homerooms (learners grouped by elective, possibly per term), including Work Immersion and field-exposure blocks off campus | [I] |
| CLS-04 | Sectioning assistant: bulk placement by grade, elective choice, sex balance and optional criteria (homogeneous/heterogeneous is school policy), with manual drag-free alternatives (WCAG 2.5.7) | [I] |
| CLS-05 | Section changes mid-year are effective-dated movements that carry attendance and partial grades along | [I] |
| CLS-06 | Room and facility inventory feeds the BEIS school-profile export (rooms, seats, laboratories) | [I] |

### Teacher loading: DO 5 s.2024 limits for public schools, policy tables for private

DO 5 s.2024 sets **6 hours of actual classroom teaching plus 2 hours of ancillary tasks** for public school teachers, with overload pay and compensation for ancillary and teaching-related assignments. It operationalizes RA 4670 and follows DO 2 s.2024's removal of administrative tasks ([PNA](https://alpha.pna.gov.ph/articles/1223752); [GMA](https://gmanetwork.com/news/topstories/nation/905258/deped-overload-pay-public-school-teachers/story)) [N]. RA 4670 Sec. 13 caps actual teaching at 6 hours a day and pays an extra 25% of basic pay for teaching up to 8 hours ([LawPhil](https://lawphil.net/statutes/repacts/ra1966/ra_4670_1966.html)) [K]. Private schools are not bound by RA 4670, so their limits come from school policy or a collective bargaining agreement [I].

| ID | Requirement / business rule | Basis |
|---|---|---|
| TLD-01 | Teaching assignment = teacher × section × subject × weekly minutes, derived from the class program; advisership and Homeroom Guidance counted per policy | [I] |
| TLD-02 | `LoadPolicy` per SY and mode. (Pub) Seed: ≤ 360 min/day actual teaching, ≤ 480 min/day total, minutes above 360 flagged as overload. (Pvt) Limits defined by the school | DO 5 s.2024 [N]; RA 4670 [K] |
| TLD-03 | Ancillary and teaching-related designations (e.g., grade coordinator, club adviser, LIS focal) with time credits and compensation type (service credit or pay; formula not yet verified) | DO 5 [N]; [I] |
| TLD-04 | Overload ledger per teacher per period, approved by the principal, exportable for payroll | [I] |
| TLD-05 | Qualification check warnings: subject specialization vs assignment; PRC licence validity; registered guidance counselor licence for counselors | RA 9258 [N]; [I] |

### Attendance: SF2 is the daily source, and the 20% rule drives credit

Daily attendance on SF2 feeds SF4, the 5-consecutive-absence column and dropout risk ([Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf)) [P]. The instruction that a home visit is *required* after 5 consecutive absences appears only on an unofficial template ([Scribd SF2](https://www.scribd.com/document/677015938/SF2)) [S]. Under DO 15 s.2026, **absences above 20% of prescribed class days mean a failing grade or no credit unless justified**, and the school head may grant documented exemptions ([DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/)) [S]. DO 006 s.2026 bans portable devices during instructional hours, with academic and emergency exceptions ([eduknasyon](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)) [S].

| ID | Requirement / business rule | Basis |
|---|---|---|
| ATT-01 | Daily marks per learner per section (present, absent, tardy, excused, with reason), plus optional per-subject marks for SHS elective sections | [P]; [I] |
| ATT-02 | Monthly SF2 per section and SF4 roll-up generated automatically, with submission reminders (5th and 10th of the following month) | [Annex B](https://rtei.okfn.org/documents/List_of_Modified_School_Forms.pdf) [P] |
| ATT-03 | At-risk rules (configurable): N consecutive absences (seed 5) → home-visit task for the adviser and guidance notification; cumulative absence approaching the threshold (seed 20%) → warning to adviser and guardian | [P]; [S]; [I] |
| ATT-04 | Absence-percentage computation per learner (and per subject where applicable) against configured class days, with an `AttendanceExemption` record (school-head approval, documents) that suspends the no-credit consequence | DO 15 [S] |
| ATT-05 | Attendance summaries per month (legacy SF9) and per term (DO 15 report) from the same data | DO 8 [K]; DO 15 [S] |
| ATT-06 | Class-suspension days are excluded from class-day counts automatically | [I] |
| ATT-07 | Dropout/NLPA tagging requires a reason from the LIS reason list (updated EOSY 2024–25) | [LIS Support](https://support.lis.deped.gov.ph/support/) [P] |

### Grading engine: one pipeline, three seeded schemes, no constants

Both orders share the pipeline: raw scores → percentage score (PS = RS/HPS × 100) → weighted score (WS = PS × weight) → initial grade (IG = ΣWS) → transmuted grade where a table applies ([DepEdClub, Annex D](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/)) [S]. DO 15 renames the components to Written/Oral Works (WW), Product/Performance Tasks (PT) and Examinations (EX). **Formative assessment no longer counts toward grades**, and the order recommends caps on WW, PT and EX per term, though the cap values were not found ([Philstar](https://www.philstar.com/headlines/2026/06/22/2537040/deped-starts-phaseout-grade-transmutation-policy)) [N]. EX combines Summative Test 1 (30%), Summative Test 2 (30%) and the Term Examination (40%) before the EX weight applies. Values Education splits WW into cognitive 10% + affective 10% and PT into cognitive 10% + affective 10% + behavioral 30% [S]. Term grades, final grades (average of term grades) and the general average (average of final grades) are rounded to whole numbers. FG ≥ 75 meets the standard. Multi-component areas pass if the averaged FG ≥ 75 even when one component fails [S]. The SHS general average will use "equivalent units", reserved for a separate issuance [S]. AI may not determine final grades, term exams are closed to AI, and teachers may not enter learner personal data into AI platforms [N]. Raw scores, rubrics and tools are kept at least one school year [S].

**DO 15 seed weights (secondary, verify each cell)**

| Key stage / subject group | WW | PT | EX |
|---|---|---|---|
| JHS: English, Filipino, Math, Science, AP, GMRC/VE | 20 | 50 | 30 |
| JHS: EPP/TLE, MAPEH | 20 | 60 | 20 |
| SHS: Core; Other Academic Electives | 20 | 50 | 30 |
| SHS: Field Exposure; Arts Apprenticeship; Creative Production & Innovation | 15 | 70 | 15 (term exam only) |
| SHS: Arts, Sports, Health & Wellness Electives | 20 | 60 | 20 |
| SHS: Research Electives; Design & Innovation | 40 | 60 | — |
| SHS: TechPro Electives | 15 | 65 | 20 |
| SHS: Work Immersion | 20 | 80 | — |

Source: [DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/) [S]; JHS rows corroborated by [TeachPinas](https://www.teachpinas.com/e-class-record-deped-ecr-templates/) [S]. One vendor blog claims 25/50/25 ([deped.me](https://deped.me/blog/sf9-sf10-automation-class-record-deped-2026)) [S], which shows why the weights must be data.

**DO 8 s.2015 legacy seed weights [K]** ([DO 8 PDF](https://www.deped.gov.ph/wp-content/uploads/2015/04/DO_s2015_08.pdf), not re-fetched). Components are WW/PT/Quarterly Assessment. JHS: Languages, AP and EsP 30/50/20; Science and Math 40/40/20; MAPEH and TLE 20/60/20. SHS: Core 25/50/25; Academic other subjects 25/45/30; Academic Work Immersion/Research/Business Simulation/Exhibit/Performance 35/40/25; TVL/Sports/Arts & Design all subjects 20/60/20. Legacy transmutation maps IG 100 → 100 and 60.00–61.59 → 75 in steps of 1.6, then below 60 in steps of 4 down to 0–3.99 → 60. Legacy descriptors are Outstanding (90–100), Very Satisfactory (85–89), Satisfactory (80–84), Fairly Satisfactory (75–79) and Did Not Meet Expectations (< 75).

**DO 15 adjusted transmutation table, SY 2026–27 only (secondary; anchor IG 70 → 75 corroborated by news).** IG ranges are inclusive and unrounded to 2 dp.

| IG | TG | IG | TG | IG | TG |
|---|---|---|---|---|---|
| 99.50–100.00 | 100 | 85.34–86.51 | 88 | 71.18–72.35 | 76 |
| 98.32–99.49 | 99 | 84.16–85.33 | 87 | 70.00–71.17 | 75 |
| 97.14–98.31 | 98 | 82.98–84.15 | 86 | 65.34–69.99 | 74 |
| 95.96–97.13 | 97 | 81.80–82.97 | 85 | 60.67–65.33 | 73 |
| 94.78–95.95 | 96 | 80.62–81.79 | 84 | 56.01–60.66 | 72 |
| 93.60–94.77 | 95 | 79.44–80.61 | 83 | 51.34–56.00 | 71 |
| 92.42–93.59 | 94 | 78.26–79.43 | 82 | 46.67–51.33 | 70 |
| 91.24–92.41 | 93 | 77.08–78.25 | 81 | 42.01–46.66 | 69 |
| 90.06–91.23 | 92 | 75.90–77.07 | 80 | 37.34–42.00 | 68 |
| 88.88–90.05 | 91 | 74.72–75.89 | 79 | 32.68–37.33 | 67 |
| 87.70–88.87 | 90 | 73.54–74.71 | 78 | 28.01–32.67 | 66 |
| 86.52–87.69 | 89 | 72.36–73.53 | 77 | 23.35–28.00 | 65 |
| | | | | 18.68–23.34 | 64 |
| | | | | 14.01–18.67 | 63 |
| | | | | 9.35–14.00 | 62 |
| | | | | 4.68–9.34 | 61 |
| | | | | 0.00–4.67 | 60 |

Sources: [DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/) [S]; anchor [Philstar](https://www.philstar.com/headlines/2026/06/22/2537040/deped-starts-phaseout-grade-transmutation-policy), [GMA](https://www.gmanetwork.com/news/topstories/nation/992328/deped-phase-out-grade-transmutation-schools/story/) [N]. DO 15 descriptors are Advancing 90–100, Benchmarking 80–89, Connecting 75–79, Developing 65–74 and Emerging 0–64 [S].

| ID | Requirement / business rule | Basis |
|---|---|---|
| GRD-01 | `GradingScheme` (versioned, effective SY, scope) composed of: period structure; components with optional sub-components and their internal weights; a weight matrix keyed by (key stage/grade, grading category); a nullable `TransmutationTable` (IG range → TG); floor (seed 60); passing mark (seed 75); rounding points and method (IG unrounded ≥ 2 dp; TG/FG/GA rounded, half-up by default, configurable); descriptor band set; and a source citation with verification status | [S]; [K]; project constraint |
| GRD-02 | Seeds shipped as data: `DO8-2015-legacy`, `DO15-2026-transition` (adjusted table), `DO15-2027-zero-based` (no table), and the hybrid `DO8-weights+DO15-transition-table` for SY 2026–27 legacy Grade 12. Seeds ship with status `secondary`/`prior_knowledge` until verified | [S]; [K] |
| GRD-03 | Scheme selection per learner-section-subject from the curriculum version and SY, never from grade level alone | [I] |
| GRD-04 | A component with no weight (e.g., Research Electives EX) is excluded, not scored as zero. The weights of applicable components must sum to 100% (validation at scheme approval) | [I] |
| GRD-05 | Class record (ECR) per section-subject: assessment items with HPS, component, sub-component, period, date, and a "formative" flag that excludes the item from computation. Optional warnings when items exceed configured per-term caps | DO 15 [N]/[S] |
| GRD-06 | Multi-component subjects: component grades → parent FG by configured method; pass rule on the averaged FG | [S] |
| GRD-07 | Grade lifecycle per section-subject-period: draft → submitted (teacher) → reviewed (adviser/coordinator) → locked (principal). Changes after locking go through a `GradeChangeRequest` with reason, evidence and a different approver; before/after values are logged | UMIS SoD pattern; [I] |
| GRD-08 | Every computed grade stores a snapshot of the scheme version and inputs, so it is reproducible after configuration changes | [I] |
| GRD-09 | Import from Google Classroom coursework or official Excel ECR files populates assessment items as proposed scores. The teacher confirms them in SMIS, which is always the grade of record | [I] |
| GRD-10 | AI guardrails: no AI-computed final grades; no learner PII sent to AI services; any AI feature requires a privacy impact assessment and disclosure | DO 15 [N]; DO 003 s.2026 via [DM 130](https://www.depedimuscity.com/portal/uploads/DM_130_S_2026.pdf) [D] |
| GRD-11 | Retention of raw scores, rubrics and item data for ≥ 1 SY after the period (configurable longer for appeals/audit) | [S] |
| GRD-12 | Incomplete/pending grades are a status (INC/pending) that blocks promotion until resolved. No DO 15 rule was found, so the deadline is policy | [I] |
| GRD-13 | Observed core values (Maka-Diyos, Makatao, Makakalikasan, Makabansa; AO/SO/RO/NO) as configurable master data. On for legacy schemes; status "pending verification" for DO 15 because the new report card is unconfirmed | DO 8 [K]; gap |
| GRD-14 | Transferee grade conversion between schemes is a recorded registrar action with a source-scheme reference. No DepEd rule was found | [I] |
| GRD-15 | Golden test suite per scheme: published worked examples and boundary cases (IG 69.99/70.00, 59.99/60.00, rounding of .5) run in CI | [I] |

### Promotion, remedial classes and retention: derive status from counted failures

Under DO 15 s.2026 (Grades 4–12), learners who pass all learning areas are promoted. Those who fail **at most two** go to Summer Remedial Class (SRC), and those who fail **more than two** are retained. The Recomputed Final Grade is RFG = (FG + Remedial Class Mark)/2, and RFG ≥ 75 passes ([DepEdClub](https://depedclub.com/deped-grading-system-guidelines-do-015-s-2026/)) [S]. Learners still failing one or two areas after remediation "may be conditionally promoted and take back subjects", but this is reported by only one summary and overlaps ambiguously with the SRC rule ([tchersden](https://www.tchersden.com/2026/06/deped-order-015-2026-assessment-grading-awards-guide.html)) [S]. DepEd says removing transmutation "should not be treated as an automatic trigger for higher retention" ([Philstar](https://www.philstar.com/headlines/2026/06/22/2537040/deped-starts-phaseout-grade-transmutation-policy)) [N]. Under DO 8, failing a remedial class allowed promotion with back subjects, capped at two [K].

| ID | Requirement / business rule | Basis |
|---|---|---|
| PRM-01 | `PromotionRuleSet` per SY and key stage: thresholds for promote / SRC / retain (seed DO 15: 0 / ≤ 2 / > 2 failed FGs), the RFG formula and pass mark, conditional promotion and back-subject cap (flagged unverified), and the absence-rule interaction | [S]; [K] |
| PRM-02 | Per learner per subject: FG, RCM (nullable), RFG, remedial status, back-subject flag. Promotion status is derived and recomputed, never typed in | [I] |
| PRM-03 | SRC management: remedial sections, enrollment, assessments computed like term grades into the RCM, and deadlines before the next SY's LIS BOSY window | [S]; [I] |
| PRM-04 | Promotion finalization blocked for Temporarily Enrolled learners (REC-05) and for INC grades | DM 023 [D]; [I] |
| PRM-05 | Completion: Grade 10 certificate and SHS diploma require all learning areas passed and credentials complete; Grade 12 SHS exit-choice tagging | DO 8 [K]; LIS [P] |
| PRM-06 | Learners with disabilities: accommodation notes and individualized plans recorded. No DO 15 provisions were found | gap; [I] |

### Awards: one Academic Excellence Award, listed alphabetically

DO 15 abolishes With Honors, With High Honors and With Highest Honors. The single **Academic Excellence Award** for Grades 4–12 requires **GA ≥ 90, no final grade below 80 and no derogatory or disciplinary record** in the SY. Awardees are **listed alphabetically, not ranked**, and a school may certify actual rank on formal written request ([SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-new-grading-system-2026); [tchersden](https://www.tchersden.com/2026/06/deped-order-015-2026-assessment-grading-awards-guide.html)) [S]. Excellence in Specific Learning Areas, Leadership Excellence and Special Recognition are named without criteria [S]. Legacy DO 36 s.2016 tiers were 90–94, 95–97 and 98–100 with no grade below 85, plus Conduct, Perfect Attendance and Grade 12 awards [K].

| ID | Requirement / business rule | Basis |
|---|---|---|
| AWD-01 | Rule-based `AwardDefinition`s: eligibility predicates (GA threshold, min FG, no-disciplinary flag from WEL, attendance %, period: year-end or term), GA rounding choice (rounded vs unrounded, unverified), and output ordering (default alphabetical) | [S]; [I] |
| AWD-02 | Seeds: DO 15 Academic Excellence Award (GA ≥ 90, min FG 80, no disciplinary case); DO 36 legacy tiers for SY ≤ 2025–26 records | [S]; [K] |
| AWD-03 | "No disciplinary record" reads only finalized WEL sanctions in the SY, not open allegations, and the evaluation is logged | [I] |
| AWD-04 | Rank-certification report generated only on a logged written request | [S] |
| AWD-05 | Publication of awardee names (website, social media) requires the learner's and guardian's publication consent (PRV-04) | DO 017 Sec. X [D] |
| AWD-06 | LIS honors tagging export (Grades 7–10) | [LIS](https://support.lis.deped.gov.ph/support/) [P] |

### Learner welfare and discipline: DO 006 s.2026 turns case handling into timed workflows

DO 40 s.2012 (Child Protection Policy) remains in force, with 2024 supplemental guidelines ([SDO Muntinlupa NUM-2025-408](https://deped-muntinlupa.com/wp-content/uploads/2025/08/NUM-2025-408.pdf)) [D]. **DO 006 s.2026 (ESMLE, 24 Mar 2026)** overlays it without repealing it, and binds public schools while private schools are "encouraged" to adopt it ([eduknasyon](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)) [S]. It requires a Learner Handbook distributed at enrollment and posted conspicuously or on the website, and a Code of Conduct with no corporal or humiliating punishment. It also requires a localized anti-bullying policy, monthly non-contact bag inspections, Confiscation Slips (Annex F), an Initial Risk Assessment (Annex H) by the Child Protection Committee, an Incident Report and Intake Sheet, a designated Learner Formation Officer, and a **centralized, access-restricted incident database** compliant with RA 10173 [S]. Its timelines are **48 hours** for referral to the Disciplining Authority, **10 calendar days** for the fact-finding report to the school head and **30 calendar days** for results to the SDS and RD. Due process means written notice, a 10-day written answer, a written decision and appeal (generally 15 days; bullying appeals to the legal affairs undersecretary within 10 days). An annual bullying report is due in the first week of the SY [S]. Offenses fall in three levels. The third level (weapons, bomb threats, hazing, sexual assault, drugs, exam cheating, sharing explicit videos) means non-readmission on the first offense and immediate referral to law enforcement and social welfare, and victims receive immediate psychosocial support ([Tribune](https://tribune.net.ph/2026/07/02/bomb-threats-deadly-weapons-now-top-school-offenses-under-deped-rules)) [N]. RA 10627 requires anti-bullying policies, reporting to the division and parent notification [K]. **RA 12080 (2024)**, with an IRR signed March 2025, creates School Counselor and School Counselor Associate posts and division Mental Health and Well-Being Offices ([LawPhil](https://lawphil.net/statutes/repacts/ra2024/ra_12080_2024.html); [IRR](https://deped.gov.ph/wp-content/uploads/IRR-of-RA-12080-Basic-Education-Mental-Health-and-Well-Being-Promotion-Act-v2.pdf)) [P]. RA 9258 reserves counseling to licensed guidance counselors [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| WEL-01 | Incident intake modelled on the DO 006 Incident Report and Intake Sheet: parties (complainant, respondent, witnesses; learners and personnel), type (bullying, abuse, violence, exploitation, discrimination, GBSH, device violation), setting (physical, online, off-campus), date/time, narrative, evidence | DO 006 [S] |
| WEL-02 | Case workflow with SLA timers seeded from DO 006: 48 h referral, 10-day fact-finding, 30-day report to SDS/RD, 10-day answer, decision, appeal windows (15 days; 10 days for bullying). Escalations go to the principal and CPC chair | DO 006 [S] |
| WEL-03 | Offense catalogue by level with the sanction ladder (reprimand, parent conference, suspension, non-readmission, exclusion), versioned because the full Annex I matrix was not obtained | [N]; [S] |
| WEL-04 | Mandatory referral checklist for third-level offenses (PNP, DSWD/LSWDO, SDO) and victim psychosocial-support tasks | [N] |
| WEL-05 | Initial Risk Assessment form, Confiscation Slips (serialized, with return/turnover record) and bag-inspection plan/log (no pat-downs) | DO 006 [S] |
| WEL-06 | CPC roster per SY (school head, guidance, teacher, parent, learner and community representatives) and Learner Formation Officer designation | DO 006 [S] |
| WEL-07 | Sanction outcomes feed enrollment status (exclusion removes the learner from class lists; non-readmission blocks next-SY enrollment), the awards disciplinary flag and, where applicable, ESC continuation checks (suspension > 2 weeks) | [I]; DO 11 s.2026 [S] |
| WEL-08 | Annual bullying report and per-case reports to the SDO generated from the database | DO 006 [S]; RA 10627 [K] |
| WEL-09 | Guidance records: counseling session notes visible only to licensed counselors (or supervised associates), referrals to the SDO MHWO, Homeroom Guidance records, consent for counseling of minors | RA 12080 [P]; RA 9258 [N]; [I] |
| WEL-10 | Health: SF8 anthropometrics (BMI, weight status), clinic visits, SBFP/deworming tags. Visible to nurse/clinic and, in summary, the adviser | DO 58 [S]; [I] |
| WEL-11 | Access to WEL data is restricted to case-assigned roles, enforced by row-level security, and every read is logged. Learner-facing portals never show respondent identities to other families | DO 006 [S]; RA 10173 [P] |
| WEL-12 | (Pvt) Adoption setting: the school records whether it adopts DO 006 in full or uses its own handbook timelines; DO 40 and RA 10627 apply regardless | DO 006 coverage [S] |

### Private-mode finance: tuition, assessment and refunds under DO 88

DO 88 s.2010, the 2010 Revised Manual of Regulations for Private Schools in Basic Education, still governs, and no replacement was found ([DepEd page](https://deped.gov.ph/?p=6543)) [P]. Tuition and other-fee increases, and any new fee, require consultation with parents and learners and an application to the Regional Office. Fees stay at the prior year's rates until approval ([DLS-Zobel memo](https://www.dlszobel.edu.ph/?p=42051)) [P, school document]. DepEd shifts the consultation and application deadlines by memo each year ([Manila Bulletin](https://mb.com.ph/2023/4/9/dep-ed-adjusts-deadline-for-tuition-increase-application-renewal-of-permit-for-private-schools)) [N]. **RA 11984** bars denying exams to enrolled learners over unpaid fees, "for the entire school year" in K to 12, for learners certified as disadvantaged by a social welfare office. It preserves promissory notes and the withholding of records ([LawPhil](https://lawphil.net/statutes/repacts/ra2024/ra_11984_2024.html); [PIA](https://pia.gov.ph/news/2024/03/26/pbbm-signs-law-allowing-disadvantaged-students-to-take-exams-despite-unpaid-school-fees)) [P]. Interest on unpaid tuition requires an express contract clause under DECS Order 63 s.1999 ([DepEd page](https://deped.gov.ph/?p=6134)) [P title; content via Respicio, S]. The refund schedule usually quoted is **10% of total fees charged for withdrawal in week 1, 20% in week 2 and full fees thereafter**, with a non-refundable reservation fee of up to 10% of tuition. It comes from a source that blends DO 88 with the higher-education manual ([lawyer-philippines.com](https://www.lawyer-philippines.com/articles/tuition-fee-refund-before-school-year-starts-philippines)) [S].

The ledger design is carried over from the UMIS specification. It uses journal entries and lines with Σdebit = Σcredit enforced by a deferred constraint trigger, append-only postings with no UPDATE or DELETE grant, corrections by reversal and re-post, typed detail codes, and the balance computed from the subledger.

| ID | Requirement / business rule | Basis |
|---|---|---|
| FEE-01 | (Pvt) GL and student subledger: `journal_entries` (business key unique, `reverses_entry_id`, reason, period) + `journal_lines` (account, debit, credit); balance trigger; app DB role without UPDATE/DELETE; period close; corrections only by reversal | UMIS spec; [I] |
| FEE-02 | (Pvt) Posting map (configurable, auditor-confirmed): charge Dr AR-Learner / Cr Tuition Revenue (or Unearned); payment Dr Cash/Clearing / Cr AR; ESC/voucher credit Dr Receivable-Government (PEAC/DepEd) / Cr AR-Learner; discount Dr Contra-revenue / Cr AR; gateway fee Dr Expense; refund Dr AR or Refund Payable / Cr Cash | [I] |
| FEE-03 | (Pvt) `FeeSchedule` per SY with lifecycle draft → consulted → filed → approved → locked; it attaches consultation evidence (minutes, attendance) and the Regional Office approval reference. If no approval exists by enrollment, the prior SY's approved schedule applies automatically | DO 88 [N]/[S]; [I] |
| FEE-04 | (Pvt) Fee lines by grade level, program/track/cluster, learner category; types tuition, miscellaneous, laboratory, other; each with refundable flag, VAT-exempt flag and GL account. Mid-year increases are blocked | [Respicio](https://www.respicio.ph/commentaries/can-a-private-school-raise-tuition-fees-midyear-without-prior-notice) [S]; [I] |
| FEE-05 | (Pvt) Assessment snapshots the fee-schedule version per learner per SY; subsidy credits (SUB) and discounts post as separate credit lines so gross revenue is preserved | [I] |
| FEE-06 | (Pvt) Payment plans (cash/annual, semestral, quarterly, monthly, or per term) generating `InstallmentDue`s; optional installment surcharge or cash discount only as defined in the approved schedule. No DepEd rule mandates schedules or channels | [I]; gap |
| FEE-07 | (Pvt) Interest and late penalties are off by default and enabled only when the signed enrollment contract contains the clause (contract version stored per learner) | DECS 63 s.1999 [S] |
| FEE-08 | (Pvt) Exam access never depends on balance. Promissory notes (amount, due date, signatory, approval) are tracked, and a `DisadvantagedStatusCertificate` (issuer, SY validity) is recorded for RA 11984 reporting | [RA 11984](https://lawphil.net/statutes/repacts/ra2024/ra_11984_2024.html) [P] |
| FEE-09 | (Pvt) Refund engine: policy table of withdrawal date bands × % of total fees chargeable (seed 10% / 20% / 100%, flagged unverified), refundability per fee item, reservation-fee rule; refunds need approval by someone other than the cashier | [S]; [I] |
| FEE-10 | (Pvt) Discounts (sibling, early payment, academic, employee) are school policy, approved by role, and post as contra-revenue | gap; [I] |
| FEE-11 | (Pvt) Statement of account per term and cumulative, visible to authorized guardians and payers | UMIS spec |
| FEE-12 | (Pvt) EOSY-rites contributions and fees for proms or field trips cannot be completion requirements; such items are flagged optional and never generate holds | DM 015 s.2026 [N] |

### Cashiering and BIR invoicing: invoices, not receipts, and e-invoice readiness

Educational services of DepEd-recognized private schools are **VAT-exempt** (NIRC Sec. 109(1)(H)). Canteen rentals and asset disposals may be VATable ([PwC Tax Alert 28](https://www.pwc.com/ph/en/tax/tax-publications/tax-alerts/2022/tax-alert-28.html)) [N]. Proprietary schools pay a **10% preferential income tax**. Non-stock non-profit schools are exempt on income used actually, directly and exclusively for education ([Grant Thornton](https://www.grantthornton.com.ph/alerts-and-publications/technical-alerts/tax-alert/2021/republic-act-no.-11635-proprietary-educational-institutions-are-subject-to-10-preferential-income-tax-rate-1-from-july-1-2020-to-june-30-2023)) [N]. Under the EOPT Act and RR 7-2024 the **invoice replaced the official receipt** for services ([PwC](https://www.pwc.com/ph/en/tax/tax-publications/taxwise-or-otherwise/2024/eopt-invoicing-clarified.html)) [N]. E-invoicing corrections are made by credit note, never by editing ([KPMG PH](https://kpmg.com/ph/en/insights/2026/09/special-intax-september-2026-issue-1-volume-2.html)) [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| CSH-01 | (Pvt) `CashierSession` (cashier, terminal, opening fund); close requires a denomination count; over/short recorded; closed session locked | UMIS spec |
| CSH-02 | (Pvt) Sales invoices with registered series per terminal, required BIR fields, "VAT-exempt sale" lines for educational fees and separate VATable lines for non-educational sales; tax profile (NSNP vs proprietary) drives wording | [N]; [I] |
| CSH-03 | (Pvt) Gap-free numbers; voids keep their number with supervisor approval (same day); in e-invoice mode corrections are credit notes only | [N]; [I] |
| CSH-04 | (Pvt) EIS adapter (structured e-invoice payload, queue, retry, certification tracking), feature-flagged pending the RDO coverage determination; CAS/CBA registration support (system serials, audit trail, archiving) | RR 11-2025/26-2025, RMC 98-2026 [N] |
| CSH-05 | (Pvt) Channels: cash, check, bank deposit/transfer, InstaPay/PESONet, e-wallets and QR Ph via gateway (INT-04), over-the-counter aggregators; manual proof uploads with a reference number, deduplicated on it and verified by finance | [I] |
| CSH-06 | (Pvt) Daily collection reports by cashier/session/channel and three-way reconciliation (SMIS vs bank vs gateway settlement); unmatched items go to a suspense queue | UMIS spec |

### Subsidies under DO 11 s.2026: government credits are receivables, not discounts

**DO 11 s.2026 (30 Apr 2026)** consolidates ESC, the SHS Voucher Program and the Teachers' Salary Subsidy, and repeals DO 20 s.2017 and DO 20 s.2023 ([DepEd page title](https://www.deped.gov.ph/2026/04/30/april-30-2026-do-011-s-2026-revised-guidelines-on-the-implementation-of-expanded-government-assistance-to-students-and-teachers-in-private-education-e-gastpe-in-the-department-of-educat/)) [P title]. **ESC** pays **₱13,000 (NCR), ₱11,000 (HUCs outside NCR) or ₱9,000 (elsewhere)** per grantee per year. The school receives the lower of the grant and its declared fees, and the grant "shall not be construed as a scholarship or a tuition fee discount". Entry is at Grade 7 only, in priority categories A–D, and TSS rises to ₱24,000 per teacher ([SchoolFinderPH](https://www.schoolfinderph.com/blog/esc-grant-private-school) [S]; [GMA](https://www.gmanetwork.com/news/topstories/nation/986030/deped-targets-2-4m-private-school-subsidy-beneficiaries-for-sy-2026-2027/story/) [N]). The grant continues while the grantee stays in the school, is promoted and keeps passing grades. It can end on drop-out, repetition or suspension longer than two weeks [S]. **SHS VP** values are A/B/C ₱22,500 NCR, ₱20,000 HUC, ₱17,500 other, and D/E ₱18,000, ₱16,000 and ₱14,000. Again the school receives min(fees, voucher). Categories A–D apply at the school and E applies online via OVAP. Nobody is automatically qualified any more ([SchoolFinderPH](https://www.schoolfinderph.com/blog/shs-voucher-program-guide)) [S]. For SY 2026–27 no new Grade 12 vouchers are issued. Redemption runs 3 Aug–3 Nov 2026, and unredeemed vouchers are forfeited. Billing statements are created 1 Aug–7 Oct 2026, with onward routing to PEAC and DepEd by 30 Oct. TSS billing runs 1 Feb–31 Mar 2027 ([NUM-2026-223 / DM 031 s.2026](https://deped-muntinlupa.com/wp-content/uploads/2026/05/NUM-2026-223.pdf)) [D]. From SY 2027–28 only private SHS with **full Government Recognition** (DO 12 s.2026) may join the VP ([NUM-2026-269](https://deped-muntinlupa.com/wp-content/uploads/2026/06/NUM-2026-269.pdf)) [D]. A voucher law ratified in Sept 2026 extends vouchers to K–6 and creates a Bureau of Private Education, but no RA number had been reported ([Tribune](https://tribune.net.ph/2026/09/23/expanded-voucher-law-extends-private-school-aid-to-elementary-learners)) [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| SUB-01 | (Pvt) `GrantProgram` (ESC, SHS VP, TSS, future programs) with versioned rate tables keyed by SY × location tier × category group | [S]; [I] |
| SUB-02 | (Pvt) Credit = min(rate, total assessed fees), posted as Dr Receivable-Government / Cr AR-Learner; the family pays the remainder ("top-up"). No top-up ceiling was found | [S] |
| SUB-03 | (Pvt) Grantee lifecycle: application with category (A–D/E), income band and evidence → committee screening (VP: 10 working days, written notice to ineligible applicants within 3) → slot allocation → grantee per SY → continuation checks (same school, promoted, not suspended > 2 weeks, not repeating) → termination reason | [S]; WEL-07 |
| SUB-04 | (Pvt) Guards: ESC only for Grade 7 entrants unless an exceptional-case approval is recorded; no new SY 2026–27 Grade 12 vouchers; voucher redemption date inside the window; warning if Government Recognition status for SY 2027–28 is unset | [D]; [S] |
| SUB-05 | (Pvt) Voucher learner fields: category, QVA certificate no. (E), redemption date, LRN, PhilSys no. (mandatory from SY 2029–30), track/cluster, G11→G12 continuation | [S] |
| SUB-06 | (Pvt) Billing worksheets matching ESC IMS / SHS VP VMS fields, with the deadline calendar from the yearly memo, and receivable tracking until payment (months after billing) | [D]; [I] |
| SUB-07 | (Pvt) TSS: eligible-teacher roster and annual amount, as a pass-through, not a learner credit | [S] |
| SUB-08 | (Pvt) High-risk data minimization: family income, CBMS/4Ps status and property data are stored encrypted with field-level access, given the 2024 OVAP exposure of 210,020 records | [Inquirer Technology](https://technology.inquirer.net/132322/ph-platform-ovap) [N] |

### Public-mode finance and transparency: no cashier, only accountability registers

Public JHS/SHS charge no tuition. Under DO 41 s.2012, non-payment of voluntary contributions "shall not be used as a basis for non-admission, non-promotion, or non-issuance of clearance". PTA collections are voluntary and agreed in a general assembly, teachers and officials should not collect them, and the PTA reports on how the prior year's money was used ([PNA](https://www.pna.gov.ph/articles/1071316)) [N]. PTA operations fall under DO 13 s.2022 ([DepEd](https://deped.gov.ph/?p=113681)) [P title]. School MOOE is directly released under DO 13 s.2016 and used under DO 12 s.2014 ([DepEd](https://deped.gov.ph/?p=5212)) [P title], through government accounting rather than a learner ledger.

| ID | Requirement / business rule | Basis |
|---|---|---|
| PUB-01 | (Pub) All learner-facing finance features are disabled: no assessment, cashier, balance or financial hold (PLT-05) | [N] |
| PUB-02 | (Pub) MOOE register: allocation per release, disbursements by category, liquidation status and attachments; maintained by the school head and bookkeeper/admin officer, not teachers | DO 13 s.2016 [P title]; DO 2 s.2024 [P]; [I] |
| PUB-03 | (Pub) PTA and voluntary-contribution transparency register maintained by PTA officers, never linked to learner status, with an annual financial report publishable on the website | [N]; [I] |
| PUB-04 | (Pub) Canteen income records if the school operates one (governing issuance unverified) | gap |
| PUB-05 | (Pub) Transparency page on the website for MOOE summaries and PTA reports; posting obligations to be confirmed (see WEB-08) | [I] |

### Parent and learner portal and communications: authoritative record, SMS reach, Messenger reality

Facebook Messenger group chats are the dominant teacher–parent channel in Philippine studies, though mostly from the pandemic era. Parents value the responsiveness, while teachers report strain on work-life balance ([ResearchGate](https://www.researchgate.net/publication/359202427_Exploring_the_Experiences_of_Filipino_Parents_on_Distance_Learning_During_COVID-19_Pandemic_Exploring_the_Experiences_of_Filipino_Parents_on_Distance_Learning_During_COVID-19_Pandemic); [ResearchGate](https://www.researchgate.net/publication/370394592_Post-Pandemic_Aspirations_of_Filipino_Elementary_School_Teachers)) [S]. Local SMS costs about **₱0.56 per message** before VAT ([Semaphore](https://www.semaphore.co)) [P], so 1,000 parents × 4 messages a month is about ₱2,240 [I]. DO 49 s.2022 bars staff from social-media interaction with learners outside school except relatives ([GMA](https://www.gmanetwork.com/news/topstories/nation/850283/deped-reminds-employees-to-avoid-relationships-social-media-chats-with-students-outside-school/story/)) [N]. That argues for a school-controlled, logged channel instead of private chats [I]. DO 017 bars disclosing learner PII, including on social media, without explicit consent of **both the learner and the parent/guardian** [D]. NPC Advisory Opinion 2025-017 addresses parents' access to a child's school records ([NPC](https://privacy.gov.ph/wp-content/uploads/2026/01/NPC-Advisory-Opinion-No.-2025-017_Redactedv2.pdf)) [P].

| ID | Requirement / business rule | Basis |
|---|---|---|
| POR-01 | Guardian link (relationship, custody/authority basis, verification by registrar against the BEEF and ID) with default scopes for minors: attendance, grades, SF9, schedule, announcements, (Pvt) SOA/payments, incident notices concerning their own child. Health and guidance details are excluded by default | UMIS spec; NPC AO 2025-017 [P]; [I] |
| POR-02 | Multiple children per guardian and multiple guardians per learner; court-order or custody restrictions block a specific guardian | [I] |
| POR-03 | Learners aged 18+ enroll themselves (DO 017) and control guardian scopes; at the 18th birthday the system prompts the learner to confirm or revoke | DO 017 [D]; [I] |
| POR-04 | Learner portal: schedule, term grades once released, attendance, assignments links (Classroom), handbook, consents, records requests | [I] |
| POR-05 | Grade release control: period grades become visible only after locking and the configured release date | [I] |
| POR-06 | (Pvt) Pay-by-reference for payers without grade visibility; online payment (INT-04) | UMIS spec |
| POR-07 | Mobile-first, low-bandwidth web (no mandatory native app), Filipino/English labels, accessible authentication (WCAG 3.3.8: no cognitive puzzles) | [W3C](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/) [P]; [I] |
| COM-01 | Notification service: in-app, email, SMS (gateway adapter), optional web push; templates per event (absence, 5-consecutive-absence alert, grade release, due date, class suspension, incident notice); per-guardian channel preferences and quiet hours | [I] |
| COM-02 | Announcement composer that also produces copy-ready text and a short link for teachers' Messenger groups, so SMIS stays the source of truth | [I] |
| COM-03 | Teacher–guardian messaging inside SMIS with configurable office hours, school-context only, retained and auditable; teacher–learner messaging limited to class contexts | DO 49 s.2022 [N]; [I] |
| COM-04 | Urgent broadcasts (class suspension) via SMS + website banner + portal, with delivery logs | [I] |

### Integrations: Google Workspace first, gateway webhooks always signed

DepEd and Google are deploying **one million Google Workspace for Education Plus accounts** for teachers and staff ([BusinessMirror](https://businessmirror.com.ph/2025/03/15/deped-google-equip-teachers-with-workspace-for-education-plus-suite/)) [N]. Learner accounts are provisioned through School ICT Coordinators ([DepEd G Suite training site](https://sites.google.com/deped.gov.ph/gsuitetraining/accounts)) [P]. Storage is capped at 100 GB for employees and 20 GB for learners ([DepEd Laguna](https://depedlaguna.com/implementation-of-storage-limits-for-deped-google-workspace-for-education-account/)) [D]. A 2023 school post claims official email moved to Microsoft 365, so the official identity provider is unclear ([Alapan 1 ES](https://alapan1es.com/2023/01/30/microsoft-365-adoption/)) [S]. **PayMongo's published rates** (VAT-exclusive) are local cards 3.125% + ₱13.39, GCash 2.23%, Maya 1.79%, QR Ph 1.34% and direct online banking 0.71% or ₱13.39, with standard settlement in 2–7 days ([PayMongo](https://www.paymongo.com/pricing)) [P]. Xendit, Maya Checkout and Dragonpay rates come only from conflicting third-party blogs [S].

| ID | Requirement / business rule | Basis |
|---|---|---|
| INT-01 | SSO: Sign in with Google (deped.gov.ph or school domain) and optionally Microsoft Entra; identity provider configurable per school; staff MFA enforced by the IdP or SMIS | [N]; [I] |
| INT-02 | Google Classroom roster push: course = section × subject × period, teachers and learners from SMIS; nightly reconciliation; archive at period end | [I] |
| INT-03 | Classroom coursework grade pull into GRD as proposed assessment items (GRD-09); Drive links instead of local file storage for learning artifacts | [I] |
| INT-04 | (Pvt) Payment gateway adapter (PayMongo first; others pluggable): checkout per invoice/installment, confirmation only by signed webhook, idempotent on provider reference, settlement-file reconciliation net of fees, gateway fees posted as expense, per-channel convenience-fee pass-through setting, default channels QR Ph/online banking | [PayMongo](https://www.paymongo.com/pricing) [P]; [I] |
| INT-05 | SMS gateway adapter (local aggregator) with delivery receipts and cost tracking | [P]; [I] |
| INT-06 | LIS: no API found, so SMIS produces validated worksheets and form layouts per LIS facility, and imports LIS-generated SF1/SF5 for reconciliation | [Schoolites](https://schoolites.com/school-management-system-philippines) [S]; [I] |
| INT-07 | (Pvt) ESC IMS / SHS VP VMS billing exports (SUB-06); (Pvt) BIR EIS (CSH-04) | [D]; [N] |
| INT-08 | Moodle, DepEd Commons/LRMDS treated as links unless an API is confirmed; OneRoster/LTI deferred | [I] |
| INT-09 | Every integration has an owner, a purpose-limited data view (Classroom never sees finance, health or incidents), a data-sharing/outsourcing agreement record and a reconciliation report | UMIS spec; [Philstar NPC](https://www.philstar.com/headlines/2026/11/12/2569565/npc-confirms-data-breach-10-government-agencies) [N] |

### Data privacy for minors and security baselines

DO 017 Sec. X sets the enrollment privacy rules [D]. Data may be collected only for enrollment and related purposes, with technical and organizational safeguards and need-to-know access. PII may not be disclosed to third parties "including on social media, without explicit consent of the learner and parent/guardian". BEEF and confirmation slips are destroyed after one year. Division memos forbid posting learner names, sections or addresses online without parental consent, and require consent forms for learner images under DO 40 ([SDO Tangub DM 050 s.2025](https://tangub.deped.gov.ph/wp-content/uploads/2025/02/divmemo050_2025.pdf)) [D]. A 2019 advisory bans posting LIS screenshots, LRNs or enrollment histories publicly ([Summit Express](https://www.thesummitexpress.com/2019/04/deped-warns-posting-diploma-information-social-media.html)) [N]. NPC Bulletin 16 requires a parent or guardian's explicit consent for recording or proctoring minors online ([NPC](https://privacy.gov.ph/?p=11354)) [P]. From the UMIS specification, **NPC Circular 2023-06** (effective 30 Mar 2024) requires a privacy impact assessment per processing system ([NPC](https://privacy.gov.ph/?p=46138)) [P]. **NPC Circular 2022-04** requires DPO and system registration for organizations with 250+ employees or processing sensitive data of 1,000+ individuals ([Circular 2022-04](https://privacy.gov.ph/wp-content/uploads/2023/05/Circular-2022-04.pdf)) [P]. OWASP ASVS 5.0.0 was released 30 May 2025 ([OWASP](https://github.com/OWASP/ASVS)) [P]. The NPC reminded organizations in Nov 2026 that **outsourcing IT does not remove Data Privacy Act obligations**, and that breach notification under Circular 16-03 is mandatory ([Philstar](https://www.philstar.com/headlines/2026/11/12/2569565/npc-confirms-data-breach-10-government-agencies)) [N].

| ID | Requirement / business rule | Basis |
|---|---|---|
| PRV-01 | Field classification Public / Internal / Confidential / Sensitive. Sensitive includes disability, health/BMI, religion, IP ethnicity, 4Ps/CBMS status, family income, birth-certificate data, incident and guidance records. Serializers drop sensitive fields unless the actor holds the scoped `view_sensitive` permission | RA 10173 [P]; [I] |
| PRV-02 | Versioned privacy notices at every collection point (website forms, BEEF, portal), lawful-basis tagging per purpose, DPO contact displayed (public schools: DepEd DPO channel; private schools: own DPO) | [D]; [I] |
| PRV-03 | Consent records captured with the BEEF (guardian signature, and the learner's where required); separate opt-ins for photo/name publication, honors-list publication, recordings, and any AI processing; withdrawal is immediate and propagates to the CMS (WEB-07) | DO 017 [D]; NPC Bulletin 16 [P]; [I] |
| PRV-04 | Publication guard: no LRN, learner list, section roster, grade or identifiable photo leaves SMIS to a public surface without a consent check | [N]; [D] |
| PRV-05 | Retention schedule as data per record class: BEEF/slip scans 1 year; raw class-record data ≥ 1 SY; SF10 permanent; financial records per BIR (period to confirm); disposal log | DO 017 [D]; [S] |
| PRV-06 | Data-subject request workflow (access, correction, deletion where lawful) with SLA; breach register with a 72-hour timer and NPC template; PIA record per module; registration status per NPC 2022-04 thresholds (a school with < 1,000 learners may fall below them, so check) | [P]; [I] |
| PRV-07 | (Pvt) The private school is its own personal information controller; vendor/hosting agreements recorded | [I]; NPC [N] |
| SEC-01 | OWASP ASVS 5.0 Level 2 overall; Level 3 controls for authentication, authorization, audit and cryptography in grades, finance and welfare modules | UMIS spec [P]; [I] |
| SEC-02 | Append-only, hash-chained `audit_events` (actor, impersonator, role/scope snapshot, IP, correlation ID, action, subject, masked before/after, reason); INSERT/SELECT-only grant; reads of sensitive records logged | UMIS spec; [I] |
| SEC-03 | Staff MFA (or IdP-enforced MFA); server-side Redis sessions; idle timeouts; re-authentication for grade locking, refunds, role grants | UMIS spec; [I] |
| SEC-04 | No publicly reachable databases or storage buckets; encryption in transit and at rest; encrypted casts and blind indexes for IDs and income; KMS-held keys | OVAP lesson [N]; [I] |
| SEC-05 | Nonce-based CSP with no inline scripts, CSRF protection, no `v-html` on user content, rate limits on login, OTP, public forms and the verification endpoint | UMIS spec; [I] |
| SEC-06 | PostgreSQL row-level security as a backstop on grades, welfare, health and ledger tables; a non-owner app role with `SET LOCAL` user context per transaction | UMIS spec; [I] |
| SEC-07 | Encrypted daily backups with WAL-based point-in-time recovery, immutable off-site copies, quarterly restore drills (proposed RPO ≤ 15 min, RTO ≤ 4 h) | UMIS spec; [I] |
| SEC-08 | Load tests for enrollment week, grade-release days and early-registration peaks; graceful degradation (queue, retry), given recurring LIS peak-load failures | [ilovedeped](https://www.ilovedeped.net/2025/04/lisdepedgovph-login-guide-how-to-access.html) [S]; [I] |

### DepEd reporting: exports from one record, SBM only for public schools

DO 007 s.2024 revised School-Based Management, repealed DO 83 s.2012 and requires public schools to self-assess ([SDO Dasmariñas](https://www.depeddasma.edu.ph/dm-no-431-s-2024-dissemination-of-deped-order-no-007-s-2024-policy-guidelines-on-the-implementation-of-the-revised-school-based-management-system/)) [D]. SF4 feeds division enrollment statistics ([SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-school-forms-guide)) [S]. DepEd attributed an apparent private-enrollment drop to reporting lag ([Inquirer](https://newsinfo.inquirer.net/1497758/deped-blames-lag-in-reporting-for-private-school-enrollment-drop)) [N], which is a reminder that exports must match what the LIS holds.

| ID | Requirement / business rule | Basis |
|---|---|---|
| RPT-01 | LIS worksheets per facility (early registration, Quick Count, BOSY, SHS BOSY/2nd sem, tagging, EOSY status) generated from SMIS data with validation | [P]; [I] |
| RPT-02 | SF1–SF10 per SF table above; reconciliation pack before EOSY | [P]; [S] |
| RPT-03 | BEIS school-profile data (rooms, seats, toilets, personnel counts, enrollment by grade/sex); collection cycle unverified | [I] |
| RPT-04 | (Pub) SBM self-assessment evidence repository and SIP/AIP tracking (Annex indicators unverified) | DO 007 s.2024 [D] |
| RPT-05 | DO 006 bullying and incident reports; RA 11984 disadvantaged-certificate counts (Pvt) | [S]; [P] |
| RPT-06 | (Pvt) Subsidy billing and grantee reports (SUB-06); TOSF increase application pack (FEE-03) | [D]; [I] |
| RPT-07 | Every statutory export is reproducible from a stored snapshot with its template version | UMIS spec; [I] |
| RPT-08 | Dashboards for the principal: enrollment vs prior year, attendance and at-risk counts, grade-submission status, SRC counts, incident SLA status, (Pvt) collections and receivables | [I] |

### Personnel: a minimal record now, HR later

| ID | Requirement / business rule | Basis |
|---|---|---|
| HR-01 | Employee record: identity, position, (Pub) plantilla item, employment status, PRC licence and expiry, LET status, RGC licence, designations, trainings | [I] |
| HR-02 | Teaching assignments and ancillary designations from TLD; overload ledger | DO 5 s.2024 [N] |
| HR-03 | RPMS/IPCRF ratings and PPST career stage per year (order versions unverified); SF7 output | gap; [I] |
| HR-04 | Payroll out of scope for Phase 1; (Pvt) TSS roster (SUB-07) | [I] |

## The public website should be the canonical source that Facebook points to

### The evidence on Facebook-only schools is real but unquantified

The earlier website research looked at higher-education institutions. CHED counted about 2,334 HEI campuses in AY 2024–25, yet Webometrics, which crawls any institutional domain, listed only **365** Philippine HEIs in January 2023. That is a rough proxy suggesting many small institutions have little independent web presence ([CHED statistics](https://legacy.ched.gov.ph/statistics/); [UPOU](https://www.upou.edu.ph/news/up-leads-countrys-webometrics-world-ranking-upou-ranks-22nd)) [S]. No study measured the share of Facebook-only institutions, and no data at all was found for JHS–SHS schools. The claim that many Philippine schools rely only on Facebook pages is therefore plausible and widely observed, but unquantified. For public schools, DO 007 s.2026 reportedly makes the official Facebook page part of the governance framework. Pages must be created with a @deped.gov.ph office email and carry the exact school name ([eduknasyon](https://eduknasyon.blogspot.com/2026/03/deped-order-007-s-2026-media-management.html)) [S]. CHED's repeated warnings about impostor pages show why an official domain matters as a trust anchor ([Inquirer](https://newsinfo.inquirer.net/1867070/ched-warns-vs-unofficial-fb-pages-posting-false-info-on-scholarships)) [N]. The design conclusion is to keep Facebook as the daily announcement channel and make the website the authoritative reference. Every post links back to a canonical page, and the website carries what Facebook cannot: the Learner Handbook, the enrollment funnel, fee transparency, document verification and an accessible calendar [I].

Accessibility is where Philippine institutional sites are weakest. A June 2026 study of 17 SUC websites, one per region, found **none fully compliant** with WCAG 2.1 and national standards ([Lagura et al.](https://so03.tci-thaijo.org/index.php/ppmjournal/article/view/294027)) [P]. NN/g's university study, which included parents among its 33 users, found users missing deadlines, unable to find programs and losing trust over stock imagery and contradictory duplicate content ([NN/g](https://www.nngroup.com/articles/university-sites/)) [P]. These findings transfer to a JHS–SHS school with one adjustment: the decision-maker for Grade 7 and Grade 11 entry is usually the parent, so the site speaks to parents first and learners second [I]. The RNL survey of US high-school students (majors 57%, scholarships and aid 49%, cost 39%, admissions process 38%) ([RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)) [P] maps onto SHS tracks/electives, ESC/voucher eligibility, approved fees and enrollment steps. It is US evidence and directional only.

### Information architecture for a single JHS–SHS school

The primary navigation is **Enroll | Academics (JHS, SHS tracks and electives) | Learner Support (guidance, health, child protection, inclusive education) | About | News & Announcements | Calendar**. The utility bar holds **Parents, Learners, Alumni, Portal login, Enroll CTA, Search, EN/FIL**. The footer holds the privacy notice and DPO contact, accessibility statement, Learner Handbook, child-protection hotlines (911, 1383, 1553 per DO 006), (Pub) transparency, (Pvt) DepEd permit/recognition numbers and approved fees, careers, contact and a map. The homepage order on mobile is hero with one CTA (Enroll / Early Registration open) → urgent banner (class suspension) → enrollment key dates from CAL → SHS track/cluster finder → announcements → news → events → outcomes (aggregate, consented) → footer [I].

| ID | Requirement / business rule | Basis |
|---|---|---|
| WEB-01 | Public site server-rendered (Blade or Inertia SSR) inside the monolith, separated from the portal by route group and session; clean URLs, canonical tags, per-type XML sitemaps, Open Graph tags for Facebook sharing | [I] |
| WEB-02 | Curriculum-driven pages: JHS learning areas and SHS tracks/clusters/electives generated from CUR (hours, prerequisites, Work Immersion), with editor-owned descriptions, facilities and career links. A cluster no longer offered hides automatically | Website notes [I] |
| WEB-03 | Enrollment funnel. (Pub) Early-registration form for G7/G11/transferees in the configured window (no fees, "does not guarantee enrollment", minimal fields, consent) → confirmation screen with next steps + email/SMS → handoff to ENR-02. (Pvt) Inquiry → application → entrance-test booking → results → reservation → enrollment, plus ESC/voucher eligibility explainer. Forms prefill across steps (WCAG 3.3.7) | DO 017 [D]; [W3C](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/) [P]; [RNL](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf) [P] |
| WEB-04 | Content types: Page (blocks), News, Announcement (priority, expiry, audience), Event (iCal), Calendar (read-only from CAL, public items only), Download/Form (versioned, owner, revision date), Club/Program page, Staff directory (consented fields only), Job posting, Transparency item | Website notes [I] |
| WEB-05 | CMS workflow Draft → In Review → Approved → Scheduled/Published → Archived; roles Contributor (teachers, club advisers), Editor (coordinators), Publisher (principal or designated web officer); revision history with restore, preview links, scheduled publish/expire, required alt text, audit log, named owner and review interval per page | Website notes [I]; DO 007 s.2026 page-editor approval [S] |
| WEB-06 | Facebook crossposting: announcements published on the site generate a post draft and link; the website URL is canonical | [I] |
| WEB-07 | Media consent guard: media assets can be tagged with learners. Publishing is blocked if any tagged learner lacks a current publication consent, and withdrawal of consent unpublishes affected assets | DO 017 Sec. X [D]; DO 40 memos [D]; [I] |
| WEB-08 | (Pub) Transparency section (MOOE summaries, PTA reports, procurement notices "on the website, if any" where the school procures) pending confirmation of the obligations that actually apply | [GPPB Circular 01-2021](https://www.gppb.gov.ph/wp-content/uploads/2023/05/GPPB-Circular-No.-01-2021.pdf) [P]; [I] |
| WEB-09 | Required publications: Learner Handbook (DO 006), privacy notice, accessibility statement, child-protection policy and hotlines, school calendar, (Pvt) approved fee schedule and refund policy | DO 006 [S]; [I] |
| WEB-10 | Document verification: each school-issued certificate (enrollment, good moral, Grade 10 completion, SHS diploma, CTC of SF10) carries a random 128-bit token and short code; the QR encodes `https://<school-domain>/verify/<token>`; the page shows only name, document type, issue date, serial and valid/revoked status, optionally after the verifier enters the learner's surname or birth date; rate-limited, logged, revocable. A verification page is reachable from the site's own navigation, because commentary warns verifiers not to rely on a printed QR alone | Website notes; [Respicio](https://www.respicio.ph/commentaries/how-to-verify-whether-a-diploma-is-authentic-in-the-philippines) [S]; [I] |
| WEB-11 | QR codes are not added to official DepEd forms (SF9, SF10 layouts) until it is confirmed that this does not breach DO 58's "no other forms" rule; verification of those forms runs through the CTC log instead | DO 58 [S]; [I] |
| WEB-12 | Accessibility: WCAG 2.2 AA including 2.4.11 Focus Not Obscured, 2.5.7 Dragging Movements, 2.5.8 Target Size (24×24 px minimum; design to 44 px), 3.2.6 Consistent Help, 3.3.7 Redundant Entry, 3.3.8 Accessible Authentication; no CAPTCHA puzzles; axe/pa11y in CI | [W3C](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/) [P] |
| WEB-13 | Performance: Core Web Vitals "good" at p75 on mobile (LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1); responsive AVIF/WebP images, hero ≤ ~150 KB, no autoplay video on mobile, minimal JS with islands for forms and finder, lazy social embeds, RUM via web-vitals | [web.dev](https://web.dev/articles/vitals) [P]; [I] |
| WEB-14 | SEO: JSON-LD for the school (schema.org school type with address, logo, `sameAs` to the official Facebook page), `Event`, `NewsArticle`, `BreadcrumbList`, `JobPosting`; no reliance on Course rich results, which Google retired in 2025 | [Google](https://developers.google.com/search/blog/2025/06/simplifying-search-results) [P]; [I] |
| WEB-15 | Search: PostgreSQL full-text with `unaccent` and trigram, best bets (enrollment, calendar, fees, handbook), zero-result logging | [I] |
| WEB-16 | Multilingual: English and Filipino for enrollment, announcements and FAQ pages, with per-entry locale and fallback | [I] |
| WEB-17 | Security: hardened CMS, WAF/CDN, defacement and malicious-redirect monitoring, subdomain inventory, separation from the portal; never publish LRNs or learner lists | [Rappler](https://www.rappler.com/technology/263568-up-visayas-down-after-defacement/) [N]; [N] |

## Core entities: one person, dated rules, immutable transactions

Setup tables are versioned by school year. Transactional tables (enrollments, attendance, grades, ledger, holds, incidents, audit) are append-only or versioned, with reversal or compensating rows [I].

| Domain | Entities | Key rules |
|---|---|---|
| Platform | Person, PersonName/Address/Contact (history), User, Role, Permission, RoleAssignment (scope, validity, granted_by), Delegation, AuditEvent, WorkflowDefinition/Instance/Action, HoldType, HoldImpact, PersonHold, ChecklistTemplate/Item, CommunicationTemplate/Log, Notification, Comment, NumberSequence, DocumentTemplate (versioned), IssuedDocument, VerificationToken, ImportJob/ExportJob, Outbox, WebhookSubscription, IdempotencyKey | ULIDs; audit hash-chained |
| Rules store | SchoolProfile (mode, School ID, tier, tax profile), PolicySet, PolicyVersion, IssuanceCitation, VerificationStatus | Locked once used |
| Calendar | SchoolYear, GradingPeriod, PeriodBlock, CalendarEvent, ClassSuspension, LISWindow, ProgramCalendarDeadline | Period structure per SY and program family |
| Curriculum | CurriculumFramework, CurriculumVersion, LearningArea, Subject (versioned), SubjectComponent, GradingCategory, Track, Strand/ElectiveCluster, Elective, Prerequisite, TimeAllotmentRule | Bound to learner-section per SY |
| Learner and enrollment | Learner (LRN), Guardian, GuardianLink, GuardianAccessGrant, LearnerGroupAttribute (IP, LWD, 4Ps, religion, mother tongue), EarlyRegistration, EnrollmentForm (BEEF/Confirmation version), Enrollment (SY, status), EnrollmentStatusHistory, DocumentRequirement, LearnerDocument, AffidavitOfUndertaking, TransferRequest, LISTag, ExternalAssessment | LRN never generated |
| Records and credentials | PermanentRecord (SF10), RecordsRequest, RecordsDispatch, CertifiedTrueCopy, Certificate, Diploma, RecordCorrection | Single original + CTC log |
| Sections and loading | Section, Room, ClassProgram, ClassPeriod, SubjectOffering, TeachingAssignment, Designation, LoadPolicy, OverloadEntry | Clash checks |
| Attendance | AttendanceMark, AttendanceExemption, AtRiskAlert, HomeVisitTask | Feeds SF2/SF4 |
| Grading | GradingScheme, SchemeComponent, WeightMatrix, TransmutationTable, DescriptorSet, ClassRecord, AssessmentItem, Score, PeriodGrade, FinalGrade, GeneralAverage, GradeLock, GradeChangeRequest, CoreValueRating | Snapshot of scheme per grade |
| Promotion and awards | PromotionRuleSet, PromotionDecision, RemedialSection, RemedialMark, BackSubject, AwardDefinition, AwardResult, RankCertificationRequest | Derived, recomputable |
| Welfare | Incident, IncidentParty, IntakeSheet, RiskAssessment, Case, CaseDeadline, Notice, Answer, Decision, Appeal, Sanction, Referral, ConfiscationSlip, BagInspection, CPCMembership, CounselingSession, HealthRecord (SF8), ClinicVisit | RLS; read-logged |
| Finance (Pvt) | Account, JournalEntry, JournalLine, DetailCode, FeeSchedule (status, approval evidence), FeeLine, EnrollmentContract, Assessment, AssessmentLine, PaymentPlan, InstallmentDue, Discount, PromissoryNote, DisadvantagedStatusCertificate, RefundPolicy, Refund, StatementOfAccount, FiscalPeriod | Σdebit = Σcredit; no UPDATE/DELETE |
| Cashiering (Pvt) | CashierSession, Terminal, Payment, PaymentAllocation, InvoiceSeries, Invoice, CreditNote, GatewayTransaction, Settlement, SuspenseItem, Deposit, Reconciliation, EInvoiceTransmission | Gap-free; idempotent |
| Subsidies (Pvt) | GrantProgram, GrantRateTable, GrantApplication, GrantCategoryEvidence, Grantee (per SY), ContinuationCheck, GrantTermination, BillingStatement, GovernmentReceivable, TSSTeacher | Receivable ≠ discount |
| Public finance (Pub) | MOOERelease, MOOEDisbursement, Liquidation, PTAReport, ContributionRecord, CanteenRecord | Never linked to learner status |
| Personnel | Employee, Licence, Rating, Training | Minimal Phase 1 |
| Communications and portal | Announcement, MessageThread, Message, ChannelPreference, SMSDispatch | Retained, auditable |
| Privacy | PrivacyNoticeVersion, ConsentRecord (purpose-specific), DataSubjectRequest, BreachIncident, PIARecord, RetentionRule, DisposalLog, DataSharingAgreement | Consent propagates to CMS |
| Website | Site, Page, Block, Entry (typed), Revision, MediaAsset, MediaLearnerTag, Inquiry/Prospect, Redirect, SearchLog | Owner + review date |
| Reporting | ExportTemplate (versioned), ExportRun (snapshot), ReconciliationRun, SBMEvidence (Pub) | Reproducible |

## Roles: scope does the work, separation of duties keeps grades and money honest

Roles are permission bundles assigned with a scope (school, key stage, grade level, section, subject offering, caseload, terminal) and a validity period. Spatie-style permission bundles plus a custom `role_assignments` table and Laravel Policies were the UMIS design, with PostgreSQL row-level security as a backstop. That design carries over unchanged [I]. A teacher who is also an adviser holds two assignments, so permissions follow the scope of each, not the person.

| Role | Scope | Key permissions | SoD and notes | Mode |
|---|---|---|---|---|
| School Head / Principal | School | Lock grades, approve promotion lists and awards, approve grade changes, certify SF9/SF10 (dry seal), approve overloads, attendance exemptions, late-enrollment exceptions; (Pub) MOOE oversight and LIS school-head account | Cannot lock grades they encoded as a teacher; certifies, does not prepare | Both |
| Assistant Principal / Academic Coordinator | Key stage or school | Review grade submissions, class programs, teacher loading, SRC | Reviewer ≠ encoder | Both |
| Owner / President / Board treasurer | School | Approve fee schedules, refunds above threshold, write-offs, discounts policy, period close | Cannot post payments | Pvt |
| Registrar / Records Officer (public: School Enrollment Focal Person, LIS coordinator) | School | Enrollment intake, document checklists, LIS worksheets, records requests and dispatch, CTC issuance, certificates | Cannot release a financial hold; cannot edit locked grades | Both |
| Grade-Level Coordinator | Grade level | Section monitoring, form consolidation, attendance compliance | — | Both |
| Class Adviser | Own section | BEEF encoding to LIS worksheet, SF1/SF2/SF8 preparation, attendance, consolidate grades, prepare SF9/SF10, home-visit tasks, guardian contact | Prepares SF10; school head certifies | Both |
| Subject Teacher | Own subject offerings | Class records, assessment items, submit term grades, attendance for own periods, Classroom sync | Cannot lock or change after lock | Both |
| SHS Track/Cluster Coordinator | Track/cluster | Elective offerings, Work Immersion placements, SHS VP liaison (Pvt) | — | Both |
| Guidance Counselor / School Counselor (RA 12080) | Assigned caseload | Counseling records, referrals, CPC membership | Notes invisible to all other roles by default; licensed only | Both |
| School Counselor Associate | Assigned caseload, supervised | Limited counseling records | Supervisor sign-off | Both |
| Learner Formation Officer / Discipline Officer | School | Incident intake, case management, sanctions recommendations | Cannot decide cases they investigated where DO 006 separates roles | Both |
| Child Protection Committee member | Assigned cases | Risk assessment, case review | Case-scoped access only; parent/learner reps see only what the CPC role permits | Both |
| Disciplining Authority | School | Decisions on notices and answers | ≠ investigator | Both |
| School Nurse / Clinic | School | SF8, clinic visits, health records | Health data restricted | Both |
| Cashier | Terminal | Open/close sessions, post payments, issue invoices, request voids | Cashier + refund approver is a blocked static conflict | Pvt |
| Accounting / Student Accounts | School | Assessments, payment plans, promissory notes, holds placement and release, reconciliation, SOA | Proposes discounts and refunds; cannot approve own | Pvt |
| Subsidy (ESC/SHS VP) Coordinator | School | Grantee applications, committee records, billing worksheets | Screening ≠ billing submission approval | Pvt |
| Bookkeeper / Administrative Officer | School | MOOE register, liquidation records, property and textbooks (SF3) | Takes clerical work off teachers (DO 2 s.2024) | Pub (Pvt optional) |
| PTA Officer | PTA | Contribution and PTA financial reports | No access to learner records; teachers do not hold this | Pub |
| Web Editor / Publisher | Site sections | CMS content and publishing | Publisher approval required; media consent guard cannot be overridden | Both |
| ICT Coordinator / System Administrator | School | Configuration, integrations, account provisioning | Cannot grant roles to self; high-privilege grants need a second approver | Both |
| Data Protection Officer | School (Pvt); DepEd DPO channel (Pub) | Consent, DSAR, breach and PIA registers, read-access logs | Alerted on break-glass and impersonation | Both |
| Internal Auditor | School | Read-only across modules and audit log | No writes | Both |
| Parent / Guardian | Linked learner(s), granted scopes | Read grades, attendance, SF9, SOA; pay; confirm re-enrollment; consents; messages | Scope from verified link and grants, never from role alone | Both |
| Learner | Self | Own schedule, grades, attendance, handbook, consents (18+: guardian scopes) | — | Both |
| Applicant family / Prospect | Own inquiry or application | Early registration or application, document uploads, booking | Applicant ≠ learner until enrollment | Both |
| Integration service account | Purpose-limited | OAuth scopes ∩ role | Never exceeds its role | Both |

Three SoD rules matter most. **Grades:** the teacher encodes, the adviser consolidates, the coordinator reviews and the principal locks. A change after locking needs a request approved by someone other than the requester, with before/after values logged. **Money:** the cashier posts, accounting proposes refunds and discounts, and the owner or treasurer approves. Fee schedules carry consultation evidence before approval. **Welfare:** the investigator, the Disciplining Authority and the appellate route stay separate, guidance notes are visible only to counselors, and every read of a case file is logged. Break-glass access requires a reason, alerts the DPO and expires within hours. Impersonation is read-only and never targets a higher-privileged user [I].

## Public and private modes differ by policy, not by codebase

| Feature | Public mode | Private mode | Basis |
|---|---|---|---|
| Enrollment policy | DO 017 s.2025 | DO 017 s.2025 plus own admission conditions (tests, interviews) | [D] |
| Early registration | Required window (last Sat Jan–last Fri Feb); school-head LIS account encodes daily | Encouraged, not required | [D]; [SDO Muntinlupa](https://deped-muntinlupa.com/wp-content/uploads/2026/01/NUM-2026-012.pdf) [D] |
| Fees at enrollment | Prohibited as a prerequisite | Assessment, reservation fee, enrollment contract | [D] |
| School calendar | DO 009 s.2026 three terms mandatory | Own calendar; three-term optional; minimum class days | [N] |
| Grading | DO 15 s.2026 binding | DO 15 encouraged; modifications need Regional Office approval (store approval reference) | [S] |
| Awards | DO 15 Academic Excellence Award | DO 15 or approved variant | [S] |
| Teacher load limits | DO 5 s.2024 / RA 4670 (6 h teaching + 2 h ancillary) | School policy / CBA | [N]; [K] |
| Welfare framework | DO 40 + DO 006 s.2026 binding | DO 40 and RA 10627 apply; DO 006 encouraged | [S] |
| Tuition, cashiering, invoicing | Disabled | DO 88 fee schedules, BIR invoices, e-invoicing per coverage | [P]; [N] |
| Credential holds | Never on financial grounds | Allowed under DM 023 with accommodation rules; never blocks exams, rites, LIS response | [D] |
| Subsidies | — (ESC/VP not applicable) | ESC (G7 entry), SHS VP (A–E), TSS; IMS/VMS billing | [S]; [D] |
| RA 11984 | Not applicable in practice (no fees) | Exam access for certified disadvantaged learners; promissory notes | [P] |
| MOOE / PTA transparency | MOOE register, PTA reports, transparency page | Optional | [N]; [I] |
| SBM / SIP | Required (DO 007 s.2024) | Not applicable | [D] |
| Official social media | @deped.gov.ph page rules (DO 007 s.2026) | Persuasive only; RA 10173 applies | [S] |
| Data privacy controller | DepEd DPO structure | School is its own PIC; own DPO/registration check | [D]; [I] |
| Identity provider | DepEd Google Workspace (or M365) | Own Workspace/M365 tenant | [N]; [I] |
| Government Recognition (SHS) | — | Full recognition needed for SHS VP from SY 2027–28 | [D] |

## Verification register: check these before relying on them

Each item stays configurable data or a feature flag until it is confirmed. "Primary" means the signed PDF on deped.gov.ph, the BIR, NPC or PEAC text, or written advice from the named authority.

| # | Item | Current basis and why it is uncertain | Who confirms | Design safeguard |
|---|---|---|---|---|
| 1 | **BIR e-invoicing coverage** of the private school (CAS/CBA user? NSNP vs proprietary), the 31 Dec 2026 deadline, EIS payload, PTI and certification steps | [N] Big-4 summaries; no school-specific source; no accredited provider as of Sep 2026 | Tax adviser / RDO — **urgent, about 6 weeks** | CSH-04 flag; credit-note model regardless |
| 2 | Invoice-vs-receipt rules after EOPT (RR 7-2024 / RR 11-2025) for tuition; required invoice fields; book-retention period | [N]/[K] | Tax adviser | Configurable invoice template; retain ≥ 10 years |
| 3 | DO 15 s.2026 full text: every weight cell (JHS and SHS groups), EX sub-weights, VE domain split, WW/PT/EX caps | [S] DepEdClub only for SHS; PDF not retrieved | DepEd PDF; Regional Office | Seeds marked `secondary` |
| 4 | DO 15 adjusted transmutation table (all rows) and scope (KS2–KS4, Grades 2–3) | [S] one source; anchor [N] | DepEd PDF | Table as data; boundary tests |
| 5 | DO 15 zero-based rules: floor 60, rounding method (half-up assumed), GA rounding for awards, SHS "equivalent units" GA | [S]; separate issuance pending | DepEd PDF / later memo | Configurable rounding and GA method |
| 6 | Hybrid scheme for SY 2026–27 legacy Grade 12: descriptors and period structure | [S] | DepEd / SDO clarification (Muntinlupa NUM-2026-286 unread) | Hybrid scheme as separate seed |
| 7 | DO 15 promotion: conditional promotion and back-subject wording vs SRC; INC rules; transferee conversion; LWD accommodations | [S] conflicting; gaps | DepEd PDF | PRM-01 flags |
| 8 | DO 15 report card template (SF9 successor name and layout); whether observed core values survive | Not found | DepEd annex | GRD-13 pending status |
| 9 | DO 15 award categories beyond Academic Excellence; year-end vs per term; conduct/perfect attendance survival | [S] names only | DepEd PDF | AwardDefinition data |
| 10 | DO 8 s.2015 and DO 36 s.2016 tables (weights, transmutation, honors) used for historical import | [K] not re-fetched | Official PDFs (URLs cited) | Seeds marked `prior_knowledge` |
| 11 | MATATAG Grade 10 rollout year (SY 2026–27 vs 2027–28); DO 10 s.2024 and its amendment number (DO 12 s.2024?); Grades 9–10 subject lists; full time-allotment table | [N]/[S] conflict | DepEd PDFs | Per-grade framework start |
| 12 | Strengthened SHS order number (DO 017 s.2026?) and DM 012 s.2026; full elective lists, Grade 12 subjects, Work Immersion hours, subjects per term, TESDA NC alignment; how SSHS maps to three terms vs LIS semesters | [S]; LIS semester facilities [P] | DepEd PDF; LIS Support | Curriculum and period structure as data |
| 13 | Curriculum for learners retained in legacy Grade 12 after SY 2026–27 | Not found | DepEd / SDO | Curriculum bound per enrollment |
| 14 | DO 009 s.2026 full text (a revised "r" version exists): holidays, INSET, private minimum class days, term-based grading for SHS; SY 2027–28 calendar | [N] | DepEd PDF | Calendar data |
| 15 | DO 017 s.2025 signed text and Annexes A (early registration), B (BEEF), C (confirmation slip) field lists; read through an OCR'd blog reproduction | [D] | DepEd PDF | Versioned form schemas |
| 16 | SY 2026–27 and SY 2027–28 enrollment week dates; LIS window dates each year | Unverified summaries; LIS dates move | DepEd memo; LIS Support | LISWindow data |
| 17 | LRN digit structure (meaning of the last four digits); DO 22 s.2012 text | [S] slide deck; 403 | DepEd / Division Planning Officer | Validate length and digits only |
| 18 | DM 023 s.2026 text (read via SDO reproduction) and DO 88 s.2010 section numbers for withholding (Sec. 128 vs 139–141) and the certificate of eligibility to transfer | [D]; [S] conflict | DepEd PDF; counsel | Hold rules configurable |
| 19 | DO 88 refund schedule (10%/20%/full), reservation-fee cap, fee-increase sections and notice period; any 2024–2026 revision of the Manual | [S] blends HEI rules | DepEd PDF; counsel; Regional Office | Refund policy table |
| 20 | DECS Order 63 s.1999 interest rule; school-level discount rules | [S] | DepEd text; counsel | Interest off by default |
| 21 | RA 11984 IRR: certificate validity, processing times, complaint window | [S] respicio | DSWD/DepEd IRR | Certificate type with configurable validity |
| 22 | SY 2026–27 / 2027–28 tuition-increase consultation and application deadlines | Issued yearly; none found | Regional Office / SDO | FEE-03 workflow dates as data |
| 23 | DO 11 s.2026 Tables 5 and 13 (ESC and voucher amounts), category mapping, ESC school eligibility, top-up ceilings, TSS mechanics | [S] single site matching old values | DepEd PDF; PEAC | Rate tables as data |
| 24 | DM 031 s.2026 billing and redemption timeline; the exact Muntinlupa memo URL flagged unconfirmed in the enrollment notes | [D] | PEAC Helpdesk; SDO | Deadline calendar data |
| 25 | DO 12 s.2026 Government Recognition requirements for SHS VP participation from SY 2027–28 | [D] | DepEd PDF | Recognition status field |
| 26 | New voucher law (Sept 2026): RA number, effectivity, any changes for JHS/SHS | [N] | Official Gazette | GrantProgram extensibility |
| 27 | DO 006 s.2026 full text, Annex I offense matrix, forms (Annexes F, H), role separation in due process; coverage of private schools | [S]/[N] | DepEd PDF | Offense catalogue as data |
| 28 | DO 5 s.2024: ancillary task list, overload formula (service credit vs pay), effectivity | [N] | DepEd PDF | LoadPolicy data |
| 29 | DM 048 s.2025 class-size targets and Annex A program of study; current JHS class-size standard | [S]; [N] 2018 | DepEd memo | Capacity as data |
| 30 | Five-consecutive-absence home-visit mandate; tardiness definitions; DM 14 s.2021 SF4 changes still in force | [P] column exists; mandate [S] | DepEd forms order | At-risk rules as data |
| 31 | DO 58 s.2017, DO 4 s.2014, DO 11 s.2018 primary texts; SF5–SF10 field lists; which forms LIS generates today; whether adding QR codes to official forms is allowed | [S]; 403 | DepEd PDFs; LIS Support | Template versions; WEB-11 |
| 32 | Certificate formats (good moral, enrollment, Grade 10 completion, SHS diploma annexes) | Not found | DepEd EOSY rites annexes | Templates as data |
| 33 | Records fees in public schools for certified copies | Not found | DepEd / SDO | Off in public mode |
| 34 | DO 007 s.2026 media rules (official page, editors); DO 49 s.2022 text | [S]/[N] | DepEd PDF | Advisory only in private mode |
| 35 | NPC: 2023-06 control wording, 2022-04 registration thresholds for a school, whether 16-03 is superseded, NPC AO 2025-017 detail on parental access, education-sector guidance; DepEd privacy manual and records disposition schedule (RA 9470) | [P] headlines; details not fetched | DPO / counsel / NPC | Exceed baseline; retention as data |
| 36 | Public-school website posting obligations (Transparency, procurement under RA 12009, MOOE/PTA) | [I]; GPPB circular predates RA 12009 | SDO / counsel | WEB-08 configurable |
| 37 | Canteen issuances and income rules; PTA fund custody (DO 13 s.2022); post-2023 no-collection reiteration; MOOE guidance revisions | Not verified | DepEd PDFs | PUB modules optional |
| 38 | Official DepEd identity provider (Google vs Microsoft 365) and learner-account provisioning API access | [N]/[S] conflict | Division ICT | Configurable IdP |
| 39 | Gateway rates other than PayMongo (Xendit, Maya, Dragonpay); education MDR discounts | [S] conflicting | Providers | Gateway adapter, fee pass-through config |
| 40 | NAT/A&E details (A&E passing score lowered to 60%; issuance numbers) | [S] | DepEd | External assessment data only |
| 41 | API reference conventions and Spatie features carried over from UMIS | [K, ref not fetched] | Engineering spike | Custom role_assignments regardless |

## Conclusion

The research shows that the hard part of SMIS is not the module list. Vendors already advertise SF1–SF10, grading sheets and parent portals at ₱95–₱130 per learner per month ([OceanEd](https://theoceaned.com/pricing); [Academe](https://academe.ph/)) [P]. The hard part is that the rules under those modules were rewritten by four major orders in twelve months (DO 017 s.2025 on enrollment, then DO 009, DO 011 and DO 015 s.2026 on calendar, subsidies and grading), and DepEd will keep amending them by memo. A product that stores DO 15's weights in code would already need a release for the SY 2027–28 no-transmutation switch and another for the next memo. The durable advantage is a rules store in which each value carries its issuance citation and verification status. Combine it with grades and money that are append-only and reproducible, and the next DepEd order becomes a configuration task with a regression suite rather than a migration. The same logic applies to the public/private split. The mode switch is mostly a set of hard guards (no fee may block a public-school learner; no balance may block an exam or rites anywhere) plus a few modules that only private schools switch on.

Two findings should shape Phase 1 planning beyond the build order. First, DepEd's own records obligations are now as much about speed as content. There are 30-day records transfers, 30-day private-school confirmations, 48-hour/10-day/30-day incident deadlines and EOSY dropout tags for unconfirmed transfers, so SLA timers and alerts are core features, not polish. Second, the evidence base is thinner than the confident tone of teacher portals suggests. Most 2026 numbers reached this research through DepEdClub, SchoolFinderPH or division reproductions. Planning should therefore treat the verification register as a sign-off gate for each module's design, budget a short verification sprint against the signed PDFs before seed data is frozen, and settle the e-invoicing question with the school's RDO before anything else.
