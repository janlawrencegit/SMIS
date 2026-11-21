# Operations and compliance requirements for a Philippine JHS-SHS school under DepEd (SY 2025-2026 to SY 2026-2027)

Scope note: these notes were compiled on 2026-11-21. Source tiers: (P) primary (deped.gov.ph, lawphil, Official Gazette); (N) news reporting of DepEd issuances; (S) secondary, meaning teacher blogs, slide decks and division/school memos repeating an order. Several key 2026 orders (DO 6, 7 and 9, s. 2026) were read only through news or blog summaries. Check them against the deped.gov.ph PDFs before coding hard rules. Items marked "[background, not re-verified]" come from the researcher's prior knowledge of the statute text and were not fetched this session.

## 1. School calendar (SY 2025-2026, SY 2026-2027, private school flexibility)

### Takeaway
SY 2025-2026 followed DO 12, s. 2025: June 16, 2025 to March 31, 2026, with 197 class days and the usual quarter structure. SY 2026-2027 changes the structure. DO 009, s. 2026 brings in a three-term calendar from June 8, 2026 to April 8, 2027, with 201 class days. Private schools may adopt the same calendar if they meet the required number of class days. The calendar module therefore has to model configurable terms, not hard-coded quarters.

### Cited Findings
- DO 12, s. 2025, "Multi-Year Implementing Guidelines on the School Calendar and Activities," is dated April 15, 2025 and signed by Sec. Sonny Angara. SY 2025-2026 runs June 16, 2025 to March 31, 2026, with 197 class days including end-of-school-year rites. It returns the calendar to the pre-pandemic June-March cycle. (N) — [Manila Bulletin](https://mb.com.ph/2025/4/18/deped-class-opening-sy-2025-2026-june-16); [Inquirer](https://newsinfo.inquirer.net/?p=2053997)
- Public-school enrollment for SY 2025-2026 ran June 9-13, 2025. (N) — [Manila Bulletin](https://mb.com.ph/2025/06/05/deped-sets-nationwide-public-school-enrollment-period-from-june-9-to-13)
- Private schools may also open SY 2025-2026 on June 16. (N) — [GMA](https://www.gmanetwork.com/news/topstories/nation/943361/private-schools-may-also-start-classes-on-june-16-deped/story); [Manila Bulletin](https://mb.com.ph/2025/4/21/private-schools-may-adopt-june-16)
- SY 2026-2027 opens June 8, 2026 and closes April 8, 2027, with 201 class days. The year has three terms, and each term has an opening block, an instructional period and end-of-term activities. (N) — [GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/); [GMA](https://www.gmanetwork.com/news/topstories/nation/984611/deped-classes-to-start-june-8-end-april-8-under-3-term-calendar/story/); [Manila Bulletin](https://mb.com.ph/2026/04/20/back-to-school-deped-sets-june-8-opening-of-classes-for-sy-20262027)
  - Term 1: opening block June 8-11, instruction June 15 to Sept 1, end-of-term activities Sept 2-15, 2026.
  - Term 2: instruction Sept 16 to Dec 4, end-of-term activities Dec 7-18, 2026.
  - Year-end break: after Dec 18, 2026 until Jan 4, 2027.
  - Term 3: instruction Jan 4 to Mar 23, 2027, final assessments and closing activities Mar 24 to Apr 8, 2027. — [GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/)
- The governing issuance is reported as DepEd Order No. 009, s. 2026, issued April 16, 2026, on implementing the three-term school calendar. The GMA article links a file named "DO_s2026_009r.pdf", which suggests a revised version exists. (N) — [Tribune](https://tribune.net.ph/2026/04/20/classes-to-start-on-8-june-under-new-three-term-calendar); [explained.ph](https://explained.ph/deped-issued-three-term-school-calendar-for-sy-2026-2027-under-new-reform-initiative/)
- Teachers follow a "budget of work" spread across each term. Remediation such as ARAL may run within or alongside instruction. Breaks between terms are for assessment, remediation and recovery. (N) — [GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/)
- Private schools, Philippine Schools Overseas and SUCs/LUCs offering basic education "may also adopt" the three-term calendar if they comply with the required number of class days. (N) — [GMA explainer](https://www.gmanetwork.com/news/topstories/nation/984622/explainer-deped-school-calendar-sy/story/); search summary of [Tribune](https://tribune.net.ph/2026/04/20/classes-to-start-on-8-june-under-new-three-term-calendar)
- One source error: Tribune gives the closing date as "8 April 2026" in one place. Every other source says April 8, 2027. — [Tribune](https://tribune.net.ph/2026/04/20/classes-to-start-on-8-june-under-new-three-term-calendar) vs [DZRH](https://www.dzrh.com.ph/post/deped-school-year-2026-2027-to-start-june-8-end-april-8)

### Inferences
- The calendar entity should hold: school year, a list of grading periods (N = 4 quarters for SY 2025-26, N = 3 terms for SY 2026-27), sub-blocks within each period (opening, instruction, end-of-term), breaks, holidays and suspensions (class-suspension days are frequent because of typhoons and heat), and a computed count of class days compared against the DepEd minimum.
- Grading, report-card (SF9) and attendance-summary periods should key off the configured periods, because SY 2026-27 uses terms.
- Private schools need their own opening and closing dates, plus a compliance check against the minimum class days.

### Gaps
- I did not read the full text of DO 009, s. 2026: holidays list, in-service training (INSET) dates, whether grading is per term, minimum class days for private schools, and whether SHS uses semesters or terms. The explainer did not say whether SHS keeps semesters.
- I did not verify the quarter dates and mid-year break of SY 2025-2026 (DO 12, s. 2025 annex).
- I did not confirm whether DO 12, s. 2025 ("multi-year") was amended or superseded by DO 9, s. 2026 for SY 2026-27.

## 2. Class programs, sectioning, time allotments, teacher workload

### Takeaway
Class programs for JHS follow DO 10, s. 2024 (MATATAG/Revised K-10), as amended by DO 12, s. 2024. Option A gives 45 minutes per learning area daily plus 45 minutes of Homeroom Guidance per week. Option B allows uniform 50, 55 or 60-minute periods, with Filipino at least 200 minutes a week and Homeroom at least 45 minutes a week. For SHS, DM 048, s. 2025 sets a class-size target of 40 learners, or 25 for laboratory and workshop electives. For public teachers, DO 5, s. 2024 sets 6 hours of actual teaching plus 2 hours of ancillary work, with overload compensation. DO 2, s. 2024 removed administrative tasks from teachers.

### Cited Findings
- DO 10, s. 2024 Key Stage 3 (Grades 7-10) time-allotment table: Filipino and English at 45 minutes, 5 times a week. The daily total is 390 minutes Monday to Thursday and 405 minutes on Friday. (S excerpt of P) — [Slideshare DOs 10 & 12 orientation](https://www.slideshare.net/slideshow/session1_guidelines-k-10-pptxusfuieeilestiyliuse/285559654); [DepEd MATATAG FAQs](https://deped.gov.ph/wp-content/uploads/FAQs-ON-THE-MATATAG-CURRICULUM.pdf)
- DO 12, s. 2024 amendment, implemented from Q2 of SY 2024-25. Option A keeps 45 minutes per learning area per day for 5 days, plus Homeroom Guidance at 45 minutes once a week. Option B uses uniform 50, 55 or 60-minute periods, with Filipino at least 200 minutes a week and Homeroom at least 45 minutes a week. (N) — [Inquirer](https://newsinfo.inquirer.net/1984864/deped-issues-new-guidelines-for-matatag-curriculum-implementation); [Manila Bulletin](https://mb.com.ph/2024/9/19/flexible-matatag-curriculum-guidelines-set-for-implementation-in-q2-of-sy-2024-2025-dep-ed)
- Special Program in Technical-Vocational Education (SPTVE) schools keep their existing curriculum and do not adopt MATATAG/DO 10, s. 2024 unless separately directed. This is from a May 2026 division memo. (S) — [DepEd Muntinlupa NUM 2026-190](https://deped-muntinlupa.com/wp-content/uploads/2026/05/NUM-2026-190.pdf)
- SHS under DM 048, s. 2025 ("strengthening senior high school"):
  - Class-size target is 40 for general classes and 25 for laboratory or workshop electives.
  - Schools that cannot comply may run larger classes, with quality safeguards (Sec. 32).
  - School heads prepare class programs that fit all required subjects, including Work Immersion.
  - A prototype program of study is in Annex A.
  - (S deck of P memo) — [Slideshare DM 048 s.2025](https://www.slideshare.net/slideshow/deped_memo_048_2025_strenthening-senior-high-schoolfinal-pptx/282577759)
- JHS class size: no current binding standard was found. 2018 DepEd planning parameters were 1:40 for Grades 5-10, against an earlier 1:45. (N, dated) — [PNA](https://www.pna.gov.ph/articles/1029281); [Manila Bulletin 2018](https://mb.com.ph/2018/03/20/deped-reaffirms-effort-to-achieve-ideal-class-size-teacher-student-ratio/)
- DO 5, s. 2024 rationalizes public school teachers' workload as a follow-up to DO 2, s. 2024 (immediate removal of administrative tasks). It operationalizes RA 4670. It sets 6 hours of actual classroom teaching plus 2 hours for ancillary tasks, which may be done inside or outside school premises. It provides overload pay and compensation for ancillary and teaching-related assignments. (N) — [PNA](https://alpha.pna.gov.ph/articles/1223752); [Manila Bulletin](https://mb.com.ph/2024/4/30/dep-ed-streamlines-public-school-teachers-workload-ancillary-tasks-for-more-teaching-time); [GMA on overload pay](https://gmanetwork.com/news/topstories/nation/905258/deped-overload-pay-public-school-teachers/story); DO 2 s.2024 PDF (P) — [deped.gov.ph](https://www.deped.gov.ph/wp-content/uploads/DO_s2024_002.pdf)
- In March 2025, DepEd said reforms would cut teacher paperwork by about 57%. Additional forms are to be filled out only according to a teacher's specific designation. (N) — [ABS-CBN](https://abs-cbn.com/news/nation/2025/3/18/deped-says-to-reduce-teachers-paperwork-by-approximately-57-percent-1708); [Inquirer](https://newsinfo.inquirer.net/2044603/deped-set-to-reduce-public-school-teachers-paperwork-by-57/amp)
- DO 2, s. 2024 was reported as ordering the immediate removal of administrative tasks from teachers. (N) — [Inquirer](https://newsinfo.inquirer.net/1894934/deped-on-officially-ordering-immediate-removal-of-admin-tasks-for-teachers)
- RA 4670 (Magna Carta for Public School Teachers, 1966), Sec. 13: teachers engaged in actual classroom instruction shall not be required to render more than 6 hours of actual classroom teaching a day. Teaching beyond 6 hours, up to a maximum of 8, is paid an additional 25% of basic pay. [background, not re-verified] — [lawphil RA 4670](https://lawphil.net/statutes/repacts/ra1966/ra_4670_1966.html)

### Inferences
- Teacher-load engine:
  - Store per teacher: daily teaching minutes, ancillary assignments with time credit, and overload minutes.
  - Validation for public schools: actual teaching up to 360 minutes a day, total up to 480 minutes; anything above 360 is flagged as overload.
  - Private schools are not bound by RA 4670. Load is set by the school or its CBA and the Labor Code, so make the limits configurable per school.
- Sectioning:
  - Section entity: grade, strand/track (SHS), adviser, room, capacity.
  - Default capacity 40, or 25 for SHS laboratory/workshop electives, with an override that records a reason, which mirrors the "larger classes with safeguards" allowance.
- The class-program builder should support both DO 12 options (45-minute periods or uniform 50/55/60-minute periods). It should validate that Filipino gets at least 200 minutes and Homeroom Guidance at least 45 minutes per week, and keep a different template for SHS (core/applied/specialized plus Work Immersion).
- Removing administrative tasks implies the system should push clerical work (forms, reports) to admin staff or roles, not advisers.

### Gaps
- I could not fetch the full DO 5, s. 2024 text (deped.gov.ph returned 403). Missing: the exhaustive list of ancillary tasks and teaching-related assignments, the overload compensation formula (service credits vs pay) and the effectivity details.
- I did not fetch the full JHS time-allotment table for all learning areas (Math, Science, AP, MAKABANSA/TLE, MAPEH, GMRC/Values Education).
- The new SHS curriculum (strengthened SHS, pilot from SY 2025-26) and its subjects and hours are not confirmed. Annex A was not obtained.
- I found no source on private-school teacher-load practice. Typical practice of about 24-30 units a week is anecdotal, so it is not included.

## 3. Attendance (SF2, SF4, tardiness, at-risk/dropout tracking)

### Takeaway
Daily attendance is recorded on School Form 2 (SF2) per section. Learner movement (transfers, dropouts) is summarized monthly on SF4. Both reconcile with the SF1 register generated from the LIS. I could not confirm a single binding absence threshold in a primary source. The commonly cited practice is a home visit after 5 consecutive absences, which is S-tier only.

### Cited Findings
- SF1 (School Register) is the class master list generated through the LIS, keyed by LRN and prepared by the adviser at the start of the year. SF2 is the daily attendance record and helps identify learners at risk of dropping out. SF4 (Monthly Learner's Movement and Attendance) summarizes transfers and dropouts and feeds division enrollment statistics. (S) — [SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-school-forms-guide); [TeachPinas](https://www.teachpinas.com/deped-school-forms-sf-1-10/)
- An SF2 template's instructions state that home visits are required for learners absent for 5 consecutive days or at risk of dropping out. This is unverified against an official order. (S) — [Scribd SF2](https://www.scribd.com/document/677015938/SF2)
- Checking rules (secondary summary of DepEd guidelines):
  - Cumulative school leavers and transferred-out learners must be validated against SF1 and SF2 per section.
  - The SF1 learner count must match learners who reported as of March 31 per SF4.
  - (S) — [TeacherPH](https://www.teacherph.com/guidelines-checking-school-forms/)
- DM 14, s. 2021 (pandemic) changed SF4 to quarterly submission and redefined the dropout column, so a learner counts as a dropout or "no longer participating" only under specific conditions. Its continued applicability after the pandemic is unclear. (P) — [DM s2021 014](https://www.deped.gov.ph/wp-content/uploads/2021/03/DM_s2021_014.pdf)
- DO 006, s. 2026 provides that portable devices are banned during instructional hours, with academic and emergency exceptions. Sanctions are in Annex G and are relevant to class-conduct logging. (S summary) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)

### Inferences
- Attendance module:
  - Per-session daily marks: present, absent, tardy, excused.
  - Monthly auto-generation of SF2, per section in DepEd layout.
  - Monthly SF4 roll-up.
  - Configurable at-risk rules, defaulting to 5 consecutive absences, which triggers a home-visit task for the adviser.
  - Integration with the guidance and case record.
  - End-of-year reconciliation checks: SF1 vs SF2 vs SF4.
- The LRN is the canonical learner key. The system should import from and export to LIS rather than replace it.

### Gaps
- The current official DepEd order on school forms (DO 58, s. 2017 on checking school forms, or any 2025 revision) and the tardiness definitions were not verified.
- I found no current DepEd program name or order for "learners at risk of dropping out" (e.g., the older DORP or the new ARAL program linkage).

## 4. Learner welfare (child protection, anti-bullying, discipline, guidance/mental health, health, inclusion)

### Takeaway
DO 40, s. 2012 (Child Protection Policy) remains in force. DO 006, s. 2026 (Ensuring a Safe and Motivating Learning Environment, ESMLE, dated March 24, 2026) now overlays it with mandatory forms, a centralized incident database, timelines and a three-level offense and sanction scheme. DO 006 does not amend or repeal DO 40 or the RA 10627 IRR. RA 12080 (2024) and its 2025 IRR create school counselor positions and division Mental Health and Well-Being Offices. A school system needs a confidential case-management module that complies with the Data Privacy Act.

### Cited Findings
- **DO 40, s. 2012 is still in force.** A Sept 26, 2024 DepEd memorandum issued supplemental guidelines for implementing it, covering referral and online safety. Division offices in 2025 still required an updated school-based child protection policy manual for SY 2025-2026. (S/division memos) — [Tangub div memo 053-2025](https://tangub.deped.gov.ph/wp-content/uploads/2025/02/divmemo053_2025.pdf); [Muntinlupa NUM 2025-408](https://deped-muntinlupa.com/wp-content/uploads/2025/08/NUM-2025-408.pdf)
- **DO 006, s. 2026 (ESMLE): title, date and coverage.**
  - Dated March 24, 2026.
  - Covers bullying, abuse, violence, exploitation, discrimination and gender-based sexual harassment, in physical and virtual settings including off-campus activities.
  - Binds public schools and CLCs. Private schools, SUCs/LUCs and PSOs are "encouraged" to adopt it.
  - Supplements DO 40 s.2012, DO 18 s.2015, DO 32 s.2017, DO 57 s.2017, DO 32 s.2019, DO 47 and 49 s.2022, and the RA 10627 IRR, and states it does not amend or repeal them.
  - Repeals DO 6 s.1954, DO 70 s.1999, DO 26 s.2000 and DO 83 s.2003 (cellphones).
  - (S summary of P) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)
- **DO 006, s. 2026: required artifacts.**
  - A Learner Handbook distributed at enrollment and posted in 3 conspicuous places or on the school website.
  - A standardized Code of Conduct for learners and personnel, with no corporal or humiliating punishment.
  - A localized anti-bullying policy submitted to the SDO.
  - Monthly random non-contact bag inspections under a plan submitted to the SDS. Stop-and-frisk and pat-downs are prohibited.
  - A Confiscation Slip (Annex F).
  - An Initial Risk Assessment Form (Annex H) completed by the Child Protection Committee (CPC).
  - An Incident Report and Intake Sheet.
  - A centralized incident database (incidents, actions, outcomes, learner details), access-restricted and compliant with RA 10173.
  - A designated Learner Formation Officer.
  - (S) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)
- **DO 006, s. 2026: CPC, timelines and reports.**
  - CPC composition: school head, guidance counselor or teacher, teacher representative, parent representative, learner representative and community representative.
  - Within 48 hours, the reporting personnel refers the case to the Disciplining Authority.
  - Within 10 calendar days, the fact-finding report goes to the School Head.
  - Within 30 calendar days, results go to the SDS and RD.
  - Due process: written notice, a 10-day written answer, a written decision, then appeal (generally 15 days; bullying cases go to the Office of the Undersecretary for Legal Affairs within 10 days).
  - An annual bullying report goes to the SDO in the first week of the school year.
  - Hotlines: 911, 1383, 1553.
  - (S) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)
- **DO 006, s. 2026 offense levels (reported July 2026).**
  - First level, e.g. profanity, simple vandalism: reprimand, parent conference, suspension.
  - Second level, e.g. theft, harassment, stalking, slight physical injuries: suspension, then non-readmission, then exclusion.
  - Third level, e.g. bomb threats or jokes, deadly weapons, hazing, sexual assault, drugs or liquor, cheating in exams, sharing sexually explicit or demeaning videos: non-readmission on the first offense, exclusion on the second. Third-level cases must be referred immediately to law enforcement and social welfare.
  - Victims must receive immediate mental health and psychosocial support.
  - (N) — [Tribune, 2 Jul 2026](https://tribune.net.ph/2026/07/02/bomb-threats-deadly-weapons-now-top-school-offenses-under-deped-rules)
- **School safety (Aug 2025).** DepEd ordered stricter school safety measures citing DO 40's prohibitions on violence and prohibited items. (N) — [Manila Bulletin](https://mb.com.ph/2025/08/09/deped-orders-stricter-school-safety-measures-to-prevent-violence-protect-learners)
- **RA 10627 (Anti-Bullying Act of 2013).** It requires all elementary and secondary schools to adopt anti-bullying policies. Schools must report bullying incidents and actions taken to the division office, and the school head must notify parents. [background, not re-verified] — [lawphil RA 10627](https://lawphil.net/statutes/repacts/ra2013/ra_10627_2013.html). The current reporting deadlines are those in DO 006 s.2026 above.
- **RA 12080 (Basic Education Mental Health and Well-Being Promotion Act).**
  - Signed Dec 2024.
  - Creates a Mental Health and Well-Being Office in each SDO.
  - Creates plantilla posts for Schools Division Counselor, School Counselor and School Counselor Associate.
  - Behavioral-science graduates may serve as School Counselor Associates.
  - Psychologists may counsel.
  - The IRR was signed in March 2025 and prioritizes offices in high-burden areas.
  - (P/N) — [lawphil RA 12080](https://lawphil.net/statutes/repacts/ra2024/ra_12080_2024.html); [DepEd IRR PDF](https://deped.gov.ph/wp-content/uploads/IRR-of-RA-12080-Basic-Education-Mental-Health-and-Well-Being-Promotion-Act-v2.pdf); [GMA](https://www.gmanetwork.com/news/topstories/nation/938137/angara-signs-irr-for-school-mental-health-programs-law/story); [Philstar](https://www.philstar.com/headlines/2024/12/09/2406146/new-law-signed-mental-health-services-be-expanded-schools)
- **RA 9258 (Guidance and Counseling Act).** It reserves counseling to licensed guidance counselors, though enforcement has been lax. (N) — [Philstar](https://www.philstar.com/headlines/2024/12/09/2406146/new-law-signed-mental-health-services-be-expanded-schools)
- **Homeroom Guidance.** It is a scheduled subject of at least 45 minutes a week (DO 12, s. 2024). (N) — [Inquirer](https://newsinfo.inquirer.net/1984864/deped-issues-new-guidelines-for-matatag-curriculum-implementation)

### Inferences
- Welfare/case module:
  - Incident intake, using fields modelled on the Incident Report and Intake Sheet.
  - Risk assessment (Annex H).
  - Case timeline with SLA timers: 48 hours, 10 days, 30 days, 10-day answer, appeal windows.
  - Offense classification by level, with the sanction ladder.
  - Confiscation slips.
  - Referral log (PNP, DSWD, SDO).
  - The annual bullying report generated for the first week of the school year.
  - Strict role-based access limited to the guidance counselor and CPC, with an audit trail.
- Guidance module: counseling session notes that only licensed RGCs or counselors can see, homeroom guidance records, and referrals to the SDO MHWO.
- Discipline outcomes (suspension, non-readmission, exclusion) must feed enrollment and LIS status. Exclusion removes the learner from the class list.

### Gaps
- School health and nutrition were not researched within the tool budget: SF8 content (BMI/nutritional status), the School-Based Feeding Program order (DO 39 s.2017 or later), deworming and the clinic. SF8 is only listed as the "health and nutrition" form. (S) — [SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-school-forms-guide)
- Inclusive education was not verified this session: DO 44 s.2021 (Policy Guidelines on Inclusive Education for Learners with Disabilities), RA 11650 (2022, Inclusive Education Act) and its IRR, and ILRCs.
- I found no primary source for the "Career Guidance" program order. The "RA 11206" citation in the brief was not verified. It may refer to the Secondary School TVL law rather than career guidance, so treat it as unconfirmed.
- DO 006 Annex I (full offense matrix) was not obtained. The July 2026 Tribune list may be partial.

## 5. DepEd reporting and planning (LIS/BEIS, SRC, SIP, SBM)

### Takeaway
Public schools must self-assess under the revised School-Based Management system, DO 007, s. 2024 (dated May 16, 2024), which repealed DO 83, s. 2012. The SIP is developed participatively and aligned with the revised SBM. Learner data flows through LIS (SF1, SF4 and enrollment), keyed by LRN. I could not verify primary-source details of BEIS/EBEIS, the School Report Card or monthly report lists in this session.

### Cited Findings
- DO 007, s. 2024, "Policy Guidelines on the Implementation of the Revised School-Based Management System," is dated May 16, 2024. It repeals DO 83, s. 2012 (SBM framework, assessment process and tool). (S division memo) — [DepEd Dasmariñas DM 431 s.2024](https://www.depeddasma.edu.ph/dm-no-431-s-2024-dissemination-of-deped-order-no-007-s-2024-policy-guidelines-on-the-implementation-of-the-revised-school-based-management-system/); [Tangub div memo 315-2024](https://tangub.deped.gov.ph/wp-content/uploads/2024/09/divmemo315_2024.pdf)
- All public schools submit an SBM Self-Assessment Checklist. Example deadlines were Oct 21, 2024 in one division and Apr 3, 2025 for SY 2024-25 in another. (S) — [Muntinlupa NUM 2024-317](https://deped-muntinlupa.com/wp-content/uploads/2024/11/NUM-2024-317.pdf); [Tangub div memo 315-2024](https://tangub.deped.gov.ph/wp-content/uploads/2024/09/divmemo315_2024.pdf)
- According to an orientation deck, the revision ties the SIP to the rationalized plan structure. This is unofficial. (S) — [Slideshare DO 007 orientation](https://www.slideshare.net/slideshow/policy-orientation_-do-007-s-2024-2-pptx/275829929)
- LIS screenshots, LRNs and learner PII must never be posted on social media (2019 DepEd advisory). (N) — [Summit Express](https://www.thesummitexpress.com/2019/04/deped-warns-posting-diploma-information-social-media.html)
- SF4 feeds division enrollment statistics, and SF1 is generated from LIS. (S) — [SchoolFinderPH](https://www.schoolfinderph.com/blog/deped-school-forms-guide)
- The annual bullying report goes to the SDO in the first week of the school year (DO 006 s.2026). (S) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)

### Inferences
- The system should produce data exports matching:
  - LIS uploads: enrollment, SF1 and end-of-year status.
  - School forms: SF1, SF2, SF4, SF5 (promotion), SF6 (summary), SF7 (personnel), SF8 (health), SF9 (report card) and SF10 (permanent record).
  - BEIS school-profile data: rooms, seats, toilets, personnel counts and enrollment by grade/sex.
  - SBM evidence repository and SIP/AIP tracking.
  - DO 006 incident and bullying reports.
- Private schools are not covered by SBM (it is a public-school system), but they also report enrollment through LIS. Make SBM/SIP modules toggleable by school type.

### Gaps
- I did not verify the current BEIS/EBEIS data-collection cycle (beginning-of-school-year/end-of-school-year), the School Report Card (SRC) order, the SIP guide version, or LIS end-of-school-year deadlines.
- I did not obtain the full text and Annex A indicators of DO 007, s. 2024.

## 6. Personnel (SF7, plantilla, PRC/LET, RPMS/PPST)

### Takeaway
Little was verified within the tool budget. Confirmed: RA 12080 adds new counselor plantilla items, and DO 5, s. 2024 requires tracking teaching vs ancillary hours and overload. SF7 (School Personnel Assignment List) is the standard personnel form, but its fields were not verified.

### Cited Findings
- RA 12080 creates plantilla posts for School Counselor, School Counselor Associate and Schools Division Counselor. The CSC is to standardize recruitment for school counselors. (N) — [GMA on CSC](https://www.gmanetwork.com/news/topstories/nation/938243/csc-to-oversee-standardization-of-recruitment-process-for-school-counselors/story); [lawphil RA 12080](https://lawphil.net/statutes/repacts/ra2024/ra_12080_2024.html)
- DO 5, s. 2024 provides workload, overload pay and ancillary compensation (see Section 2). (N) — [PNA](https://alpha.pna.gov.ph/articles/1223752)
- RA 4670 covers public teachers' hours and additional pay. [background, not re-verified] — [lawphil RA 4670](https://lawphil.net/statutes/repacts/ra1966/ra_4670_1966.html)

### Inferences
- The personnel record should cover:
  - Identity, plantilla item number and position (public only), and employment status.
  - PRC license number and expiry, LET status, and Registered Guidance Counselor license for counselors.
  - Teaching assignments and ancillary designations with time credits.
  - Overload ledger, IPCRF/RPMS rating per year, PPST career stage, and trainings.
  - This supports SF7 output.

### Gaps
- Not verified: the SF7 format, the RPMS order (DO 2 s.2015 / DO 42 s.2017 PPST), whether the 2025 results-based performance management (RPMS-PPST) revision applies, and private-school teacher licensing requirements (RA 7836 as amended by RA 9293). I fetched no sources on these.

## 7. Websites, social media, digital systems, data privacy

### Takeaway
DO 007, s. 2026 (Media Management Guidelines) reportedly requires official school pages to be created with a @deped.gov.ph office email and named exactly after the school. DO 49, s. 2022 bars personnel from social-media interaction with learners outside school, except relatives, and bars using DepEd email for personal social media. An Aug 11, 2026 memo reiterates responsible use. RA 10173 governs learner data. Posting LIS data or LRNs publicly is prohibited.

### Cited Findings
- DO 007, s. 2026 (Media Management Guidelines) provides that official pages must be created using an office's @deped.gov.ph email. The page name must match the official school or office name. Page editors may use DepEd-issued personal emails with the Head of Office's approval. The order is anchored to RA 10173. (S blog; verify) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-007-s-2026-media-management.html)
- The Aug 11, 2026 DepEd memorandum on responsible social media use covers posts involving learners, classrooms, premises or duties. There is no blanket ban on personal accounts, but they are regulated when they appear official or harm DepEd. It cites DO 006 and DO 007, s. 2026. (N) — [Tribune](https://tribune.net.ph/2026/08/12/deped-reminds-personnel-exercise-professionalism-caution-on-social-media); [Tribune](https://tribune.net.ph/2026/08/12/deped-hammers-socmed-prudence)
- A claim that personnel are prohibited from having personal accounts contradicts the memo and is treated as unreliable. — [tchersden](https://www.tchersden.com/2026/08/responsible-use-social-media-deped-personnel-2026.html) vs [Tribune](https://tribune.net.ph/2026/08/12/deped-reminds-personnel-exercise-professionalism-caution-on-social-media)
- DO 49, s. 2022 provides that staff must not follow or interact with learners on social media outside the school setting unless they are relatives. DepEd email must not be used for personal social media accounts. (N) — [GMA](https://www.gmanetwork.com/news/topstories/nation/850283/deped-reminds-employees-to-avoid-relationships-social-media-chats-with-students-outside-school/story/); [PhilSTAR Life](https://philstarlife.com/news-and-views/386642-deped-memo-social-media-use)
- A May 2024 memorandum states that learners are data subjects protected by the Data Privacy Act, which governs posting of learner images and data. (S) — [DepEd Tambayan](https://www.depedtambayanph.net/2024/05/guidance-on-posting-learners-images-or.html)
- A 2019 advisory bans posting LIS screenshots, LRNs, names, documents or enrollment histories on any public social media, regardless of privacy settings. (N) — [Summit Express](https://www.thesummitexpress.com/2019/04/deped-warns-posting-diploma-information-social-media.html)
- DO 006, s. 2026 requires incident records to comply with RA 10173, with access limited to authorized personnel and administrative liability for breaches. The Learner Handbook may be posted on the school website. (S) — [eduknasyon blog](https://eduknasyon.blogspot.com/2026/03/deped-order-006-s-2026-guidelines-on.html)

### Inferences
- The public school website should:
  - Publish the Learner Handbook, calendar and announcements.
  - Never publish LRNs, learner lists, grades or identifiable photos without consent.
  - Expose a privacy notice and DPO contact.
- The portal should use role-based access, audit logs and consent records for learner images. Public schools should use @deped.gov.ph email for official accounts and SSO where possible.
- For a private school, DO 006 and DO 007 are persuasive or encouraged rather than binding, but RA 10173 applies fully.

### Gaps
- Not found: a DepEd order specifically on school information systems, third-party apps or cloud, or the DepEd Data Privacy Manual / DPO structure (e.g., DO 3 s.2020 or later). I did not search privacy.gov.ph NPC circulars for schools (e.g., NPC Advisory on schools' CCTV and online learning). These should be researched further.
- I did not read the full DO 007, s. 2026 text.
