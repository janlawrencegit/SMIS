# Philippine Legal, Regulatory and Reporting Requirements for a University MIS (UMIS)

Scope: Philippine HEIs (SUCs, LUCs, private HEIs), as of November 2026. Research ran on 2026-11-21.

Source-confidence legend used below:
- **[V]**: verified this session from the primary or official text, or a reputable secondary source that was fetched or searched (URL given).
- **[S]**: a statute or issuance cited to its official or lawphil URL from established knowledge, but **not re-fetched this session**. The writer should treat these as high-likelihood but should re-verify exact section numbers before quoting them as law.
- Uncertain items are flagged **UNCERTAIN** or listed under Gaps.

---

## 1. CHED reporting and academic regulation (HEMIS, SO, permits/recognition, PSGs, calendar, handbook, MORPHE)

### Takeaway
CHED runs an annual HEMIS data collection through its Regional Offices, usually in Q4. Private HEIs and LUCs file 4 forms: A (institutional profile), BC (programs, enrollment, graduates), E5 (faculty/personnel) and a Graduate List. SUCs file 7 forms. A UMIS therefore needs per-program, per-term enrollment and graduate data plus faculty data that it can export straight into the CHED templates. Private HEIs also need workflows for Special Orders (SO) for graduates, program permit/recognition tracking, and curricula compliant with the PSGs. RA 10931 additionally *requires* SUCs/LUCs to run a student information system that follows CHED guidelines.

### Cited Findings
**HEMIS / data collection**
- [V] HEMIS is CHED's central platform for student enrollment, graduates, program offerings and institutional profiles. CHED's mandate is to "collect, collate, store, and disseminate data". — [CHEDRO I, 2024 HEMIS orientation](https://region1.ched.gov.ph/chedro-spearheads-2024-hemis-orientation/)
- [V] Private HEIs and LUCs submit **four HEMIS forms (A, BC, E5 and a Graduate List)**; SUCs submit **seven HEMIS forms**. The RO I orientation was on 8 Nov 2024 and tied to a CHED Memorandum Order No. 45 (the series year was cut off in the source: **UNCERTAIN**). — [CHEDRO I](https://region1.ched.gov.ph/chedro-spearheads-2024-hemis-orientation/)
- [V] SY 2024-2025 HEMIS annual data collection orientation, CHED RO XI: about 150 HEI registrars, records officers and HEMIS coordinators attended. HEMIS is therefore a registrar-owned annual cycle. — [CHED RO XI](https://ro11.ched.gov.ph/2024/10/25/online-orientation-for-the-annual-data-collection-of-hemis-for-sy-2024-2025/9581/uncategorized/)
- [V] Earlier cycles were titled "Higher Education Data Collection and Quick Survey on Enrollment, Graduates and HEI Personnel" (AY 2020-2021). This confirms the three core datasets: enrollment, graduates and personnel. — [CHEDRO III Memo 2020-100](https://chedro3.ched.gov.ph/wp-content/uploads/2020/12/CHEDRO3-MEMO-2020-100-AY-2020-2021-HIGHER-EDUCATION-DATA-COLLECTION-AND-QUICK-SURVEY-ON-ENROLLMENT-GRADUATES-AND-HEI-PERSONNEL.pdf); [CHED Region 2 RM 330 s.2022 (regional HEMIS rollout)](https://chedregion2.com/wp-content/uploads/series-of-2022-Regional-Memorandum-No-330.pdf)
- [V] RA 10931 IRR Sec. 38(a): SUCs/LUCs must "(1) establish a student information system, in accordance with the guidelines to be developed by the CHED, to facilitate the tracking of students; (2) submit relevant information, as determined by CHED, on school quality and performance". Compliance is a criterion in CHED's budget endorsement. — [RA 10931 IRR, UniFAST](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf)

**Special Orders (SO), permits, recognition, PSGs**
- [V] The SO is a CHED-issued authority that private (non-autonomous) HEI graduates need. CHED RO XI issued "Enhanced Guidelines on the Application, Processing, and Issuance of Special Order" effective 1st sem SY 2022-2023. Approved SO applications are returned to the HEI for safekeeping, so the UMIS must store SO numbers and scans. — [CHED RO XI RM 030 s.2022](https://ro11.ched.gov.ph/wp-content/uploads/2022/10/RM-NO.-030-S.-2022.pdf)
- [V] One HEI memo (2024) consolidates "Omnibus Guidelines on Special Order Applications, Undergraduate Curriculum Proposal and Curriculum Revisions" and requires notarized application forms. SO workflows are linked to the approved curriculum. — [SPC memo 003 s.2024](https://www.spc.edu.ph/wp-content/uploads/2024/01/memo-from-dir-iv-no-003-s-2024-omnibus-guidelines-special-order-applications-undergraduate-curriculum-proposal.pdf)
- [V] When a program/campus is closed, CHED may allow students to finish, "shall be issued a special order subject to the evaluation CHEDRO". The UMIS therefore needs to flag a program's permit status and its effect on graduates. — [CHED notice on AMA Legazpi/Naga](https://legacy.ched.gov.ph/notice-to-the-public-concerning-the-status-of-program-offerings-of-ama-computer-college-legazpi-and-naga-campuses/)
- [V] Autonomous/deregulated private HEIs are listed by CMO (CMO No. 2 s.2025 updated the list; CMO No. 15 s.2025 covers autonomy/deregulation guidelines). Autonomous HEIs are generally exempt from SO issuance, so the UMIS needs a configurable flag for "institution status: regulated / deregulated / autonomous". — [CHED 2025 CMOs listing via search](https://legacy.ched.gov.ph/2025-ched-memorandum-orders/); [Galera, CHED Updates](https://ucsra.uphsl.edu.ph/assets/resources/36th/Dr.%20Rogelio%20T.%20Galera%20-%20CHED%20Updates.pdf) (the SO exemption for autonomous HEIs comes from established practice: **verify**)
- [V] CMO No. 1 s.2025 sets Guidelines for Micro-Credential Development, Approval and Recognition in Higher Education. The UMIS must support non-degree micro-credential records and certificates. — [CHED 2025 CMOs](https://legacy.ched.gov.ph/2025-ched-memorandum-orders/)
- [V] CMO No. 10 s.2025 revises the policies for Centers of Excellence/Development (COE/COD). This is an institutional status attribute per program. — [CHED 2025 CMOs](https://legacy.ched.gov.ph/2025-ched-memorandum-orders/)
- [V] The DFA (via CHED) advises that the status of HEIs and programs (permit/recognition) can be verified with CHED. Program authority numbers therefore have to be traceable. — [DFA/CHED memo on verification of HEI status, 14 Jun 2023](https://dohape.dfa.gov.ph/newsroom/advisories/808-ched-memorandum-on-the-verification-of-the-status-of-higher-education-institutions.html)
- [S] MORPHE 2008 (CMO 40 s.2008) governs private HEIs. It covers Government Permit (GP) then Government Recognition (GR) per program; school records (permanent record/TOR, enrollment lists, promotional reports/grade sheets submitted to CHED); the maximum class size and faculty qualifications; student admission, retention and transfer credentials; issuance of TOR/diploma; and tuition fee increases. — [CMO 40 s.2008 (Ateneo KM page)](https://sites.google.com/ateneo.edu/jsp-km-initiative/policies-processes/ched)
- [S] CHED's program PSGs (one CMO per discipline, mostly 2017 outcomes-based PSGs) prescribe the minimum curriculum (course codes, units, prerequisites), faculty qualifications (generally a master's degree in the field), and OJT/practicum hours. The UMIS curriculum module must version curricula against the PSG CMO number. — [CHED issuances index](https://legacy.ched.gov.ph/issuances/)

**Academic calendar**
- [V] 2019 CHED memo: SUCs/LUCs were "enjoined" to open in August, later clarified as a recommendation. BOR approval is required, and private HEIs were not covered at first. Most HEIs moved to August openings by 2020. — [GMA](https://www.gmanetwork.com/news/news/nation/691227/shifting-start-of-academic-year-to-august-only-a-recommendation-says-ched/story); [Manila Bulletin 2020](https://mb.com.ph/2020/05/11/private-universities-and-colleges-should-start-this-august-ched)
- [V] June 2025: CHED RO XI consulted HEIs on a "proposed adjustment of Academic Year 2025-2026" (calendar realignment, linked to DepEd's return to a June-March SY). The final memorandum text was not found (**UNCERTAIN**). — [CHED RO XI](https://ro11.ched.gov.ph/2025/06/23/ched-ro-xi-holds-online-consultation-with-davao-region-heis-on-the-adjustment-of-ay-2025-2026/10863/news-and-activities/technical-assistance-to-heis/)
- [V] CHED requires approval for a change in delivery mode. It probed Cebu Normal University (Aug 2025) over an unapproved shift to fully online classes. Separately, CHED permitted a shift to 100% online classes amid an oil crisis. The UMIS should record each section's delivery mode and the CHED authority for it. — [Manila Bulletin](https://mb.com.ph/2025/08/05/ched-probes-cebu-normal-university-over-unapproved-shift-to-fully-online-classes); [GMA](https://www.gmanetwork.com/news/topstories/nation/983161/ched-permits-shift-to-100-online-classes-amid-oil-crisis/story)

### Inferences
- Configurable calendars per campus are needed: semester/trimester/term, start month and the opening date reported to CHED. Hard-coding June or August will break.
- Core HEMIS-ready data model: institution (CHED UII/institution code, campus, type, autonomy status); program (CHED program code, major, PSG CMO ref, GP/GR number and date, COE/COD, accreditation level); enrollment per program/year level/sex per term; graduates list (name, sex, program, date of graduation, SO number for private HEIs); faculty (sex, highest degree, rank, employment status, full/part-time, teaching load, discipline).
- Graduation clearance should block issuance of the diploma/TOR "graduated" annotation for regulated private HEIs until the SO number is recorded.

### Gaps
- The exact current HEMIS form column specs and file formats (Excel templates, portal) were not retrieved. Collect the templates from the CHED Regional Office.
- The number and series year of the governing HEMIS CMO (No. 45, year unknown) is unconfirmed.
- I found no central (national) 2024-2026 CMO consolidating SO requirements. Rules appear to be regional.
- No current CHED student handbook CMO was retrieved. MORPHE requires a student handbook, and the RA 10931 IRR lists "handbook fees" as a covered fee, so a handbook exists by regulation. Its mandated content (e.g., anti-hazing, Safe Spaces, DPA notices) is inferred, not verified.
- The 2025 CHED memo on the AY 2025-2026 calendar adjustment was not retrieved.
- Grading rules: no CHED-wide uniform grading scale was found. The 1.0-5.0 scale is conventional, and institutions set their own policies (**UNCERTAIN**).

---

## 2. RA 10931 (UAQTEA) and UniFAST: Free Higher Education, TES, SLP, Tulong Dunong

### Takeaway
RA 10931 sets hard data and reporting duties. Within **5 working days after the last day of registration each semester**, SUCs/LUCs must report entrance-exam takers and results, the list of Free HE beneficiaries with course/units/semesters remaining, opt-out payments and voluntary contributions. The UMIS must compute eligibility (no prior bachelor's degree, the maximum residency rule, the retention policy), handle notarized opt-out and voluntary-contribution forms, and produce TES billing statements (per-grantee annexes, signed by the president or head of the HEI, print and electronic) for private HEIs.

### Cited Findings
**Free Higher Education (SUCs/LUCs)**: all from [RA 10931 IRR](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf) [V]
- Sec. 5: only LUCs recognized by CHED on or before the annual cut-off are eligible.
- Sec. 6 ineligible: (a) already holds a bachelor's or comparable degree; (b) fails admission/retention policies that lead to permanent disqualification; (c) fails to finish within **one year after the prescribed program period**. For shiftees, semesters already availed are subtracted. For transferees, semesters with any government-funded StuFAP are subtracted. LOA/returnees are handled case by case, and the SUC/LUC decides extensions. (d) opted out.
- Sec. 4: SUCs/LUCs must implement a **Return Service System** for Free HE beneficiaries, approved by the BOR and CHED.
- Sec. 7 benefits: free tuition for all curricular subjects, including approved petitioned classes but excluding tutorial or review classes. Free "other school fees", with a fixed list of 13: library, computer, laboratory, school ID, athletic, admission, development, guidance, handbook, entrance, registration, medical/dental, cultural. Only the **first copy** of the ID, library ID and handbook is free. Affirmative action programs are required for IPs (Lumads), Muslims, PWDs, public school graduates and students from depressed areas.
- Sec. 8 opt-out: the decision is made during enrollment, per semester, and is irrevocable for that term. The student pays the assessed tuition and fees based on UniFAST composite fees. The waiver is a pro-forma notarized by the institution and contains: an awareness statement and reason, the academic period, the student's signature (plus the parent/guardian's if a minor), and **registrar and/or guidance counselor certification**. Opt-outs are exempt from the civic (return-service) obligation that term.
- Sec. 9 voluntary contribution: the same pattern, plus the amount. It is irrevocable for the term.
- **Sec. 11 Reporting**: submitted to CHED within **5 working days after the last day of registration** each semester: (a) entrance exam takers and pass/fail; (b) Free HE availees with details "(e.g., courses enrolled, number of units enrolled, number of semesters left in the Free HE benefit, etc.)"; (c) opt-out payments; (d) voluntary contributions. These accrue as SUC/LUC income.
- Sec. 38: a year-end report to CHED on the use of funds generated from Free Tuition/OSF. A 10-year development plan goes to CHED and the JCOC. Opt-out and contribution payments are also reported.

**TES**: [RA 10931 IRR](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf) [V]
- Sec. 22: TES covers first undergraduate programs in SUCs, LUCs and private HEIs that are in the UniFAST **Registry** (Sec. 42: a registry of quality-assured programs and institutions published by UniFAST/CHED).
- Sec. 24: TES-1 (tuition/OSF, private HEIs only, pegged to the nearest SUC); TES-2 (education-related expenses, room and board); TES-3 (PWD-related expenses and the one-time first professional licensure cost). The grant is per full academic year, renewed yearly.
- Sec. 25 priority: (a) students in the latest DSWD **Listahanan**; (b) others ranked by per-capita income from proof-of-income documents. The UMIS must capture a Listahanan/4Ps household ID and family income.
- Sec. 28 ineligible: failed admission/retention, **exceeded the Maximum Residency Rule**, or program/HEI not in the Registry.
- Sec. 45: HEIs must provide a special enrollment procedure for TES grantees.
- [V] Billing mechanics (2022 TES guidelines, CHED RO2): CHEDRO certifies the list of applicants per HEI (Annex 2). HEIs submit billing statements on prescribed forms: **Annex 5 for continuing grantees, Annex 7 for new grantees**. The Annex 5 student information doubles as **proof of enrollment** for validation and billing. — [CHED RO2 RM 062 s.2022](https://chedregion2.com/wp-content/uploads/series-of-2022-Regional-Memorandum-No-062.pdf)
- [V] HEI duties include "Prepare TES billings. TES Billing Details approved by the president/head of the private HEI (print-out and electronic copy)". 2023 example: a billing/disbursement window of 21 Sept to 31 Oct 2023, with new **TES Form 1 and 2** plus a **notarized registrar's certification** for the 2nd semester. — [CHED RO2 RM 226/228 s.2023](https://chedregion2.com/wp-content/uploads/series-of-2023-RM-No.-226.pdf); [RM 228](https://chedregion2.com/wp-content/uploads/series-of-2023-RM-No.-228.pdf)
- [V] TES public overview — [QC LGU TES PDF](https://quezoncity.gov.ph/wp-content/uploads/2024/03/2.-CHED-%E2%80%93-UNIFAST-Tertiary-Education-Subsidy-TES.pdf)

**SLP**: [RA 10931 IRR](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf) [V]
- Sec. 33: borrower requirements include admission/retention compliance, a **TIN and SSS number**, financial counseling, and a guarantor (parent/guardian) for short-term loans.
- Sec. 34: loan proceeds for tuition/OSF are **paid directly to the HEI**. The UMIS needs a receivable or third-party payer type "UniFAST SLP".
- Sec. 36: UniFAST tracks borrowers via BIR/SSS/GSIS/etc. The HEI may be asked for enrollment and graduation status.
- Sec. 44, 46: students can hold TES and SLP together and keep DOST/CHED merit scholarships, subject to UniFAST harmonization. The UMIS must support stacking multiple StuFAPs per student per term.

### Inferences
- A "sponsor/StuFAP" ledger is needed per student-term: Free HE, TES-1/2/3, SLP, Tulong Dunong, CHED merit, DOST, LGU and private scholarships. Each needs eligibility status, amount and billing batch.
- Residency counters are needed: semesters availed of Free HE or StuFAP, the expected program duration, and the remaining Free HE semesters (directly required by the Sec. 11(b) report).
- Generated forms: a notarizable opt-out waiver, a voluntary contribution form, a registrar's certification, TES billing annexes (exported as XLSX/PDF) and the 5-day post-registration CHED report.

### Gaps
- Current (2024-2026) UniFAST Memorandum Circulars on TES billing templates, TES amounts (historically about PHP 40,000/AY for private HEIs and PHP 20,000 for SUCs/LUCs: **unverified**), and the Free HE billing template (the "Form 1/Form 2" or "Annex" formats) were not retrieved.
- **Tulong Dunong Program (TDP)**: no source retrieved this session. It is known to be a CHED/UniFAST grant (about PHP 7,500 per semester) billed by HEIs using grantee lists (**unverified**).
- Whether UniFAST now uses an online billing portal (e.g., "UniFAST billing system" or the "UniFAST Student Information System") is **unverified**.

---

## 3. Data Privacy Act of 2012 (RA 10173), IRR and NPC circulars

### Takeaway
A university is a personal information controller (PIC) that processes sensitive personal information: grades, health, religion, government IDs, and minors' data. In practice it meets the NPC Circular 2022-04 mandatory-registration thresholds (250 or more employees, or sensitive data of 1,000 or more individuals), so it must register its DPO and data processing systems via NPCRS. The UMIS must implement lawful-basis tagging, privacy notices, data-subject-rights workflows, access controls/audit logs/encryption, breach handling within 72 hours, and retention/disposal schedules. The NPC education-sector guidance stresses institutional accountability even where consent was obtained.

### Cited Findings
- [V] **NPC Circular 2022-04** (Registration of DPOs and DPS): effective **11 Jan 2023**, with a compliance deadline of **10 July 2023**. Mandatory registration applies to a PIC/PIP that employs **250 or more persons** or processes **sensitive personal information of 1,000 or more individuals**, or carries out automated decision-making/profiling. Others may register voluntarily or file a notarized sworn declaration (Annex 1). Filing is only through **NPCRS**, and only **one DPO** may be registered per organization. — [Circular 2022-04 PDF](https://privacy.gov.ph/wp-content/uploads/2023/05/Circular-2022-04.pdf); [Baker McKenzie](https://insightplus.bakermckenzie.com/bm/data-technology/philippines-new-npc-circular-on-registration-of-data-protection-officers-and-data-processing-systems-takes-effect_1); [NPC reminder](https://privacy.gov.ph/?p=43514). The two sources word the threshold differently: one NPC summary says "1,000 or more customers", while the Circular's Sec. 5 refers to sensitive personal information of 1,000 or more. Verify against the Circular text.
- [V] NPC encouraged school DPOs to adopt **online learning guidelines** after a surge in school data breaches (hacked portals/databases, phishing, stolen laptops, system glitches, human error). It advised limited use of tools the school has not officially adopted. The NPC-backed Data Privacy Council Education Sector states schools "are accountable for all personal data it collects and processes, even if they properly obtained the consent of students". — [NPC](https://privacy.gov.ph/?p=11880); [Inquirer](https://newsinfo.inquirer.net/1336881/respect-kids-privacy-amid-online-learning-council-urges)
- [S] RA 10173: Sec. 3(l) defines sensitive personal information to include education, health, government-issued IDs, religion and ethnic origin. Sec. 12 and 13 set the lawful criteria (consent, contract, legal obligation, vital interest, public authority, legitimate interest; and for sensitive data, consent/law/regulation/medical/legal claims). Sec. 16 lists data subject rights: to be informed, access, object, erasure/blocking, rectification, damages, and Sec. 18 portability. Sec. 20 requires organizational, physical and technical security measures. Sec. 21 sets accountability for outsourcing and cross-border transfers. Sec. 25-37 set penalties. — [RA 10173, lawphil](https://lawphil.net/statutes/repacts/ra2012/ra_10173_2012.html)
- [S] NPC Circular 16-03 (Personal Data Breach Management): notify the NPC and affected data subjects **within 72 hours** of knowledge of a breach involving sensitive personal information (or information usable for identity fraud) that is likely to cause real risk of serious harm. Keep a breach incident log and submit an annual breach report summary. — [NPC Circular 16-03](https://privacy.gov.ph/memorandum-circulars/npc-circular-16-03-personal-data-breach-management/). (**Note**: NPC issued an updated breach circular, NPC Circular 2025-?, reported in 2025. **UNCERTAIN; verify**.)
- [S] NPC Circular 16-01 (Security of Personal Data in Government Agencies) applies to SUCs/LUCs as government bodies: encryption at rest and in transit (AES-256 is recommended), access by authorized personnel only, audit trails, no storage of personal data on personal devices without authorization, and data centres/cloud subject to agreements. — [NPC Circular 16-01](https://privacy.gov.ph/memorandum-circulars/npc-circular-16-01-security-of-personal-data-in-government-agencies/)
- [S] IRR of RA 10173 (2016): Sec. 19 sets the general data privacy principles; Sec. 26 designates the DPO; Sec. 29 sets the security measures; Sec. 34 lists rights; Sec. 44-45 set data sharing agreements. NPC Circular 2020-03 governs **Data Sharing Agreements** (relevant to sharing with CHED/UniFAST/DSWD/LGU sponsors and SLP partners). — [DPA IRR](https://privacy.gov.ph/implementing-rules-regulations-data-privacy-act-2012/); [NPC Circular 2020-03](https://privacy.gov.ph/memorandum-circulars/npc-circular-no-2020-03-data-sharing-agreements/)
- [S] NPC Circular 2023-04 (Guidelines on Consent) requires consent to be freely given, specific, informed, and evidenced by written, electronic or recorded means, and it covers consent from parents/guardians of minors. NPC Circular 2023-06 covers security of personal data in government and the private sector (consolidating security measures). — [privacy.gov.ph circulars](https://privacy.gov.ph/memorandum-circulars/). **Verify numbers.**

### Inferences
- UMIS controls: a privacy notice at every collection point (admission, enrollment, scholarship application) with versioned acceptance; field-level classification (PI / SPI); role-based and attribute-based access; an immutable audit log of reads of SPI (grades, health, disciplinary, guidance notes); encryption; a DSAR (data subject access request) workflow with SLA tracking; a breach register with a 72-hour timer and NPC report template; retention schedules per record class; and a disposal log.
- Parental access: most college students are adults (18 or older), so disclosure of grades or records to parents needs a lawful basis such as student consent or a waiver. Minors (e.g., SHS learners and some first-years) require parent/guardian consent. Model a "guardian access consent" flag per student.
- DSAs and outsourcing agreements must be tracked for each external data recipient: CHED HEMIS, UniFAST, DSWD, PRC, banks/SLP partners, LMS/cloud vendors.

### Gaps
- No NPC advisory specific to parental access to college student records was found. Treat the parental access rule as an inference.
- Whether a 2025/2026 NPC circular superseded Circular 16-03 on breach management was not confirmed.
- NPC advisories on school CCTV and ID photos/yearbooks (e.g., NPC Advisory Opinions on graduation lists and posting of grades) were not retrieved. Posting grades or names of passers with full names has been addressed in NPC advisory opinions (**unverified**).

---

## 4. Academic records and credentials (TOR, diploma, certifications, transfer credentials, CAV, apostille, retention)

### Takeaway
The registrar must issue the TOR, diploma, certificate of graduation, honorable dismissal/transfer credential and certifications, and must support CHED CAV and DFA apostille chains: school certification, then CHED CAV, then DFA apostille. Certified true copies signed by the registrar, plus a registrar's indorsement, are required. Since July 2025, a regional e-CAV channel applies in at least one CHED Regional Office (CHEDRO IV-A). Academic permanent records are retained permanently by long-standing practice under MORPHE, and the RA 10931 IRR's student tracking duty reinforces this.

### Cited Findings
- [V] CAV sequence: the school certifies, then CHED issues the CAV, then the DFA apostilles the CAV. Required documents are a certified true copy of the TOR and diploma/certificate of graduation signed by the current HEI registrar. The DFA apostille, not the "Red Ribbon", is now required. — [DLSU CAV](https://www.dlsu.edu.ph/wp-content/uploads/pdf/registrar/cav.pdf); [DLSU CHED CAV procedures](https://www.dlsu.edu.ph/wp-content/uploads/pdf/registrar/ched-cav-requests-procedures.pdf); [Australian Embassy, "The CAV Process"](https://philippines.embassy.gov.au/files/mnla/The%20CAV%20Process.pdf)
- [V] CHEDRO Citizen's Charter lists an "indorsement from HEI Registrar" among the CAV checklist items. — [CHEDRO NCR Citizen's Charter](https://chedro-ncr.com/assets/attachments/CHEDRO-Citizens-Charter-converted.pdf); [CHEDRO III undergraduate CAV form](https://chedro3.ched.gov.ph/wp-content/uploads/2020/09/Undergraduate-CAV-form.pdf)
- [V] DLSU example timelines and fees: CHED authentication takes 15 working days (PHP 1,550); CHED plus DFA apostille takes 26 working days (PHP 1,950), or 18 days express (PHP 2,150). — [DLSU](https://www.dlsu.edu.ph/wp-content/uploads/pdf/registrar/cav.pdf)
- [V] **CHED-RO Memorandum No. 40 s.2025 (e-CAV)**: from **1 July 2025**, all requests for academic documents requiring CHED endorsement or authentication go through the new e-CAV channel (reported by a CHEDRO IV-A school). — [Southville](https://www.southville.edu.ph/ched-ro-memorandum-no-40-series-of-2025/)
- [V] DFA apostille documentary requirements for school records — [DFA consular](https://consular.dfa.gov.ph/requirements-of-documents); [apostille.gov.ph](https://www.apostille.gov.ph/?p=347)
- [S] MORPHE 2008 (CMO 40) records provisions: the HEI keeps a permanent record per student (TOR data), registration lists and grade sheets. A TOR is issued only upon clearance. Transfer credentials (honorable dismissal / certificate of transfer eligibility) are issued on request. Records of closed HEIs are turned over to CHED. — [CMO 40 s.2008 reference](https://sites.google.com/ateneo.edu/jsp-km-initiative/policies-processes/ched)

### Inferences
- Credential documents to generate: TOR (with "Remarks: Graduated with the degree of X on date; SO No. ___ s. ___" for private regulated HEIs), diploma, certificate of graduation, certificate of enrollment, GWA/units earned certification, good moral, honorable dismissal/transfer credential, CAV packet (CTC plus registrar indorsement), and certified true copies. Each needs anti-tampering features (serial number, QR verification, dry-seal placeholder, registrar e-signature) and an issuance log.
- Admission of freshmen and transferees must capture incoming credentials: SHS Form 138 (report card) and SF10 (Form 137 equivalent) from DepEd, or TOR/honorable dismissal from the prior HEI.
- Retention: academic permanent records should be kept permanently. Financial and enrollment support docs should follow COA/BIR periods (see section 5). Disposal of records in SUCs follows National Archives (RA 9470) schedules **[S, unverified this session]**.

### Gaps
- No primary CHED text on retention periods was retrieved. "Permanent retention of academic records" is established practice and is **not cited from a primary source** here.
- National e-CAV rollout status beyond CHEDRO IV-A is unconfirmed.

---

## 5. Finance and tax (BIR invoices, CAS, e-invoicing/EIS, EOPT RA 11976, tuition increase consultation)

### Takeaway
Under the EOPT Act (RA 11976, effective January 2024), the "invoice" replaces the official receipt as the primary sales document. Schools that use a computerized accounting/billing system must register it with the BIR (CAS/CBA, via a Permit to Use / ATP rules). Under RR 11-2025 as amended by RR 26-2025 and RMC 98-2026, **all covered taxpayers except micro taxpayers must issue structured e-invoices and report sales to the EIS on or before 31 Dec 2026**, with an EIS Certification due within 6 months of the PTI. A private university's cashiering module must therefore be EIS-capable now. Whether proprietary non-stock educational institutions or SUCs are carved out was **not found**.

### Cited Findings
- [V] **RR 11-2025** implements Sec. 237/237-A NIRC as amended by **CREATE MORE (RA 12066)**: mandatory e-invoicing and electronic sales reporting. It was signed 26 Feb 2025 and took effect around 14 Mar 2025. Group 1 includes large taxpayers, e-commerce businesses and **CAS/CBA users**, plus Commissioner designees. Micro taxpayers are excluded. — [PwC](https://www.pwc.com/ph/en/tax/tax-publications/taxwise-or-otherwise/2025/paperles-invoicing-and-sales-reporting.html); [Grant Thornton](https://www.grantthornton.com.ph/insights/articles-and-updates1/tax-notes/create-more-mandatory-use-of-electronic-invoicing-and-electronic-sales-reporting-with-allowable-deduction/); [KPMG US](https://kpmg.com/us/en/taxnewsflash/news/2025/03/philippines-expansion-e-invoicing-mandate.html)
- [V] **RR 26-2025** (16 Oct 2025) extended the e-invoicing compliance deadline to **31 Dec 2026**. One source says 1 Jan 2027 (conflict). — [PwC Tax Alert 29](https://www.pwc.com/ph/en/tax/tax-publications/tax-alerts/2025/tax-alert-29.html); [Tribune, Sept 2026](https://tribune.net.ph/2026/09/23/bir-sets-31-december-e-invoicing-deadline)
- [V] **RMC 98-2026** (22 Sept 2026): all covered taxpayers except Micro comply on or before 31 Dec 2026. They must secure a **PTI Electronic Invoice** first, then an **EIS Certification within 6 months**. Invoices printed from CAS/POS are **not** e-invoices unless the system issues and transmits electronically and reports sales to the BIR. Corrections are made by a **credit note** (decrease) or a new e-invoice (increase), never by editing. Manual invoices are the fallback during downtime. The PTI covers the HO and branches. Printed copies may be given in B2C. A BIR advisory of 14 Sept 2026 states that no e-invoicing service provider (ESP) is BIR-accredited yet. — [KPMG PH Special InTax Sept 2026](https://kpmg.com/ph/en/insights/2026/09/special-intax-september-2026-issue-1-volume-2.html)
- [S] **RA 11976 EOPT Act** (effective 22 Jan 2024) and **RR 7-2024**: the sales invoice replaces the OR as the primary document for sales of goods and services. ORs become supplementary. Existing ORs may be used, stamped "Invoice", until exhausted. Taxpayers are classified as micro/small/medium/large (RR 8-2024). Taxpayers can file and pay anywhere. — [RA 11976, lawphil](https://lawphil.net/statutes/repacts/ra2024/ra_11976_2024.html); [BIR RR 7-2024](https://www.bir.gov.ph/)
- [S] CAS/CBA: computerized accounting/invoicing systems require BIR registration/acknowledgment (RR 9-2009; RMO 29-2002; RR 9-2021 lists required invoice fields, the system-generated serial numbering, audit trail and electronic archiving; books are kept 5 years in the system under RR 17-2013 / NIRC Sec. 235). — [BIR](https://www.bir.gov.ph/)
- [S] Tax treatment of schools: non-stock, non-profit educational institutions are exempt under 1987 Constitution Art. XIV Sec. 4(3). Proprietary educational institutions pay a 10% preferential income tax rate (1% from Jul 2020 to Jun 2023 under CREATE). Educational services by accredited private institutions and government schools are **VAT-exempt** (NIRC Sec. 109(1)(H)). Being VAT-exempt does not remove the duty to invoice. — [NIRC, lawphil](https://lawphil.net/statutes/repacts/ra1997/ra_8424_1997.html)
- [S] Tuition fee increases (private HEIs): CHED requires consultation with students, parents, faculty and staff, plus a written notice. The allocation of incremental proceeds follows **RA 6728 Sec. 5(2)**: **70%** to salaries/wages/benefits of teaching and non-teaching personnel, **20%** to facilities/improvements, and up to **10%** to returns. Applications go to the CHEDRO under CMO 3 s.2012 (Policies on Tuition and Other School Fees, as amended). — [RA 6728, lawphil](https://lawphil.net/statutes/repacts/ra1989/ra_6728_1989.html). **Verify the current CMO number and deadlines.**
- [S] SUCs are government entities: they use COA-prescribed Official Receipts (Accountable Form 51) and the Government Accounting Manual, and are subject to COA audit. — [COA](https://www.coa.gov.ph/)

### Inferences
- The cashier/billing module needs: BIR-registered serial numbering per branch/campus; the required invoice fields (seller TIN and branch code, registered name/address, "VAT-exempt" labelling, buyer name/TIN, item description, amounts); credit/debit notes instead of voids; structured JSON output to the EIS with retry/queue; downtime fallback to manual booklets with later encoding; and 10-year retention of e-records (NIRC Sec. 235 as amended by EOPT reduced it to 5 years: **verify**).
- Third-party payers (UniFAST TES, SLP, CHED, LGU scholarships) require invoices/receivables per sponsor.
- A tuition increase workflow is needed: proposal, then consultation minutes and attendance, then CHEDRO submission, then a 70/20/10 allocation report.

### Gaps
- No source confirmed how e-invoicing applies to schools specifically (VAT-exempt educational services), or to SUCs/LUCs (government, COA ORs).
- The current CHED tuition-and-fees CMO (number, consultation timing, deadline for application, e.g., before the end of the AY) was not retrieved.
- Required e-invoice field list and EIS JSON schema were not retrieved.

---

## 6. Accreditation (AACCUP, PAASCU, PACUCOA, ISO 21001, COPA/FAAP)

### Takeaway
Accreditation is voluntary but carries regulatory weight. CHED's autonomy/deregulation criteria (CMO 15 s.2025) and the COE/COD criteria (CMO 10 s.2025) rely on accreditation levels. SUC accreditation is through AACCUP, and private HEIs use PAASCU, PACUCOA or ACSCU-AAI under FAAP. The UMIS should produce evidence: enrollment and graduation trends, faculty profile (degrees, ranks, research), licensure exam performance, graduate tracer studies, student services usage, library holdings and outcomes-based assessment.

### Cited Findings
- [V] CMO 10 s.2025 revised COE/COD policies. CMO 2 and CMO 15 s.2025 cover autonomous/deregulated status. These are statuses that reference accreditation and quality indicators. — [CHED 2025 CMOs](https://legacy.ched.gov.ph/2025-ched-memorandum-orders/)
- [V] RA 10931 IRR Sec. 38(d): SUC/LUC budget endorsement depends on CHED quality standards and quality indicators. — [IRR](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf)
- [S] AACCUP accredits SUC programs at Levels I-IV across areas: VMGO, faculty, curriculum and instruction, support to students, research, extension, library, physical plant, laboratories, and administration. PAASCU and PACUCOA use similar area-based surveys. ISO 21001:2018 (Educational Organizations Management Systems) requires documented learner satisfaction, curriculum design control, complaint handling and special-needs accommodation. — [AACCUP](https://www.aaccupqa.org.ph/); [PAASCU](https://paascu.org.ph/); [PACUCOA](https://www.pacucoa.ph/)

### Inferences
- An "evidence repository" with an area-mapped document store, KPIs per program (enrollment, retention/attrition, graduation rate, board passing rate against the national rate, employability via tracer), faculty qualification matrix, and student satisfaction surveys.

### Gaps
- Current AACCUP instrument versions (2024/2025 outcomes-based instrument) were not retrieved.

---

## 7. Other statutory regimes (Safe Spaces, anti-hazing, PWD, IP data, NSTP, board exams, SHS/LIS)

### Takeaway
Several statutes create case-management, roster and reporting duties: a Safe Spaces (RA 11313) committee with case handling; anti-hazing (RA 11053) registration of organizations, notices of initiation and monitoring; disaggregated data on PWDs and IPs (affirmative action under RA 10931 IRR Sec. 7); NSTP serial numbers (RA 9163) on the TOR; and DepEd LIS/SF reports if the university runs a Senior High School.

### Cited Findings
- [V] RA 10931 IRR Sec. 7 requires affirmative action programs for Lumads, Muslims, other IPs, PWDs, public school students and students from depressed areas. Sec. 23(d) TES-3 gives PWD students disability-related allowances. The UMIS must capture PWD status (and PWD ID) and IP affiliation as optional, consent-based SPI. — [IRR](https://unifast.gov.ph/assets/pdf/guidelines/IRR10931.pdf)
- [S] **RA 11313 Safe Spaces Act** (2019) and IRR: educational institutions must adopt anti-sexual-harassment policies, set up a Committee on Decorum and Investigation (CODI), act on complaints, protect confidentiality, and include provisions in the student handbook. CHED was mandated to issue implementing policies (CMO 1 s.2015 on gender and development predates it). — [RA 11313, lawphil](https://lawphil.net/statutes/repacts/ra2019/ra_11313_2019.html)
- [S] **RA 11053 Anti-Hazing Act** (2018): school organizations must register; initiation requires written notice to the school authorities **at least 7 days** before, with names of participants. The school must assign at least 2 representatives to attend, and the law imposes school liability. The school must keep a list of organizations, officers and members. — [RA 11053, lawphil](https://lawphil.net/statutes/repacts/ra2018/ra_11053_2018.html)
- [S] **RA 7277 Magna Carta for Disabled Persons** (as amended by RA 9442/RA 10754): non-discrimination in admission, assistance to PWD students, and the 20% PWD discount (RA 10754 covers goods/services, with tuition subject to rules: **verify**). — [RA 7277, lawphil](https://lawphil.net/statutes/repacts/ra1992/ra_7277_1992.html)
- [S] **RA 8371 IPRA**: IP data is sensitive (ethnic origin under DPA Sec. 3(l)). — [RA 8371](https://lawphil.net/statutes/repacts/ra1997/ra_8371_1997.html)
- [S] **RA 9163 NSTP Act** (2001): NSTP (ROTC/LTS/CWTS) is required of baccalaureate and 2-year technical-vocational students. Graduates are issued a **serial number** by CHED/TESDA/DND through the institution. The IRR requires HEIs to submit enrollment and graduate lists for NSTP. **RA 11929 / CMO** and the 2025 proposal to make ROTC mandatory were pending: **UNCERTAIN**. — [RA 9163, lawphil](https://lawphil.net/statutes/repacts/ra2002/ra_9163_2002.html)
- [S] **Board/licensure exams (PRC)**: applicants need a TOR with "for board examination purposes" remarks (and, for private regulated HEIs, the SO number). The PRC publishes performance of schools, which CHED uses in program monitoring (e.g., phase-out of low-performing nursing programs). — [PRC](https://www.prc.gov.ph/)
- [S] **SHS (DepEd)**: if the university runs an SHS, it must enroll learners in the DepEd **Learner Information System (LIS)** using the 12-digit LRN. It must maintain School Forms (SF1 register, SF2 attendance, SF5 promotion, SF9 report card/"Form 138", SF10 permanent record/"Form 137"), obtain Special Orders for Grade 12 completers in private schools, and process ESC/SHS Voucher Program billing (PEAC). — [DepEd DM s2025 093r (SO-related)](https://www.deped.gov.ph/wp-content/uploads/DM_s2025_093r.pdf); [DepEd](https://www.deped.gov.ph/)

### Inferences
- Modules: a CODI case management module (confidential, access-restricted, retention-controlled); a student organization registry with initiation notices and attendance; a PWD/IP self-identification module with consent; NSTP component, grade and serial number fields printed on the TOR; licensure applicant TOR issuance; and an SHS module with LRN, LIS sync/export and DepEd SF generation as a separate basic-ed track.

### Gaps
- The current CHED CMO operationalizing Safe Spaces in HEIs, the NSTP serial number issuance procedure and 2025-2026 changes, and the DepEd LIS data format were not verified this session. Only statutory baselines are cited, and those were not re-fetched.
- Whether mandatory ROTC legislation passed in 2025-2026 is **UNCERTAIN**.
