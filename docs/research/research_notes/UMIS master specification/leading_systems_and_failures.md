# Leading Higher-Education SIS/ERP Systems: Scope, Module Structure, Data Model, and Implementation Failures

Research date: 2026-11-21. About 20 search/fetch calls. Primary vendor documentation was used where it was reachable: Oracle PeopleBooks, Workday course manuals, the OpenEduCat GitHub repo, and Ellucian press releases. Ellucian's Banner data dictionary is not public. Banner table facts below come from university-published ODS metadata and naming-convention guides, so they are secondary sources.

## 1. What modules do the leading products include, and how do they divide responsibilities?

### Takeaway
Every mature product separates the same layers:
1. A shared person/community layer (identity, bio-demo data, holds, checklists, communications).
2. An academic-structure and calendar foundation.
3. A curriculum layer: the course catalog, kept separate from scheduled class sections.
4. Admissions/recruiting.
5. Student records: enrollment, grades, transcripts, degree conferral.
6. Advising and degree audit.
7. Student financials: billing and accounts receivable.
8. Financial aid.
9. HR and finance, often in a separate suite.

The open-source products (OpenEduCat, Fedena) are K-12-style "school management" suites. They do not model institution, career, program, plan or term with the same rigor.

### Cited Findings

**Oracle PeopleSoft Campus Solutions (CS 9.2)**
- Campus Community Fundamentals is the shared base layer. Its documentation covers service indicators and the "3Cs — Communications, Checklists, and Comments" — [Oracle PeopleBooks, Campus Community Fundamentals](https://docs.oracle.com/cd/E56917_01/cs9pbr4/eng/cs/lscc/index.html); [Oracle, Managing Service Indicators](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lscc/htm/lscc39.htm)
- Term and session dates are shared across modules: "Student Financials, Financial Aid, and Student Records … all must use dates that match the dates set here," particularly withdrawal dates. Terms, sessions and time periods "affect class enrollment, financial aid, billing, tuition refunds, and statistical reporting" — [Oracle PeopleBooks CS 9.0, Establishing Terms and Sessions](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)
- Holiday schedules for terms and sessions are maintained in HRMS (the Holiday Schedule Table). This is a dependency from CS on the HR suite — [same source](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)
- Academic Advisement has a requirements engine that is set up in phases, for example "Phase Two: Setting Up Requirement Descriptions and Details" — [Oracle CS 9.2.038 Academic Advisement](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/phase-two-setting-requirement-descriptions-details.html)

**Workday Student**
- Workday Student course manuals are organized as Student Records and Advising, Student Financials, Student Recruiting and Admissions, and Organizations and Academic Foundation. Each functional manual begins with an "academic foundation review" — [Workday, Organizations and Academic Foundation](https://doc.workday.com/workday-education/en-us/course-manuals/student-for-administrators/organizations-and-academic-foundation.html); [Workday, Academic Foundation Review (Student Financials)](https://doc.workday.com/workday-education/en-us/course-manuals/student-financials-for-administrators/academic-foundation-review.html); [Workday, Academic Foundation Review (Recruiting & Admissions)](https://doc.workday.com/workday-education/en-us/course-manuals/student-recruiting-and-admissions-for-administrato/academic-foundation-review.html)
- Workday Student sits on the same tenant as Workday HCM and Financials. At Washington University in St. Louis, the Workday program (HR, Finance and Student) replaced about 80 legacy systems — [The Register, Dec 2025](https://www.theregister.com/2025/12/12/washington_university_workday_costs_revealed/)

**Ellucian Banner**
- Banner object names are seven characters long:
  - Position 1 is the system: S = Banner Student, G = Banner General.
  - Position 2 is the owning module.
  - Position 3 is the object type: B = base table, R = repeating table / rules / report, V = validation.
  - One institution's guide lists T, not V, as the validation code.
  - Sources: [UNM Banner Naming Conventions](https://artsci-da.unm.edu/sites/default/files/Banner%20Naming%20Conventions.pdf); [CCSU Banner Naming Conventions](https://www.ccsu.edu/it/files/banner/Banner_Naming_Conventions.pdf); [Stetson Banner page name conventions](https://www.stetson.edu/law/offices/it/media/banner_page_name_conventions.pdf); [U. South Alabama Banner Student object naming standards](https://meteorology.southalabama.edu/departments/registrar/resources/ellucian-training-materials/banner-student-getting-started-object-naming-standards.pdf)
- Banner Student tables live in the SATURN schema, for example SATURN.SORLCUR (student curriculum: department, major, etc.) and STVTERM (term validation table) — [Anthology help: Suggested Banner Tables](https://help.anthology.com/data-management/en/suggested-banner-tables.html)

**Anthology Student (formerly Campus Management / CampusNexus Student)**
- For CampusNexus Student versions 20.0–21.0, the analytics module covers the Academics, Admissions, Career Services, Financial Aid and Student Account modules. This is the closest available official module list — [Anthology Help, Student Analytics](https://help.anthology.com/IM/1.22/Content/Analytics/InstallingAnalytics.htm)
- Ownership has changed:
  - Anthology filed for Chapter 11 on 29 Sep 2025.
  - Ellucian was named successful bidder in November 2025 and closed the acquisition of Anthology's SIS and ERP business around 31 Dec 2025 to 5 Jan 2026.
  - The deal added more than 260 customers. Ellucian says it will keep maintaining the Anthology SIS/ERP products.
  - Sources: [Campus Technology, Jan 2026](https://campustechnology.com/articles/2026/01/05/ellucian-officially-acquires-anthologys-sis-and-erp-business.aspx); [Ellucian newsroom](https://www.ellucian.com/newsroom/ellucian-completes-acquisition-anthologys-sis-and-erp-business); [ERP Today](https://erp.today/ellucian-completes-anthology-sis-and-erp-acquisition-adding-260-higher-education-customers/)

**OpenEduCat (open source, Odoo-based)**
- The 19.0 branch contains these modules: openeducat_core, openeducat_admission, openeducat_activity, openeducat_assignment, openeducat_attendance, openeducat_classroom, openeducat_exam, openeducat_facility, openeducat_fees, openeducat_library, openeducat_parent, openeducat_timetable, plus the openeducat_erp meta-module and a web theme.
- The license is LGPL-3.0.
- Source: [GitHub openeducat/openeducat_erp](https://github.com/openeducat/openeducat_erp)

**Fedena (open-source core)**
- Core modules are Student Admission, Student Information, Student Attendance, Timetable, Examination, Finance and Human Resources, with paid add-on modules on top — [LinuxLinks: Fedena](https://www.linuxlinks.com/fedena/); [Fedena add-on modules](https://fedena.com/feature-tour/addon-modules)
- Fedena's own marketing says the core is free and open source. Competitor OpenEduCat describes it as only "partial" open source, with paid tiers of $999–$2,299 per year. That comparison is biased — [Fedena 101 reasons](https://fedena.com/101-reasons); [OpenEduCat compare page](https://openeducat.org/compare/fedena/)

### Inferences
- A complete UMIS scope, based on where the vendors draw their boundaries:
  1. Core/Community: person, organization, addresses, IDs, holds, checklists, communications, comments, security.
  2. Academic Foundation: institution, campus, academic organization/unit, career/level, program, plan, subplan, calendar, term, session.
  3. Curriculum/Catalog: subjects, courses, requisites, course versions.
  4. Class Scheduling: sections, meeting patterns, rooms, instructors.
  5. Recruitment and Admissions.
  6. Student Records: matriculation, program/plan stack, enrollment, grading, transcripts, graduation.
  7. Advising and Degree Audit.
  8. Student Financials: tuition/fee rules, billing, payments, accounts receivable.
  9. Financial Aid / Scholarships.
  10. HR and Payroll.
  11. Finance / General Ledger.
  12. Facilities, Library and LMS integrations.
  13. Reporting/Analytics.
- OpenEduCat and Fedena show that a lightweight suite covers admissions, timetable, attendance, exams, fees and library. Neither has a multi-career, effective-dated academic structure or a rules-based degree audit, and both are weak for a degree-granting university.
- After the Ellucian–Anthology deal, Ellucian owns Banner, Colleague and Anthology Student. Vendor consolidation is a longevity risk for any buyer.

### Gaps
- No public Ellucian document listing current Banner modules was retrieved. Banner's Student, Financial Aid, Finance, HR/Position Control, Advancement and General modules are widely known, but were not verified from a primary source in this session.
- No current official Anthology Student module catalog was found.
- Workday Student has no public data model. Its structure is inferred from course manuals and university glossaries.

## 2. What are the core data entities and their relationships?

### Takeaway
All the major systems use the same core chain:
- Institution → organizational units → career/level → program → plan (major) → subplan (concentration)
- Program → credential/degree
- Subject → course (catalog) → class/section in a term or session, with meeting patterns
- Student enrollment in a section, then grades and transcript

Plus a shared person record keyed by an internal ID (PeopleSoft EMPLID, Banner PIDM). Catalog vs. section and term vs. session are universal splits. Student academic data is effective-dated by term.

### Cited Findings

**PeopleSoft academic structure**
- Oracle states these relationships:
  - "An academic institution can have many campuses."
  - "Academic programs are part of academic careers and the academic institution."
  - "Subject areas are part of academic organizations and the academic institution."
  - "Academic plans and academic subplans are subdivisions of academic programs."
  - "Degree records are directly linked to academic plans."
  - "Courses and classes are subdivisions of subject areas and directly linked to terms and sessions."
  - Source: [Oracle CS 9.2, Understanding Academic Structure](https://docs.oracle.com/cd/G11181_01/cs92pbr35/eng/cs/lsfn/UnderstandingAcademicStructure-ab5851.html)
- Terms are linked to academic careers: "different academic careers at an institution can have different term structures." A term is "an administrative time period within which sessions are defined, students are billed, and statistics are accumulated." A session subdivides a term "into multiple time periods in which to offer classes" — [Oracle, Establishing Terms and Sessions](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)
- Program, plan and subplan:
  - The program is the entity a student applies to and graduates from.
  - A plan is a major, minor or certificate.
  - A subplan is an emphasis or concentration.
  - A student has a "program/plan stack" grouped by academic career and Student Career Number.
  - A valid plan is required to term-activate a student.
  - Sources: [University of Colorado, PS Campus Solutions Glossary](https://www.cu.edu/blog/irm-updates/ps-campus-solutions-glosarry); [Pitt, PS Student Program/Plan Guide](https://registrar.pitt.edu/sites/default/files/pdf/PS%20Student%20Program_Plan%20Guide.pdf); [UNI, PeopleSoft Academic Structure Terminology](https://uni.edu/sis/sites/default/files/inline-uploads/Quick%20Reference%20-%20PeopleSoft%20Academic%20Structure%20Terminology.pdf)
- Records on the term table:
  - Fields: term begin/end dates, Academic Year (for reporting and financial-aid accumulation), Weeks of Instruction, Sixty Percent Point in Time (refunds), Max Program Effdt for Term, Transcript Date Print, self-service display flags.
  - The Term Values Table holds term numbers, which must be sequential. Oracle advises "increments of two or three so that you can insert additional terms" later.
  - "Last Class Nbr" sets the starting point for class numbering, with large gaps between terms so students do not reuse a prior term's class number.
  - Source: [Oracle, Establishing Terms and Sessions](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)
- Records on the session table:
  - Fields: begin/end dates (defaults for class sections), first/last date to enroll (enforced by the enrollment engine), open enrollment date, last date for wait list, census date (informational only), sixty-percent point, and an "enrollment control session" that caps total units across the term's sessions.
  - Session Time Periods and the Time Period Table define landmark dates. These secure enrollment functions and control drop retention or deletion through Enrollment Action Reasons.
  - Oracle warns: "If you do not enter any time periods … the system denies access to enrollment functions."
  - Source: [same source](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)

**Workday Student academic foundation**
- Educational institution: one tenant can hold several institutions. An academic unit is designated an institution separately, and the designation cannot be removed once objects are associated with it.
- Academic unit: a college, school or department with a subtype, arranged in a single superior-unit hierarchy. Units control data ownership and security. Each unit is configured to admit students, offer courses, offer programs and recruit. Subordinate units inherit roles and business processes.
- Academic unit hierarchies: separate rollup trees for reporting and routing.
- Academic level: undergraduate, graduate, etc. Each unit-and-level combination carries the admit/offer/recruit configuration. If a unit is not configured for a level, the next superior unit with that configuration performs those functions.
- Calendar chain: period types → academic calendar (a template) → academic year (dated) → academic periods. Periods are fixed, dynamic or nonstandard. Calendar policies are effective-dated and assigned to a unit or program of study.
- Program of study (POS): a major, minor or certificate. It has an owning unit and level, a POS type and a code, grants educational credentials (degree, certificate, badge, license, award), and can be "addable" or "stackable". It has first and last entry dates.
- Source for all of the above: [Workday, Organizations and Academic Foundation](https://doc.workday.com/workday-education/en-us/course-manuals/student-for-administrators/organizations-and-academic-foundation.html)
- A course section is a specific offering of a course for one academic period, with a meeting pattern. A student can have one or more academic records, each with one or more programs of study, holding GPA, registrations and history. At WashU, the program of study replaced the legacy "academic division" in many cases — [Workday Student Glossary, LSU](https://lsue.edu/workday-resources/glossary.php); [Bowdoin glossary](https://www.bowdoin.edu/workday/workday-erp/workday-student-glossary.html); [WashU Sunrise Foundations](https://sunrise.wustl.edu/workday-student/foundations/page/2); [Miami University terminology](https://miamioh.edu/workday-info/terminology.html)
- A Student Financials Period Record is created automatically at matriculation, based on the primary POS's anticipated dates. None is created for applicants — [Workday, Organizations and Academic Foundation](https://doc.workday.com/workday-education/en-us/course-manuals/student-for-administrators/organizations-and-academic-foundation.html)

**Banner**
- Records are keyed by PIDM, an internal person identifier. SGBSTDN (the general student record) is keyed by SGBSTDN_PIDM plus SGBSTDN_TERM_CODE_EFF, an effective term — [Missouri State Banner ODS metadata, AS_GENERAL_STUDENT_COMP](https://prodssb.missouristate.edu/metadata/AS_GENERAL_STUDENT_COMP_target.html)
- SFRSTCR (student course registration) carries SFRSTCR_PIDM, SFRSTCR_TERM_CODE, SFRSTCR_CRN ("Computer assigned internal unique number for the schedule offering"), SFRSTCR_CREDIT_HR and SFRSTCR_BILL_HR. Credit hours and billing hours are stored separately — [Toledo Banner ODS metadata, STUDENT_COURSE_ODS](https://reports.utoledo.edu/metadata/metadata85/STUDENT_COURSE_ODS_target.html); [Northeastern ODS metadata](https://bnrordsp.neu.edu/metadata_nfs/STUDENT_COURSE_ODS_target.html)
- SSBSECT is the section/schedule table, with columns such as SSBSECT_GRADABLE_IND and SSBSECT_PRIOR_ENRL — [Northeastern ODS, AS_COURSE_OFFERING_COMP](https://bnrordsp.neu.edu/metadata_nfs/AS_COURSE_OFFERING_COMP_target.html)
- SORLCUR holds learner curriculum (level, program, college, major, etc.). Rows are sequenced, so the latest row may need to be found through SORLCUR_SEQNO. STVTERM is the term validation table to "use in term logic" — [Anthology help: Suggested Banner Tables](https://help.anthology.com/data-management/en/suggested-banner-tables.html)
- SFRSTCR holds only the most recent record per student enrollment. Registration history is kept separately in an audit table (Banner ODS exposes STUDENT_COURSE_REG_AUDIT) — [Anthology help](https://help.anthology.com/data-management/en/suggested-banner-tables.html); [Toledo ODS, STUDENT_COURSE_REG_AUDIT](https://wrl.utoledo.edu/metadata/metadata92/STUDENT_COURSE_REG_AUDIT_ODS_target.html)

**OpenEduCat**
- The core module carries the student, faculty, course, batch and subject entities. Admission, timetable, exam and fees each extend this core, per the repo's module layout — [GitHub openeducat_erp](https://github.com/openeducat/openeducat_erp)
- Entity-level detail was not fetched. Only the module names are confirmed.

### Inferences
- A UMIS core entity list built from the cross-vendor common denominator:
  - **Foundation:** Institution, Campus, AcademicOrganization/Unit (a hierarchy), AcademicCareer/Level, AcademicGroup/College, Subject.
  - **Credentials:** Program, Plan (major/minor/certificate), Subplan (specialization), Degree/Credential.
  - **Calendar:** AcademicCalendar, AcademicYear, Term, Session, TimePeriod/Deadline.
  - **Curriculum and scheduling:** Course (catalog, versioned), CourseRequisite, ClassSection (term/session plus CRN/class number), MeetingPattern, Room/Facility, InstructorAssignment.
  - **Person and student:** Person (internal surrogate ID separate from the public student number), PersonName/Address/Contact (history kept), StudentCareer/AcademicRecord, StudentProgramPlan (effective-dated stack), TermActivation.
  - **Enrollment and outcomes:** Enrollment (credit hours separate from billing hours), Grade, TranscriptEntry, TransferCredit, DegreeConferral.
  - **Student services and finance:** Hold/ServiceIndicator, Checklist, Communication, Comment, Application (admissions), StudentAccount and charges, AidAward.
- Credit hours and billing hours should be separate fields on enrollment (Banner does this). In the Philippine context, this lets lab, NSTP and tutorial units bill differently from academic units.
- Term numbering should leave gaps or use sortable codes (Oracle advice). Section numbers should be unique across terms so a stale CRN or class number cannot be used.
- "Program" (what you are admitted to and graduate from) and "Plan" (major) are separated in both PeopleSoft and Workday. Workday flattens them into a program of study plus credential. UMIS must decide whether a Philippine "degree program" such as "BS Accountancy" is a Program, a Plan, or both. In CHED terms a single program usually maps 1:1, but majors/specializations such as "BSEd major in Math" map to Plan or Subplan.

### Gaps
- Exact Banner column-level definitions were not verified from Ellucian primary sources for SPRIDEN (identity/names), SPBPERS (bio-demo), SCBCRSE (course catalog), SHRTCKN (academic history), SPRHOLD (holds), SOBTERM (term controls), SARADAP (admissions application) and TBRACCD (AR detail). These are commonly cited Banner tables but are unverified in this session.
- PeopleSoft record names (e.g. ACAD_PROG, ACAD_PLAN, CLASS_TBL, STDNT_ENRL, CRSE_CATALOG) were not retrieved from a primary source.

## 3. What foundational setup must exist before transactions, and in what order?

### Takeaway
Setup follows the dependencies:
1. Security and core configuration.
2. Institution, campus and organizational hierarchy.
3. Careers/levels.
4. Calendars, terms and sessions (with deadlines and time periods).
5. Subjects and the course catalog.
6. Programs, plans, subplans and degrees.
7. Fee, aid and enrollment rules.
8. Person records.
9. Admissions and matriculation.
10. Class schedules.
11. Enrollment.
12. Grading, billing and aid.

Vendors explicitly require the academic foundation to be finished first.

### Cited Findings
- Oracle: "Set up your academic structure before using the full functionality of the PeopleSoft Campus Solutions system. Make sure that you understand how the institution structures campuses, academic careers, academic organizations, academic departments or groups, and subject areas" — [Oracle, Understanding Academic Structure](https://docs.oracle.com/cd/G11181_01/cs92pbr35/eng/cs/lsfn/UnderstandingAcademicStructure-ab5851.html)
- Oracle's Academic Advisement requirements guidance says to begin "at the highest level, which is your institution" — [Oracle, Academic Advisement setup](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/academic-advisement/phase-two-setting-requirement-descriptions-details.html)
- Hard dependencies on the PeopleSoft time structure:
  - Each term must have at least one session.
  - Session dates default class-section dates. Oracle warns that "the system does not validate against term begin and end dates."
  - Session Time Periods must exist or enrollment functions are denied.
  - Holiday schedules come from HRMS.
  - Sources: [Oracle, Establishing Terms and Sessions](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm); [CU glossary](https://www.cu.edu/blog/irm-updates/ps-campus-solutions-glosarry)
- Workday's explicit order:
  - Period types, then calendars (with optional holiday calendars), then academic years, then periods.
  - Academic units are created and then linked to superior units, then levels are configured per unit.
  - Calendars must exist before they are assigned to units or programs.
  - POS types come before programs of study.
  - An institution designation cannot be removed once objects reference it, so it must be decided correctly up front.
  - Source: [Workday, Organizations and Academic Foundation](https://doc.workday.com/workday-education/en-us/course-manuals/student-for-administrators/organizations-and-academic-foundation.html)
- Each Workday functional track (Admissions, Student Financials, Records) starts with an "academic foundation review", which signals that the foundation is a prerequisite for all of them — [Workday, Academic Foundation Review](https://doc.workday.com/workday-education/en-us/course-manuals/student-financials-for-administrators/academic-foundation-review.html)
- WashU's Workday Student program ran a Discovery Phase from April 2020 to August 2021 before build, then took staged go-lives through the 2024–25 academic year. Foundations work was a distinct workstream — [WashU Sunrise, Discovery Phase](https://sunrise.wustl.edu/?p=450); [WashU Sunrise Foundations](https://sunrise.wustl.edu/workday-student/foundations/page/2)
- Common practice is phased go-lives with HR/Finance before Student:
  - Minnesota State planned HR/payroll for July 2023 and Student for fall 2026, later revised to July 2024 and fall 2029.
  - Edinburgh launched HR in 2020, then payroll, then finance.
  - Sources: [The Register, Apr 2026](https://www.theregister.com/off-prem/2026/04/08/minnesota-payroll-problems-grew-after-workday-say-auditors/5221270); [Panorama, Edinburgh case](https://www.panorama-consulting.com/edinburgh-universitys-failed-implementation/)

### Inferences
Recommended UMIS build and dependency order:
1. Platform: identity and access (RBAC), audit log, code/validation tables, numbering sequences.
2. Organization: institution, campuses, colleges, departments (effective-dated hierarchy).
3. Careers/levels (e.g. Basic Ed / SHS / Undergraduate / Graduate / Law / Medicine, if relevant).
4. Calendar: academic years, terms (semesters/trimesters/summer), sessions, deadlines and time periods.
5. Curriculum: subjects, course catalog (versioned), requisites, equivalencies.
6. Programs, plans, subplans and degrees, plus curriculum/prospectus requirements (needed before degree audit).
7. Person/bio-demo with holds, checklists and communications.
8. Admissions: application, evaluation, admit, matriculate. This creates the student career/program record.
9. Class schedule: sections, rooms, faculty load (needs HR faculty records).
10. Fee/tariff rules (need term, career, program and course).
11. Registration/enrollment (needs holds, term activation, sections and fee rules).
12. Billing and payments, then aid/scholarships.
13. Grading, transcripts, academic standing, graduation.
14. Analytics and regulatory reporting.

HR (employee and faculty records) is needed before scheduling faculty load. GL/finance is needed before posting student-account revenue.

### Gaps
- No vendor-published end-to-end "implementation sequence" document was found. The order above is built from documented dependencies.

## 4. How do they handle effective dating, holds/service indicators, checklists, communications, and audit history?

### Takeaway
- **Effective dating** is pervasive. PeopleSoft effective-dates setup rows and some student data. Banner effective-dates student data by term (`TERM_CODE_EFF`). Workday effective-dates calendar policies.
- **Holds** are configurable codes with separate "impacts" (which services are blocked), reasons, date- or term-based validity, amounts, placing office and release security. Release history is kept.
- **Checklists, communications and comments** form a shared "3C" layer attached to any person or organization.

### Cited Findings
- PeopleSoft effective-dated setup is live: "If a new effective-dated row is added to a service indicator definition, the changes to that row will affect existing assignments to IDs as well as new assignments" — [Oracle, Managing Service Indicators](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lscc/htm/lscc39.htm)
- The term begin date serves as the term's effective date. "Max Program Effdt for Term" is the latest effective date a program/plan change can carry and still count for term activation in that term — [Oracle, Establishing Terms and Sessions](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lsfn/htm/lsfn07.htm)
- Banner's general student record is effective by term (SGBSTDN_TERM_CODE_EFF). Curriculum rows in SORLCUR are sequenced (SORLCUR_SEQNO) rather than overwritten — [Missouri State ODS metadata](https://prodssb.missouristate.edu/metadata/AS_GENERAL_STUDENT_COMP_target.html); [Anthology help: Suggested Banner Tables](https://help.anthology.com/data-management/en/suggested-banner-tables.html)
- Workday calendar policies are effective-dated, so calendars can change without affecting prior academic years. Unit policies inherit down the hierarchy — [Workday, Organizations and Academic Foundation](https://doc.workday.com/workday-education/en-us/course-manuals/student-for-administrators/organizations-and-academic-foundation.html)

**PeopleSoft service indicator model** (source for this list: [Oracle, Managing Service Indicators](https://docs.oracle.com/cd/E17221_01/cs9pbr2/eng/psbooks/lscc/htm/lscc39.htm))
- Effect is Positive or Negative.
- Indicators are made of one or more service impacts, for example registration, transcript, or enrollment verification.
- Impacts are term-based or date-based. Start Term 0000 means all terms, 9999 means never. With no end term or end date, the indicator lasts until released.
- Each assignment records:
  - A reason code (limited to the reasons valid for that indicator).
  - Amount and currency needed to clear it.
  - Contact person, placed-by, department, reference and comments.
  - Placed method (manual, background or mass) and placed process.
- Release:
  - Manual release requires release security for the institution, indicator and reason.
  - Automated or mass release processes are available (SCC_SI_RELS).
  - "The service indicator assignment and release will remain part of the service indicator audit history."
- Mass assignment works by equation, external file or query.
- Campus Self Service shows students only negative indicators, labeled "Holds" — [Oracle CS 9.2.038, Self-Service Service Indicators](https://docs.oracle.com/en/applications/peoplesoft/campus-solutions/9.2.038/campus-self-service/using-self-service-service-indicators-data.html)
- Institutional practice is that only the office that placed an indicator may remove it — [FSCJ training: Service Indicators and Checklists](https://training.fscj.edu/images/pdfs/cs/intro_serv_indic_checklists.pdf)
- PeopleSoft groups Communications, Checklists and Comments as the "3Cs" in Campus Community, with separate setup for each — [Oracle Campus Community Fundamentals index](https://docs.oracle.com/cd/E56917_01/cs9pbr4/eng/cs/lscc/index.html)

### Inferences
- Holds design for UMIS: a HoldType (code) with many HoldImpact rows (registration, grades view, transcript/TOR release, graduation clearance, enrollment certification). A PersonHold assignment carries reason, amount, office, placed-by, method, start/end (term or date) and release info. History is append-only, never deleted. This directly supports Philippine "clearance" processes, such as library, accounting and registrar clearance before TOR or diploma release.
- Effective dating should be applied to setup tables (org units, programs, plans, courses, fee rules) and to student academic status (the program/plan stack by effective term). Transactional rows (enrollments, charges) should be immutable with reversal entries, and backed by a separate audit log.
- The 3C pattern (Checklist templates and assigned checklist items with due dates and status; communication templates and logged communications; categorized comments) can serve admissions requirements, enrollment document submission and graduation requirements.

### Gaps
- The full text of PeopleSoft's 3C chapters (checklist item statuses, communication generation and letter codes) and Banner's SPRHOLD/STVHLDD hold structures was not retrieved.
- Banner audit-trail mechanics were not verified.

## 5. What are the well-documented failure points and lessons from university SIS/ERP implementations?

### Takeaway
Failures cluster around:
- Under-scoped budgets and timelines (costs routinely 1.5x to 5x the plan).
- Customization caused by departments resisting standardization.
- Immature process definition before build.
- Weak governance that ignores red flags.
- Interfaces and partial cutovers between legacy and new systems.
- Inadequate testing and load testing.
- Poor usability and training for non-specialist users.
- Payroll and financial-aid errors that directly harm people.

### Cited Findings

**Minnesota State (Workday, NextGen)**
- Scale: 54 campuses, about 270,000 students.
- Budget: $151.1M initially, $242.7M after the 2020 contract award, and $290.4M by November 2024, due to scope additions, extended timelines and contingency.
- Schedule: Student moved from fall 2026 to fall 2029.
- The Office of the Legislative Auditor found:
  - 19 of 202 sampled faculty were paid inaccurately, plus 38 more found in additional testing, and late pay.
  - Faculty payroll calculation was not included in Workday, so pay is produced across Workday, the legacy ISRS system and SEMA4.
  - Interface problems arose between ISRS and Workday.
- Workday responded that scope changes and cost increases are "routine" at this scale.
- Source: [The Register, 8 Apr 2026](https://www.theregister.com/off-prem/2026/04/08/minnesota-payroll-problems-grew-after-workday-say-auditors/5221270)

**Washington University in St. Louis (Workday HCM/Finance/Student)**
- Total cost is about $265–266M over at least seven years, around $16,000 per student. The figure was disclosed after student protests.
- The program replaced about 80 legacy systems.
- Sources: [The Register, Dec 2025](https://www.theregister.com/2025/12/12/washington_university_workday_costs_revealed/); [Student Life, Dec 2025](https://www.studlife.com/news/2025/12/10/breaking-down-workdays-265-million-cost)

**SUNY Erie Community College (Workday)**
- The college says Workday "has been a failure" that cost over $12M in five years. It approved $5.2M to move to Ellucian Banner.
- Source: [GovTech](https://www.govtech.com/education/higher-ed/erie-community-college-to-spend-5-2m-replacing-disastrous-erp-system)

**University of Edinburgh ("People and Money", Oracle ERP/HCM Cloud)**
- Contract: £25M, final cost £37M.
- Problems after the finance go-live:
  - Late PhD stipends and supplier payments.
  - Staff working in spreadsheets.
  - Thousands of mis-coded transactions, with more than £300k misallocated.
  - A system designed for users with financial training.
- Causes cited:
  - Processes flagged "red" for immaturity but the project proceeded anyway.
  - Leadership ignored warnings.
  - Weak change management and training.
  - Timeline-driven governance.
- Source: [Panorama Consulting case study](https://www.panorama-consulting.com/edinburgh-universitys-failed-implementation/) (a consultancy blog drawing on The Register reporting)

**CIO.com, "University ERP: Big Mess on Campus"** (source for all items below: [CIO.com](https://www.cio.com/article/272120/enterprise-resource-planning-university-erp-big-mess-on-campus.html))
- UMass Amherst (PeopleSoft "Spire"): the system crashed the day before classes and was down 4 days. About 1,000 password-reset requests overloaded it because no load testing had been done.
- Stanford (PeopleSoft HR/Student, Oracle Financials):
  - Productivity fell compared with the mainframe.
  - Departments resisted standardization, which led to costly customizations.
  - The new systems cost more to support than the legacy systems.
  - The CFO said they "tried to do too much in too little time."
- Indiana University: a buggy ERP wrongly denied financial aid to about 3,000 students, and emergency loans had to be issued.
- Cleveland State (PeopleSoft): the university alleged the software was "virtually unusable" and blocked receivables collection. The settlement with Oracle was estimated at $4.25M.
- Northeastern: bought 22 PeopleSoft modules for a Y2K deadline and the project derailed. The recovery cut scope to one HR module and used middleware to keep the legacy mainframe.
- A survey cited (without sample details) found university ERP projects cost about 5x the projected price.
- A dissertation cited in a secondary review found higher-education ERP projects overrun budgets about 50% of the time. Unverified — [Bettera research review](https://www.bettera.co/post/higher-education-erp-failure-research)
- Analogous public-sector case: Birmingham City Council's Oracle Fusion went from about £19M to £108M. Officers "had no idea what they were buying", and there was a failure to invest in implementation capacity — [The Register, Feb 2025](https://www.theregister.com/2025/02/25/birmingham_oracle_latest/)

### Inferences
Design and implementation lessons for UMIS:
1. **Standardize processes before build.** Treat "fit to standard" as a governance rule, and make customization requests go through a board (Stanford, Edinburgh).
2. **Phase scope and avoid big-bang module counts.** Northeastern's 22 modules is the cautionary example. Deliver the foundation and Student Records first, then add modules.
3. **Do not leave critical calculations outside the system.** Minnesota State's faculty pay is the example. Avoid long-lived dual-running legacy interfaces, and give each interface an owner, a reconciliation report and an end date.
4. **Test at load for registration and term start.** Include password-reset and enrollment surges. Enrollment periods are Philippine SIS peak load (UMass).
5. **Build usability for non-specialist users** such as faculty and department staff (Edinburgh).
6. **Run financial aid and payroll calculations in parallel** against legacy before cutover, because errors directly harm students and staff (Indiana, Minnesota State).
7. **Treat data migration as a workstream of its own,** with data cleansing of person records, curriculum history and AR balances.
8. **Set honest TCO budgets with contingency** and publish them early. WashU's disclosure came only under protest.
9. **Watch vendor consolidation.** The Ellucian–Anthology deal shows that product roadmaps can shift through M&A. Owning the data model reduces lock-in.

### Gaps
- No primary state-auditor PDF was retrieved. The Minnesota OLA figures come via The Register.
- Ohio State's reported 2022 abandonment of Workday Student was not confirmed from a primary source in this session.
- No EDUCAUSE quantitative study on SIS implementation success rates was retrieved.
- Some well-known cases were not researched here: Cal State's PeopleSoft, Oregon/Sheridan College, and UK and Irish SITS/Banner projects. A €10.6M unfinished Irish university student-records system appears only in an aggregator — [Archyde](https://www.archyde.com/irish-university-spends-e10-6m-on-unfinished-student-records-system/) — and is unverified.
- No Philippine-specific SIS failure post-mortems were found. This was out of scope for this subtopic.
