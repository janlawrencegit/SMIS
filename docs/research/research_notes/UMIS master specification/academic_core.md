# Academic Core of a University Management System (Curriculum, Calendar, Scheduling, Enrollment, Grading/Transcripts, Degree Audit/Graduation), with Philippine conventions

Scope note: This covers the academic core only (not admissions, finance or HR). Sources are vendor documentation (Ellucian Degree Works, Oracle PeopleSoft Campus Solutions), Philippine registrar documents (UP Diliman OUR, UP OVPAA, Mapúa, PUP), and timetabling literature (ITC-2007). Several UP PDFs were downloaded and text-extracted to quote them exactly. Items marked "Inference" are design conclusions drawn from the cited material, not vendor statements.

---

## 1. What entities and relationships are required?

### Takeaway
Mature systems split the static offering (program, curriculum/requirement version, catalog course) from the term-specific delivery (term, section, meeting, enrollment, grade). They also tie every requirement set to an "academic structure + catalog year/requirement term", so each student is audited against the version they entered under. Requirements are built as a tree: group, then requirement, then line/rule, then course list/condition. Grades come from a configurable scheme in which each value carries flags (points, include-in-GPA, earn-credit, in-progress, valid-attempt).

### Cited Findings
- PeopleSoft Academic Advisement: the **requirement group** is the highest-level parent record. It contains **detail lines** pointing to conditions, courses and requirements, plus parameters such as unit and course minimums. It defines the student population it applies to (all undergraduates, one plan, one student group). — [Oracle: Understanding Academic Requirement Groups](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/understanding-academic-requirement-groups.html)
- The PeopleSoft engine matches the student's **career, program, plan, subplan and precondition** against the requirement group's academic structure. It uses the **catalog year ("requirement term")** to decide which groups apply. — [Oracle: Understanding Academic Requirement Groups](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/understanding-academic-requirement-groups.html)
- PeopleSoft requirements are built bottom-up: course lists first, then requirement line items, then requirements, then requirement groups. Groups at the same structure level and reporting sequence are evaluated in group-number order. — [Oracle Academic Advisement 9.2 PDF](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/academic-advisement.pdf); [CSUCI Advising Setup Guide](https://www.csuci.edu/cicms/internal/sa/Advisement/Advising%20Setup%20Guide.pdf)
- Degree Works audits are organized into **blocks**, each showing the catalog year it runs from and a status (incomplete / in-progress / complete / unmet rule). Block types include: Degree; General Education; Major/Minor/Certificate; Additional program blocks (admission requirements, upper-division GPA); "Audited, Dropped, Failed, Repeated" (courses ineligible to fulfill requirements); "Not Counted" (e.g. only one course of a group counts); and graduation-optional blocks such as Honors College. — [Missouri State Degree Works User Guide 5.1.6 (AUL/Exceptions)](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- Degree Works course wildcards: `HST @` means any HST course, `SPN 5@` means any 500-level SPN course. Clicking a course shows its prerequisites, description and term schedule with seats available. — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- PeopleSoft grading: each **Grading Scheme** has **Grade Bases** (e.g. OPT, SUS, PNP; NON is required). Each **Grade Input** value carries Grade Points, Include in GPA, Earn Credit, In Progress Grade, Exclude Progress Units, Valid Attempt, Convert To Grade, Include in Self Service (faculty roster) and Grade Category. An Audit grade basis disables the GPA, credit and in-progress flags. — [Oracle: Setting Up Your System for Grading](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)
- PeopleSoft defines **penalty grades** per grade basis (Drop with Penalty, Drop with Greater Penalty, Withdraw with Penalty, Withdraw with Greater Penalty). Without them, the enrollment engine falls back to the Session Calendar setting. — [Oracle Grading setup](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)
- UP Diliman vocabulary that the data model must represent:
  - academic year of 2 semesters (≥16 weeks / ≥100 class days) plus a 6-week summer session
  - Program = degree + discipline
  - Subject = course
  - Prerequisite; Corequisite ("taken simultaneously within a semester")
  - Cross-registration
  - Shiftee 1 / Shiftee 2 (within college / within university)
  - Transferee 1 / Transferee 2 (other UP unit / outside UP)
  - Regular vs Irregular student; Non-degree and Special student; Non-major (dismissed from college, not from university)
  - Rejoining student; LOA; AWOL; Residence enrollment
  - Year level by % of units: Freshman ≤25%, Sophomore 25–50%, Junior 50–75%, Senior ≥75%

  — [UPD General Catalogue Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- UP distinguishes several averages:
  - **GWA**: all subjects at a level, including previous programs and enrichment subjects
  - **Curriculum Weighted Average**: only courses credited in the new program; used for shifting
  - **Cumulative Weighted Average Grade**: graduate level; only courses in the approved Program of Study, plus residence-rule courses
  - Honors average: only resident credit, curriculum-prescribed courses plus qualifying electives

  — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf); [UPD Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- The UPD Transcript of Records is the "complete and permanent educational record of a student, whether graduated or not". It is official only with the University Registrar's original signature and the seal. The **True Copy of Grades** is a less detailed internal evaluation document. Certificates include the Certificate of Completion (issued while awaiting BOR conferment), Certificate of Graduation and Certificate of Enrollment. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)

### Inferences (proposed data model)
- **Curriculum and catalog**
  - `Institution` → `College/Faculty` → `AcademicUnit(Department)`
  - `Program` (degree type, discipline, level/career UG/GR/doctoral, normal length in terms, CHED/BOR authority ref, status) → `Major/Track/Specialization` (optional) → `CurriculumVersion` (effective admit term / catalog year, status draft/approved/active/phased-out, approving body and ref, total units)
  - `CurriculumVersion` → `CurriculumTerm` (year level + term slot, e.g. Y1-S1, Y2-Midyear) → `CurriculumCourse` (course or elective-slot placeholder, units, required/elective/GE category, recommended term)
  - `Course` (catalog master: subject code + number, title, credit units, contact hours lecture/lab, grading basis default, repeatable flag and max, effective-dated versions, owning unit, credit-bearing flag for NSTP/PE)
  - `CourseRequisite` (prereq/coreq/concurrent, stored as a boolean expression tree; can reference course, standing/year level, units earned, program, min grade, permission)
  - `CourseEquivalency` (internal equivalents and cross-listings; effective-dated)
  - `ElectiveGroup` / `CourseList` (explicit list, wildcard rules such as "any MATH 1xx", attribute-based lists such as GE domain AH/SSP/MST)
  - `RequirementGroup` → `Requirement` → `RequirementRule/Line` → `CourseList`/`Condition`. The CurriculumVersion either generates these or holds them directly.
- **Calendar**
  - `AcademicYear` → `Term` (TermType from a configurable lookup: semester, trimester, quarter, summer/midyear; sequence; counts-as-regular flag; start/end; census date)
  - `Term` → `Session/PartOfTerm` (full term, first half, modular) → `CalendarEvent/Deadline` (typed: pre-enlistment, registration, change of matriculation, last day to drop, withdrawal, grade submission, INC removal period, graduation application, clearance)
- **Scheduling**
  - `ClassOffering` (course × term)
  - `Section` (section code, capacity, reserved seats by program/year, delivery mode, campus, grading basis, linked components lecture/lab, cross-listed group)
  - `MeetingPattern` (days, start/end, date range, room, component)
  - `Room` (building, capacity, type, features, owner unit, availability)
  - `InstructorAssignment` (faculty, role, load credit %)
  - `FacultyAvailability` / `FacultyLoadPolicy`
- **Enrollment**
  - `StudentProgram` (student × program × curriculum version × admit term × status; history rows for shifts)
  - `TermRegistration` (student × term: load class regular/irregular/overload/underload, max units, status, assessment link)
  - `Enrollment` (student × section: status enlisted/enrolled/waitlisted/dropped/withdrawn, dates, units, grading basis, override records)
  - `WaitlistEntry`; `Hold` (type, source office, blocks which actions, dates); `Override/Permission` (type matching the error type, granted by, scope)
  - `AdvisingRecord` / `StudyPlan`; `CrossEnrollment` (home/host institution, approval chain)
- **Grading**
  - `GradeScale/Scheme` (per institution/level/program, effective-dated) → `GradeValue` (code, points, percentage range, flags)
  - `GradeRoster` (section × grade type midterm/final, status) → `GradeEntry` (enrollment × grade value, entered by/at)
  - `GradeChangeRequest` (old → new, reason, approvals)
  - `IncompleteContract` (deadline, lapse-to grade)
  - `TermStanding` (term GWA, units attempted/earned, scholastic status, dean's list)
  - `TransferCredit` (source institution, source course, grade, equivalent course, units, evaluator)
- **Audit and graduation**
  - `AuditRun` (snapshot of results per requirement, what-if flag, parameters)
  - `AuditException` (substitute / also allow / apply here / force complete / remove-or-change-limit; tied to requirement address and catalog version)
  - `GraduationApplication`; `ClearanceItem` (office, status); `HonorAward`; `Diploma` (number, conferment date, BOR/Academic Council ref)
  - `TranscriptRequest` / `IssuedDocument` (serial, signatories, verification hash)

### Gaps
- I did not retrieve vendor documentation for the Banner Student catalog/schedule tables (SCACRSE/SSASECT), so Banner-specific entity names are not cited.
- No authoritative source was retrieved for the CHED-prescribed curriculum structure (CMO per discipline). Units per GE course and curriculum approval workflows under CHED were not confirmed in this research.

---

## 2. What business rules and constraints must be enforced?

### Takeaway
The core rules are well documented in PH registrar sources:
- normal load 15–18 units (21 for some programs), with overload and underload needing approval
- requisite checks, time-conflict and capacity checks, each override type-specific
- scholastic standing computed by % of units failed
- Maximum Residence Rule of 1.5× normal program length
- INC/4.0 removal within one academic year, after which the grade lapses to 5.0
- honors residency of 75% of units plus 2 years
- program retention rules (e.g. Engineering 24-unit rule, Math-fail limits)

### Cited Findings
- **Unit load (UPD)**:
  - Normal load = units the curriculum requires per semester, 15–18 academic units (21 for some programs)
  - Overload = 21 units and more
  - Underload = less than 15 units, or less than the normal load in the curriculum

  — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Irregular student (UPD)**: registered for formal credit but carrying less than the full load the curriculum calls for in that semester. **Regular** students carry the full semester load prescribed by their curricula. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Scholastic standing (UPD)**, by % of units with grades below "3":
  - Good standing: grade of 3 or better in ≥75% of registered units
  - Warning: 25–49% failed
  - Probation: 50–75% failed; load limited by the Dean; lifted by passing >50% of units next semester
  - Dismissal from college: ≥76% failed
  - Permanent disqualification: 100% failed

  — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Program retention rules**: Engineering students may fail any Math subject at most twice. The "24-unit rule" requires passing ≥24 units per academic year; violators become Non-Majors. — [UPD Glossary (College-specific terms)](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Maximum Residence Rule**: students must finish within actual residence equal to 1½ times the normal length of the course. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Transferee advance credit (UPD)**: admitted transferees must validate courses from their previous school at up to 18 units per semester, within 3 semesters of admission. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Corequisite** = taken simultaneously within a semester. **Prerequisite** = required before enrolling. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **INC (UPD)**:
  - Definition: given when class standing is "Passing" but the student misses the final exam or other requirements for illness or other valid reasons
  - **Grade of 4** = "Conditional". Removed only by re-exam within one academic year: pass → 3, fail → 5, not removed → becomes 5

  — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **UP removal window**:
  - The removal period is one academic year. A grade can no longer be improved after the third regular removal period following the term it was incurred.
  - A 4.0 earned after completing an INC must be removed within the remaining time of the original INC period.
  - Removal at other times needs Dean approval and a fee.
  - The student must be enrolled (or enrolled "for residence") in the term of completion.
  - Permit: UP Form 25.

  — [UPD OUR: Removal of Incomplete](https://our.upd.edu.ph/files/acadinfo/REMOVAL%20OF%20INCOMPLETE.pdf); [UPD OUR: Removal of the Grade of 4](https://our.upd.edu.ph/files/acadinfo/REMOVAL%20OF%20THE%20GRADE%20OF%204.pdf); [UP OVPAA Memo 2021-95](https://www.ac.upd.edu.ph/acmedia/images/newpdfs/OVPAA_Memo_2021_95_Inc_4.pdf) (search-result summaries; the PDFs were not fully read)
- **Mapúa (trimester)**:
  - "I" is completed within the next trimester or it lapses and the course must be repeated; it is excluded from the term weighted average
  - "W" (official withdrawal) is filed by Friday of week 7, cannot be removed, and is allowed at most twice for the same course; PE/NSTP cannot be withdrawn
  - 5.00 is given for poor performance, unofficial withdrawal, absences ≥20% of school days, or integrity violations
  - "C" (continuing, thesis) must be completed within one academic year
  - Audit (Au) is not on the TOR and is excluded from averages

  — [Mapúa: Grading System](https://support.mapua.edu.ph/kb/article/53/grading-system)
- **PUP**: 1.0 (excellent) to 5.0 (failure). INC appears to lapse to 5.0 if not completed within one year. W = voluntary drop. This comes from a third-party Scribd copy of the handbook and is unverified. — [Scribd: PUP Grading System](https://www.scribd.com/doc/223256007/Pup-Grading-System)
- **Registration error checking (Banner schools)**:
  - Time-conflict errors name the conflicting CRN; check lecture, lab and recitation, and note that alternate-week courses can trigger false conflicts
  - Capacity overrides allow over-enrollment without raising capacity
  - Maximum-hours errors need overload approval (one school caps at 20 credits/semester)
  - The override "MUST MATCH the registration error"

  — [Ole Miss: Common Registration Errors](https://olemiss.edu/encompass/students/common-registration-errors/); [UNF: Registration Override Codes](https://unf.edu/records/registration/registration-overrides.html); [Purdue: Registration Error Help](https://www.purdue.edu/registrar//faculty/advisors/registration_error_help.html)
- **Repeat handling (PeopleSoft)**: each grade has a repeat-checking option combining "counted in repeat pool" (Y/N) with "processed by repeat checking" (Y/N). — [Oracle Grading setup](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)
- **Degree Works repeats**: repeated courses move to the "Audited, Dropped, Failed, Repeated" block only after end-of-term processing assigns the repeat code. — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)

### Inferences
- **Rule engine shape**: model each rule as a configurable `Policy` with scope (institution > college > program > curriculum version) and effective term. Each check (requisite, conflict, capacity, max/min load, hold, program restriction, repeat limit) returns a typed error code, and each `Override` grants exactly one error code for one section/term. This mirrors the Banner practice of overrides matching the error.
- **Requisite expression**: an AND/OR tree with nodes such as `COURSE(code, minGrade, allowConcurrent)`, `STANDING(yearLevel)`, `UNITS_EARNED(n)`, `PROGRAM(in list)`, `CONSENT(instructor|chair)` and `NOT_TAKEN(course)` (anti-requisite).
  - Satisfaction must consider equivalencies, transfer credit, in-progress enrollment (provisional pass), and an INC that has not yet lapsed (treat as unsatisfied unless policy allows).
  - Coreqs must be validated as a set at commit time, so dropping a coreq triggers a cascade warning.
- **Load**:
  - Computed max = min(curriculum term load, policy max, probation cap set by the Dean); graduating students may get +3 or +6 by policy.
  - Overload ≥ threshold requires an approval workflow.
  - Underload below the normal load flags the student irregular.
  - Load decisions must be persisted, because UP honors eligibility needs documented underload justification (see §6).
  - Non-credit units (e.g. NSTP, or PE where configured) are counted for load but excluded from GWA. This was not verified per institution; make it configurable.
- **Lapse jobs**: a scheduled job converts INC/4.0/"I" past its deadline to the configured lapse grade (5.0 or "repeat required"). The deadline is computed from the term in which the grade was incurred, plus N regular terms or one academic year. Summer is not counted as a regular term at UP; make this configurable per scheme.
- **Scholastic standing**: computed per term from final grades, using %-of-units thresholds stored in policy (UP style) or a GPA threshold (US style). The result feeds holds (probation load cap, dismissal block).
- **MRR**: a counter of terms in actual residence (excluding LOA). Raise a warning at a threshold and enforce at 1.5× normal length (configurable).
- **Grade finalization lock**: once a roster is approved/posted, edits are only possible via a GradeChangeRequest with an approval chain. Locks are by term or roster, with an admin reopen that is logged.

### Gaps
- I did not fully read the UPD Removal PDFs or OVPAA Memo 2021-95. The pandemic-era memo may have changed INC deadlines (e.g. extensions); verify the current text.
- DLSU and Ateneo specific load and grading rules (DLSU 4.0 CGPA, Ateneo QPI A–F) could not be confirmed from primary sources in this session. DLSU's three trimesters of about 14 weeks each was found. — [DLSU Academic Calendar](https://www.dlsu.edu.ph/?p=14587)
- Retake policy (which attempt counts, e.g. latest vs best vs all averaged) is institution-specific. I found no PH-wide rule. UP's GWA includes all grades taken, per its "all subjects taken" definition ([UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)), which implies failed attempts stay in the GWA; this inference was not confirmed with an explicit UP retake rule.

---

## 3. How should grading scales be modelled to be configurable (numeric 1.0–5.0, letter, percentage, pass/fail)?

### Takeaway
Use a scheme → basis → grade-value model with per-value flags, following PeopleSoft (and Workday). Each grade value maps to points and carries independent booleans for GPA inclusion, credit earning, in-progress/temporary status, valid attempt, progress-unit exclusion and faculty-selectable. Scales are effective-dated and assigned by level/program, with section-level grading-basis options. Direction ("lower is better" for PH 1.0–5.0 versus "higher is better" for 4.0) and honor thresholds must be scheme properties, not hard-coded.

### Cited Findings
- PeopleSoft grade-value flags:
  - Grade Points: used with units attempted to compute GPA
  - Include in GPA: e.g. not for Pass
  - Earn Credit
  - In Progress Grade: e.g. Incomplete
  - Exclude Progress Units: e.g. W
  - Valid Attempt: A–F valid, AU/W invalid
  - Convert To Grade: posts a converted grade within the same scheme
  - Include in Self Service: whether faculty may assign it on the roster
  - Audit basis: disables the GPA, credit and in-progress flags

  — [Oracle: Setting Up Your System for Grading](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)
- PeopleSoft Grade Basis Exception Rule maps student-requested grade bases to existing rules (e.g. graduate to undergraduate scheme). — [Oracle Grading setup (search summary)](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)
- Workday likewise has an "Include in GPA" setting on grades. — [Workday: Grade Point Averages concept](https://doc.workday.com/admin-guide/en-us/student/student-records/academic-records/academic-policies/concept--grade-point-averages.html)
- PH numeric scale example (Mapúa):
  - 1.00 Excellent; 1.25 Highly Meritorious; 1.50/1.75 Meritorious
  - 2.00/2.25 Very Satisfactory; 2.50/2.75 Satisfactory
  - 3.00 lowest passing; 5.00 Failure
  - Percentage cutoffs are set per course syllabus, not centrally
  - P/F only for thesis/practicum, where F counts as 5.00 in the average

  — [Mapúa: Grading System](https://support.mapua.edu.ph/kb/article/53/grading-system)
- UP adds **4.0 "Conditional"** (removable by re-exam → 3 or 5) and INC, both temporary. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- DLSU graduate scale reportedly runs 4.0–0.0 (master's) and 4.0–2.5 (doctoral), with retake required below 2.0 / 2.5. P/F units count toward enrolled load. This comes from a third-party Scribd document and is unverified. — [Scribd: DLSU Grading System](https://www.scribd.com/document/166856783/DLSU-Grading-System)
- UP honor/scholar thresholds (lower is better):
  - University Scholar ≤1.45 term average (UG); ≤1.25 (graduate)
  - College Scholar ≤1.75 (UG); ≤1.50 (graduate)

  — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)

### Inferences
- **`GradeScheme`**: id, name, level/career, effective_from/to, `direction` (ASC_BETTER | DESC_BETTER), `passing_threshold_points`, `precision`/rounding rule (e.g. truncate vs round to 2 or 4 decimals), `average_label` (GWA/GPA/QPI/CGPA), and optional `percent_to_grade` transmutation table per course or section. Mapúa leaves percentage bands to syllabi, so transmutation may need to live at section level.
- **`GradeValue`**: code (1.00, 1.25, …, 5.00, INC, 4.00, DRP, W, P, F, AU, NG, IP), display label, points (nullable), percent_min/max, `counts_in_average`, `earns_credit`, `is_passing`, `is_temporary/in_progress`, `lapse_to_value` + `lapse_rule` (N regular terms / 1 AY / next term), `is_valid_attempt`, `counts_toward_load`, `faculty_selectable`, `requires_approval` (e.g. DRP/W entered by registrar only), `shows_on_transcript`, `sort_order`.
- **Assignment**: Program/CurriculumVersion → default scheme; Course → allowed bases (graded / P-F / audit); Section → chosen basis; Enrollment → student-elected basis (where allowed).
- **Averages**: define named `AverageDefinition`s (Term GWA, Cumulative GWA, Curriculum WA, Honors WA, Major GPA). Each has filters:
  - which grade values count
  - which enrollments: resident-only, curriculum-only, elective selection order
  - repeat treatment: all / latest / best
  - level boundary

  Formula: Σ(points × units) / Σ(units) over counted rows. Store the computed values per term with an audit trail.
- **Cross-scheme conversion** for transferees (e.g. letter → 1.0–5.0): a `GradeConversionTable` per source institution or scheme. Transfer grades are usually excluded from resident averages (see §6).

### Gaps
- I did not find a CHED-mandated national grading scale. CHED appears to leave grading to HEIs (a secondary commentary says there is no uniform national cutoff). — [Respicio commentary](https://www.respicio.ph/commentaries/legal-requirements-for-granting-latin-honors-in-philippine-schools) (secondary, non-authoritative)
- Rounding and truncation conventions for GWA at PH schools were not found in primary sources.

---

## 4. How do degree audit engines (Degree Works, PeopleSoft AA, uAchieve) model requirements and what-if analysis?

### Takeaway
Both Degree Works and PeopleSoft model requirements as a hierarchy of blocks/groups keyed to academic structure and catalog year.
- Degree Works uses its Scribe language. Courses are allocated to rules with sharing restrictions, unusable courses go to fallthrough/"Not Counted" and "Failed/Repeated" blocks, and status shows as complete / in-progress / incomplete / unmet.
- Student-specific deviations are stored as exceptions (Substitute, Also Allow, Apply Here, Force Complete, Remove Course / Change Limit) tied to a block address. An exception is "broken" if the student's program or catalog changes.
- What-If runs the same engine against a hypothetical program or catalog year without changing the record.

### Cited Findings
- Degree Works audit types: **Academic** (primary) and **What-If** (a prospective audit for a different program or degree). Views include Student View and Registrar Report (which shows the Scribe code). — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- What-If lets students "test out hypothetical changes to their student record without officially committing the changes". It allows choosing a different program or catalog year and additional areas of study (extra majors/minors). — [Missouri State DW Guide 5.1.6](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516Registrar.pdf); [WWU What-If](https://registrar.wwu.edu/degree-works/what-if)
- New Scribe blocks are tested via What-If by selecting the program and the new catalog term. — [CVTC KB: Scribe Catalog Updates](https://kb.cvtc.edu/page.php?id=124426)
- Degree Works refreshes audits nightly when grades, registration or test scores change; users can also process manually. — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- Degree Works status legend:
  - Complete; Complete except in-progress; Not Complete
  - "Unmet block or requirement rule": e.g. a GPA or minimum-credit qualifier not met, with no course list to show

  — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- **Degree Works exception types**:
  - **Also Allow**: adds a course to a requirement list. Also used for in-progress or incomplete courses.
  - **Apply Here**: forces a specific course onto a requirement. Can override a sharing restriction to double-count, move a course between requirements, or accept a grade below the minimum. Recommended only for passed courses; in-progress use needs a grade filter.
  - **Force Complete**: marks a requirement satisfied with no course. "Should be among the least used."
  - **Substitute**: replaces one course with another.
  - **Remove Course / Change Limit**: removes a course from a list, or raises/lowers the credit or class count (a lower count acts as a waiver).
  - Filters ("With" qualifiers) select among duplicate course instances, e.g. repeatable topics or transfer electives.
  - Exceptions cannot be edited, only deleted and re-entered. Descriptions are limited to 50 characters, details to 220 characters.
  - "Each exception ties to a specific block, which is like an address based on the program and catalog identification of the block". A program change breaks the exception.

  — [Missouri State DW Guide (Exceptions)](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- Degree Works handles transfer-based waivers by entering a "fake course" in transfer evaluation (e.g. GEN 042 for a completed 42-hour GE block), which automatically satisfies GE. — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)
- Exceptions override the Scribe for one student without changing the rules for everyone else. — [NJIT Degree Works](https://www.njit.edu/registrar/node/746)
- PeopleSoft AA:
  - requirement group → requirements → line items with course lists or conditions
  - applies by career/program/plan/subplan + precondition + requirement term (catalog year)
  - processing order by reporting sequence, then group number

  — [Oracle AA docs](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/understanding-academic-requirement-groups.html); [CSUCI Setup Guide](https://www.csuci.edu/cicms/internal/sa/Advisement/Advising%20Setup%20Guide.pdf)
- PeopleSoft uses the grade's "Valid Attempt" flag in Academic Advisement to distinguish valid from invalid attempts. — [Oracle Grading setup](https://docs.oracle.com/cd/G40826_01/cs92pbr36/eng/cs/lssr/SettingUpYourSystemforGrading-ab47e2.html)

### Inferences
- **Requirement model**: `RequirementNode` tree with node types:
  - GROUP (all-of / n-of / min-units)
  - COURSE_SET (explicit list, wildcard, attribute query; min grade; min units/courses; max units)
  - CONDITION (min GPA in scope, min resident units, min upper-level units)
  - NON_COURSE (thesis defense, practicum hours, NSTP, exit exam, comprehensive exam)

  Each node has sharing policy (exclusive / may share with listed nodes), `optional_for_graduation`, display order and catalog effectivity.
- **Allocation algorithm**: a deterministic greedy pass with priority (most-specific rule first), then a backtracking or optimization pass to maximize satisfied requirements. Leftover courses go to Electives / Not Counted / Insufficient (failed/withdrawn/INC) buckets.
- **Exceptions**: model student exceptions as first-class records tied to the requirement node + curriculum version, with type ∈ {substitute, also_allow, apply_here, force_complete, remove_course, change_limit, waive}, approver, reason and date. On program or curriculum change, re-evaluate and flag exceptions as "broken" (Degree Works behaviour), rather than silently dropping them.
- **What-if**: run the engine with a hypothetical StudentProgram (program, curriculum version, additional minor) plus hypothetical planned courses. Never persist to the official record; store the run as an AuditRun with `is_what_if = true`. This directly supports PH shiftee evaluation, where UP's Curriculum Weighted Average is computed only on courses creditable in the new program.
- **Audit snapshots** should be stored at graduation evaluation for defensibility.

### Gaps
- uAchieve (CollegeSource) documentation was not retrieved, so no cited description of its requirement model is included.
- The Degree Works Scribe syntax details (BLOCK, RULE, ShareWith/DontShare, MinGrade qualifiers) are documented in the Scribe Language User Guide, which I did not read in full. — [Jefferson-hosted Scribe Guide 5.0.1](https://banadmin.jefferson.edu/Banner_Docs/OtherDocs/Degree_Works_Scribe_Language_User_Guide_5.0.1.pdf)

---

## 5. What scheduling/timetabling approaches and constraints are used?

### Takeaway
In practice, registrars build schedules manually or semi-manually (copy forward the prior term, then edit) with real-time conflict checks. Automated optimization is formalized in the academic literature as curriculum-based course timetabling (CB-CTT, ITC-2007 Track 3) and post-enrollment timetabling. In those formulations, hard constraints cover room/teacher/curriculum conflicts and availability, and soft constraints are penalties for room capacity, minimum working days, isolated lectures and room stability.

### Cited Findings
- **ITC-2007 Track 3 (CB-CTT) hard constraints**:
  - every lecture scheduled
  - RoomOccupancy: no two lectures in the same room and period
  - Conflicts: lectures of courses in the same curriculum, or taught by the same teacher, in different periods
  - Availabilities: teacher/course unavailable periods

  Some formulations add a hard rule keeping all lectures of a course in one room. — [Harmony Search for CB-CTT (arXiv 1401.5156)](https://arxiv.org/pdf/1401.5156); [Feature-based tuning SA for CB-CTT (arXiv 1409.7186)](https://arxiv.org/pdf/1409.7186)
- **CB-CTT soft constraints**: RoomCapacity (students exceed seats), MinimumWorkingDays (a course spread over too few days), CurriculumCompactness (isolated lectures with no adjacent lecture of the same curriculum that day), RoomStability (a course split across rooms). — [arXiv 1409.7186](https://arxiv.org/pdf/1409.7186); [arXiv 1401.5156](https://arxiv.org/pdf/1401.5156)
- The official ITC-2007 description is the Di Gaspero, McCollum & Schaerf technical report. The "comp" dataset is the most used benchmark. Integer-programming work (Lach & Lübbecke) has proved optimality on some instances. — [QUB ITC2007 tech report](https://www.eeecs.qub.ac.uk/itc2007/curriculmcourse/report/curriculumtechreport.pdf) (fetch returned HTTP 503; the content is cited via the arXiv papers)
- A 2022 survey identifies six "standard" educational timetabling formulations with benchmarks and state-of-the-art results (bounds, techniques, run times). — [Ceschia, Di Gaspero, Schaerf: Educational Timetabling survey (arXiv 2201.07525)](https://arxiv.org/abs/2201.07525)
- Operational conflicts at registration: time conflicts must consider lecture, lab and recitation, and alternate-week patterns can falsely conflict. — [Ole Miss](https://olemiss.edu/encompass/students/common-registration-errors/)

### Inferences
- **Recommended UMIS approach**: interactive manual scheduling with live hard-constraint validation, plus an optional solver (CP-SAT or MIP, or a metaheuristic such as simulated annealing) to propose room and time assignments.
- **Hard checks on save**:
  - Room double-booking: overlap of (day ∩ time ∩ date range) for the same room
  - Instructor double-booking
  - Block-section/curriculum-cohort conflicts: PH "block sections" for regular students are the analogue of the ITC "curriculum" constraint
  - Room capacity ≥ section capacity; room type/features match the component (lab vs lecture)
  - Instructor availability; meeting pattern fits the term's or session's date range
  - Contact hours match the course definition (e.g. 3 lecture hours, or 3 lab hours = 1 unit — institution-configurable)
- **Soft/warn**: faculty load above policy (regular load and overload units), back-to-back across distant buildings, lunch-break gaps, minimum working days, and room utilization targets.
- **PH specifics**:
  - Sections are often "blocks" tied to a year level of a curriculum version.
  - Irregular students build schedules across blocks, so student-level conflict detection at enlistment is essential.
  - Saturday classes and evening/graduate slots are common.
  - Summer/midyear terms have compressed meeting patterns (e.g. daily meetings over 6 weeks, per the UPD summer definition in §6).
- **Faculty assignment entities**: `InstructorAssignment` (section, faculty, % responsibility, load units credited) and `FacultyLoadPolicy` (regular max, overload max, preparations count by rank or employment type).

### Gaps
- Exact ITC-2007 penalty weights were not verified (the tech report fetch failed). The commonly cited weights (capacity 1 per student, min working days 5 per day, compactness 2, room stability 1) come from my background knowledge, not a fetched source, and should be verified.
- No PH-specific source on scheduling practice (e.g. CHED contact-hour-to-unit rules) was retrieved.

---

## 6. Common edge cases (curriculum changes mid-program, shiftees/transferees, substitutions, irregular students, summer terms) and Philippine graduation/honors rules

### Takeaway
The PH-specific edge cases are documented in UP rules:
- shiftees' elective selection order for honors
- transferee credit validation (18 units/semester within 3 semesters)
- residency for honors (75% of units, 2 years immediately prior)
- underload justification affecting honors eligibility
- the summer term counted differently from regular semesters
- disciplinary bars to honors

Latin honors thresholds vary by HEI. UP's 1.20 / 1.45 / 1.75 is common, but CHED sets no uniform national cutoff (per secondary commentary).

### Cited Findings
- **UP Latin honors** (Revised UP Code Art. 410, amended 1983): absolute minimum weighted average of Summa 1.20, Magna 1.45, Cum Laude 1.75. All curriculum-prescribed subjects and qualifying electives are included. — [UPD OUR: Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- **Excess electives (UP honors)**:
  - Non-shiftees: the required number of electives in chronological order.
  - Shiftees, in priority order: (a) electives taken in the graduating program, chronologically; (b) electives from the previous program acceptable as electives, chronologically; (c) prescribed courses from the previous program that qualify as electives, chronologically.

  — [UPD Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- **Honors residency (UP)**: at least 75% of total academic units or hours completed in the University, and in residence for at least 2 years immediately prior to graduation (Art. 412). Only resident credit counts in the honors average (Art. 413). — [UPD Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- **Honors load rule (UP)**:
  - Candidates must have carried ≥15 units, or the curriculum's normal load, each semester/trimester (Art. 414)
  - Exceptions: health (UHS certificate), course unavailability (adviser certification plus class schedule), or employment (payroll/appointment papers)
  - Documents must be sworn and submitted **during the semester of underloading**

  — [UPD Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- **Honors disqualifiers (UP)**: a finding of cheating/dishonesty, or suspension of ≥1 year under conduct, fraternity or anti-sexual-harassment rules, bars honors regardless of average. — [UPD Graduation with Honors](https://www.our.upd.edu.ph/files/acadinfo/GRADUATION%20WITH%20HONORS.pdf)
- **Other PH honors thresholds**: UP Manila also uses 1.20 for summa. Some private HEIs use bands such as 1.00–1.25. A secondary commentary says CHED imposes no uniform national GWA cutoff and cites a CHED fallback requiring 75% of required subjects completed at the awarding institution. One lawyer site's figure (summa 1.00–1.45) conflicts with the others and is unreliable. — [UP Manila OUR](https://our.upm.edu.ph/node/350); [Respicio: Legal Requirements for Latin Honors](https://www.respicio.ph/commentaries/legal-requirements-for-granting-latin-honors-in-philippine-schools); contradicted by [lawyer-philippines.com](https://www.lawyer-philippines.com/articles/ched-guidelines-on-awarding-latin-honors-in-philippine-universities)
- **Summer/midyear (UPD)**: the academic year has 3 terms, two semesters plus a 6-week summer session; summer class work is "equivalent to class work in one semester". Rejoining students are those not enrolled in the immediately preceding semester, **excluding the summer session**. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Calendar drift**: the UPD catalogue glossary (sourced from the 2004–2010 catalogue) says the first semester starts in June. UP and many PH HEIs have since shifted to an August/September start. Calendar dates must be data, not rules. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf) (the shift itself is not cited here; see Gaps)
- **Trimester institutions**: DLSU runs three regular trimesters of about 14 weeks each. — [DLSU Academic Calendar](https://www.dlsu.edu.ph/?p=14587). Mapúa uses trimesters; its "I" grade must be completed within the next trimester. — [Mapúa Grading](https://support.mapua.edu.ph/kb/article/53/grading-system)
- **Shiftee admission (UP)** uses the Curriculum Weighted Average (courses creditable in the new program only). — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Second degree; Residence enrollment**: students with only thesis remaining, or only an INC or 4.0 to clear, enrol "for residence". — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Graduation (UP)**: the degree is awarded by the BOR on the recommendation of the faculty. A Certificate of Completion is issued while awaiting BOR conferment. — [UPD Glossary](https://our.upd.edu.ph/files/catalogue/GLOSSARY.pdf)
- **Degree Works "broken" exceptions**: exceptions break when the student's program or catalog changes, which is relevant to curriculum changes mid-program and to shiftees. — [Missouri State DW Guide](https://www.missouristate.edu/Registrar/_Files/DWUsersGuide516AULExceptions.pdf)

### Inferences (edge-case catalogue for the spec)
- **Curriculum revision mid-program**: students stay on their admit-term CurriculumVersion by default. Support (a) a bulk migration to a new version with a course-mapping table (old course → new course/elective slot), (b) an individual curriculum-version change with audit re-run, and (c) "phase-out" offering schedules. Keep historical grades linked to the original course code, and handle equivalence through `CourseEquivalency`, not by rewriting records.
- **Shiftee**: create a new StudentProgram row (keep the old one closed, with its reason). Credit evaluation maps prior courses into the new curriculum (auto via equivalency plus manual). Keep separate averages: overall GWA (all courses, UP definition), Curriculum WA, and honors WA with the elective-selection priority. Count MRR from first enrolment or per program (configurable).
- **Transferee**: `TransferCredit` records with source institution, course, grade and units, the mapped course, the evaluator and the validation deadline (UP: ≤18 units/semester, within 3 semesters). Transfer credit counts toward units for graduation but is excluded from resident averages and honors; it does count toward the 75% residency denominator.
- **Substitution/waiver**: a requirement-level exception per Degree Works types, with approver (department chair/dean) and reason; units waived vs substituted are tracked separately for the total-unit check.
- **Irregular students**: no block section. Enlistment is course-by-course with student-level conflict checks, prerequisite chains, and advising approval. Auto-flag irregular when load < curriculum normal load or the student is off-sequence.
- **Summer/midyear**: TermType with `is_regular = false`. It affects INC lapse counting, rejoining status, honors load rules (applied per semester/trimester), scholastic-standing evaluation, and a lower max load (e.g. 6–9 units; institution-configurable, not cited).
- **Repeats/retakes**: configurable policy for which attempts count in GWA (all/latest/best). UP's GWA "all subjects taken" definition implies all attempts count. Max attempts per course come from retention rules (e.g. UP Engineering: at most 2 Math failures).
- **INC chains**: INC → completed with 4.0 → 4.0 must be removed within the original INC window → final 3.0 or 5.0. The grade-history table must preserve every transition.
- **Cross-enrollment**: the home institution approves; the host grade is recorded as TransferCredit or a "cross-registration" enrollment. Its inclusion in residency and averages is configurable.
- **Graduation workflow**: application (deadline per term) → audit snapshot → department/college evaluation → clearance (library, accounting, guidance, discipline, college, registrar) → list of candidates → Academic Council/BOR approval → conferment date → diploma (unique number, Latin honor text) and TOR with "graduated on / degree conferred" annotation, Special Order number for CHED-supervised private HEIs (not cited; verify).
- **Honors engine**: compute honors WA per scheme direction, thresholds from policy, and checks for residency (75% units, 2 years), the load rule with approved underload justifications, grade floors (some HEIs require no grade below X or no failing/INC/DRP; varies), and disciplinary flags.

### Gaps
- CHED's current memorandum on Latin honors and on the academic calendar (e.g. the August opening and midyear term nomenclature) was not retrieved from a primary CHED source. The national rule set is unconfirmed.
- The UP calendar shift to August was not cited from a primary source in this session.
- CHED Special Order requirements for graduation of private HEI students were not researched in this session.
- No PH source was retrieved for the maximum load in summer terms, or for "graduating student" overload allowances.
- The Ateneo QPI scale and honors thresholds (A = 4.0 letter system) were not verified.
