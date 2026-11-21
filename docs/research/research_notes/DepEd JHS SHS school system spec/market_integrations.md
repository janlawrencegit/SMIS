# Market, Parent Communication, and Integrations for a PH JHS–SHS School Management System

Research date: 2026-11-21. Method: web search and fetch, about 16 tool calls. Most vendor and pricing figures come from vendor marketing pages or third-party blogs. Teacher-forum and blog material is marked **(anecdotal)**. A search-summary layer sat between me and some sources, so verify figures marked "verify" against the original page before quoting them in a spec.

## 1. School management systems used by PH private and public high schools: modules, pricing, complaints

### Takeaway
The PH market is crowded with small local SaaS vendors. Nearly all advertise DepEd School Form (SF1–SF10) generation, grading sheets and parent portals. They price per student per month (about ₱95–₱130) or as flat annual or custom-build fees. Private schools are the buyers. Public schools still run on DepEd's own systems (LIS/EBEIS) plus Excel templates, and vendors themselves say official LIS submission stays on DepEd's systems. I found no independent reviews or teacher-forum complaints about specific PH vendors.

### Cited Findings
- **OceanEd** markets DepEd SF1–SF10 support and a parent portal. Pricing starts at ₱130 per student per month, with volume discounts — [OceanEd pricing](https://theoceaned.com/pricing); [OceanEd PH page](https://theoceaned.com/school-management-system-philippines)
- **Academe (academe.ph)** charges ₱95 per student per month and offers a free year for up to 100 students — [Academe](https://academe.ph/)
- **SmartEskwela**'s Basic plan is ₱19,999/year and includes a parent portal. It handles Form 137 requests and school-form generation — [SmartEskwela](https://smarteskwela.com/)
- **VenderIT** sells custom builds from ₱99,000, including hosting, domain, training and one year of support. This is the one-off custom-development model — [VenderIT](https://www.venderit.com/solutions/business-systems/school-management-system)
- **Schoolites** quotes by enrolment size, about US$0.75 per student per month internationally. It says official DepEd LIS/EBEIS submissions remain on DepEd systems, so vendors complement LIS rather than replace it — [Schoolites](https://schoolites.com/school-management-system-philippines)
- **Scholaris** positions itself as a K-12 SMS built for Philippine **private** schools — [Scholaris](https://scholaris.online/)
- **OpenEduCat**, an international open-source ERP, has a Philippines landing page — [OpenEduCat PH](https://openeducat.org/solutions/school-management-system-philippines/)
- **Sigasig** (commercial, not official) claims a "DepEd-aligned" school workspace with an automated e-Class Record (ECR), automated transmutation and SF1–SF9 support — [Sigasig](https://sigasig.online/)
- **deped.me** is a commercial blog/product pitching SF9/SF10 automation for 2026 against manual filling. It claims a MATATAG 25-50-25 weighting (WW/PT/term assessment), which conflicts with other template sites (see §2) — [deped.me](https://deped.me/blog/sf9-sf10-automation-class-record-deped-2026)
- One aggregator claimed SaaS versions cost ₱250–₱800 per student per **year**. That doesn't match the vendor pages above (₱95–₱130 per student per **month**), so treat it as unreliable — (search-summary note; source not retained)

### Inferences
- Typical SaaS price points are ₱95–₱130 per student per month. For a 1,000-student school that is about ₱1.1M–₱1.6M per year, which is a lot for small private schools. That likely explains the flat-fee (₱20k/yr) and one-off custom-build (₱99k+) models.
- Common modules across vendors: enrollment/admissions, student records (Form 137/SF10), grading sheets with DepEd transmutation, SF form generation, a parent portal, and fees/billing. Differentiators are SF form accuracy against the current DepEd order and the parent/mobile experience.
- Since official LIS submission stays on DepEd systems, the main value is less duplicate work: generate SF forms and LIS-ready exports from one data entry.

### Gaps
- I found no independent user reviews (Capterra/G2) or teacher-forum complaints about named PH vendors. Market share and adoption counts are also unknown.
- I didn't verify international products' PH presence (PowerSchool, Fedena, Edsby, etc.) or the pricing of the main university/college ERPs (e.g., Orange Apps, Edusuite).

## 2. What public school teachers use today for grades and forms, and the documented pain points

### Takeaway
Public school teachers combine DepEd's LIS (enrollment, LRNs, some school forms) with DepEd/third-party Excel e-Class Record (ECR) templates and Excel SF9/SF10 files. Several SFs are still partly or fully manual. Workload is a documented national issue: DepEd cut required teacher forms from 174 to 75 in 2025 and moved administrative tasks off teachers in 2024. The 2026 shift to a three-term calendar and new grading rules means templates keep changing. Any system must make weights and transmutation configurable.

### Cited Findings
- **Paperwork reduction:** DepEd announced a 57% cut, from 174 school forms to 75. Teachers regularly complete only 5 forms, plus up to 31 for additional tasks and 39 for teaching-related duties depending on role — [PhilStar, Mar 18 2025](https://www.philstar.com/headlines/2025/03/18/2429175/deped-reduce-teachers-paperwork-57); [Inquirer](https://newsinfo.inquirer.net/2044603/deped-set-to-reduce-public-school-teachers-paperwork-by-57/amp); [Tribune](https://tribune.net.ph/2025/03/17/deped-eases-teachers-reports-forms-burden). Reports cite the order number inconsistently (DO 005 s.2024 vs a 2025 "Streamlining School Forms" order; see [ilovedeped DO 006 s.2025](https://www.ilovedeped.net/2025/03/blog-post-deped-order-no-006-s-2025.html)), so verify it on deped.gov.ph.
- **DO 2, s. 2024** directs immediate removal of administrative tasks from public school teachers. Personnel, property custodianship, finance, records management, feeding and DRRM programs move to school heads and non-teaching staff — [DepEd DO 2 s.2024 PDF](https://www.deped.gov.ph/wp-content/uploads/DO_s2024_002.pdf); [ResearchGate analysis](https://www.researchgate.net/publication/402001142_Removing_Administrative_Tasks_Restoring_Instructional_Focus_Implications_of_DepEd_Order_No_2_s_2024_for_Teacher_Empowerment_Instructional_Quality_and_School_Readiness)
- **Workload data:** 42% of teachers work more than 50 hours per week, with an average of 17.8 hours on ancillary duties and 8.1 hours on program-related tasks (study cited in the 2025 coverage) — [PhilStar](https://www.philstar.com/headlines/2025/03/18/2429175/deped-reduce-teachers-paperwork-57); see also [NASH on EDCOM II findings](https://nash.com.ph/blog/teacher-workload-accountability-edcom-ii)
- **2026 policy changes:** Template sites cite **DO 9, s. 2026** ("Guidelines on the Implementation of the Three-Term School Calendar in Basic Education") and a **new transmutation table** for SY 2026–2027 ECRs — [TeachPinas ECR templates](https://www.teachpinas.com/e-class-record-deped-ecr-templates/). Another source cites **DO 015, s. 2026** as the updated classroom assessment, grading and awards policy, superseding DO 8 s.2015 and DO 36 s.2016 (search-summary; verify on deped.gov.ph).
- **Conflicting weights (verify against the official DO):** TeachPinas lists WW/PT/TE at 20/50/30 for ENG, FIL, MATH, SCI, AP and GMRC/Values (Grades 4–10), and 20/60/20 for EPP/TLE/MAPEH. An alternate ST1/ST2/TE scheme is 30/30/40. SHS weights aren't stated — [TeachPinas](https://www.teachpinas.com/e-class-record-deped-ecr-templates/). deped.me claims 25-50-25 — [deped.me](https://deped.me/blog/sf9-sf10-automation-class-record-deped-2026)
- **Third-party Excel ecosystem:** MATATAG ECR templates with automated MPS (mean percentage score) analysis — [Educators' Files](https://educatorfiles.com/matatag-e-class-record-ecr-templates-with-test-result-analysis/); official MATATAG ECR redistributed — [DepEd Click](https://www.deped-click.com/2025/06/deped-official-e-class-record-matatag.html); [DepEdLibre](https://depedlibre.com/deped-matatag-e-class-record-template-2026/); automated trimester SF9/SF10 for JHS MATATAG — [PinoyExcel](https://pinoyexcel.com/category/excel-forms/); automated SF9 report card by a school — [Alapan 1 ES](https://alapan1es.com/2022/10/30/automated-sf9-report-card/); SF1–10 compilation — [TeachPinas SF compilation](https://www.teachpinas.com/deped-school-forms-sf-1-10/)
- **SF forms are not fully automated by LIS.** A TeachPinas SF table (per search summary) lists SF2 (daily attendance) as partly LIS and partly manual, and SF10 (permanent record) as manual — [TeachPinas SF compilation](https://www.teachpinas.com/deped-school-forms-sf-1-10/) (verify)
- **LIS data-quality friction:** LIS keeps an audit trail counting each account's corrections and wrong entries, reported automatically to Division, Region and Central Office. Duplicate LRNs go through a formal Data Corrections process with the Division LIS Coordinator. Teachers in comments report errors they cannot fix **(anecdotal)** — [TeacherPH LIS FAQ](https://www.teacherph.com/deped-lis-data-issues-and-frequently-asked-questions/); [DepEd Teachers Club LIS concerns](https://depedclub.com/category/lis-concerns/); [BayaniGuro enrollment/LIS guide](https://bayaniguro.com/announcements/enrollment-lis-guide/)
- **Transfer deadline risk:** if a transfer request isn't confirmed by End of School Year (EOSY), the learner can be tagged as a dropout in the originating school — [DepEd Club LIS advisories](https://depedclub.com/learners-information-system-important-advisories-deped-lis/); [TeacherPH disputed transfer](https://www.teacherph.com/lis-disputed-transfer-facility/)
- DepEd advises teachers to be extra careful when enrolling learners' personal data in LIS to avoid discrepancies — [DepEd Click, SY 2024-25 LIS encoding](https://www.deped-click.com/2024/08/lis-opens-encoding-for-sy-2024-2025.html)

### Inferences
- The new system should be the **single source of truth**. Teachers encode once, and the system generates SF1/SF2/SF4/SF5/SF6/SF9/SF10, ECRs in the official layout, and LIS-ready data or exports. Duplicate encoding into LIS plus Excel is the core pain.
- Grading rules change often (2015/2016 orders, MATATAG, the 2026 three-term calendar and new transmutation). Hard-coding weights is a known pitfall. Store weights, terms and the transmutation table as versioned, per-school-year configuration.
- Validate names, birthdates and LRNs before data reaches LIS, because LIS corrections are slow and audited against the encoding account.
- Track transfers in and out against EOSY deadlines.

### Gaps
- I didn't confirm the exact SF list currently generated by LIS vs. manual, the official 2026 grading weights, or whether LIS accepts any bulk grade import (I found no evidence it does). The order numbers DO 9 s.2026 and DO 015 s.2026 need confirming on deped.gov.ph.
- I found no formal survey that quantifies time spent on SF preparation specifically.

## 3. Parent communication in PH schools

### Takeaway
Facebook Messenger group chats are the dominant, de facto teacher–parent channel, documented mostly in pandemic-era studies. Parents value responsiveness and a scrollable record. Teachers report work-life-balance strain. SMS is cheap (about ₱0.50–₱0.56 per message from local gateways) and reaches parents without data. Vendor parent portals focus on grades, attendance, fees and announcements. I found no rigorous PH survey of parents' expectations.

### Cited Findings
- In Philippine modular distance learning, social media such as Facebook Messenger was the most practical communication mode among teachers, students and parents — [IJPDLL paper](https://www.ijpdll.com/download/utilizing-facebook-and-messenger-groups-as-platforms-for-delivering-mathematics-interventions-in-11290.pdf); [ResearchGate](https://www.researchgate.net/publication/355567830_Utilizing_Facebook_and_Messenger_Groups_as_Platforms_for_Delivering_Mathematics_Interventions_in_Modular_Distance_Learning)
- Parents reported regular communication with teachers via Messenger group chats, where teachers posted instructions and announcements. Parents found schools responsive — [Experiences of Filipino Parents on Distance Learning](https://www.researchgate.net/publication/359202427_Exploring_the_Experiences_of_Filipino_Parents_on_Distance_Learning_During_COVID-19_Pandemic_Exploring_the_Experiences_of_Filipino_Parents_on_Distance_Learning_During_COVID-19_Pandemic)
- Teachers using Messenger reported benefits (convenience, accessibility) and drawbacks in work-life balance, emotional/psychological strain and technical issues — [Post-Pandemic Aspirations of Filipino Teachers](https://www.researchgate.net/publication/370394592_Post-Pandemic_Aspirations_of_Filipino_Elementary_School_Teachers)
- Messenger group chats sustained teacher–student interaction in blended learning (community-of-inquiry study) — [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC9932417/); learners' perception of Messenger for academic communication — [ResearchGate](https://www.researchgate.net/publication/387839789_The_Perception_of_Learners_on_the_Role_of_Facebook_Messenger_as_a_Tool_for_Academic_Communication)
- An NGO case: AHA! Learning Center used free Facebook Messenger, with a teacher in each parent group — [Rappler](https://www.rappler.com/culture-desk/relationships/257556-aha-learning-center-eskwelang-pamilya/)
- **SMS costs:** Semaphore (local gateway) lists outbound SMS at ₱0.56 per text excluding VAT across Globe, Smart, Sun and DITO — [Semaphore](https://www.semaphore.co). A third-party comparison lists ₱0.50 with no setup fees and says international providers cost far more (Twilio about US$0.20 per SMS) — [sent.dm](https://www.sent.dm/resources/philippines-sms-pricing); [Twilio PH pricing](https://www.twilio.com/en-us/sms/pricing/ph)
- Vendor parent portals: SmartEskwela, OceanEd and others bundle a parent portal — [SmartEskwela](https://smarteskwela.com/); [OceanEd](https://theoceaned.com/pricing)
- **Parents' right to records:** NPC Advisory Opinion No. 2025-017 covers whether school records are personal information and parents' access to a child's records. NPC AO 2018-006 covers consent before release of school records — [NPC AO 2025-017](https://privacy.gov.ph/wp-content/uploads/2026/01/NPC-Advisory-Opinion-No.-2025-017_Redactedv2.pdf)

### Inferences
- Don't try to replace Messenger head-on. Make the system the authoritative source for grades, attendance, balances and announcements. Push short notices by SMS (and optionally email or web push), with links to a light mobile web page, and give teachers copy-paste-ready announcement text for their Messenger groups.
- Mobile-first, low-bandwidth design matters: server-rendered or light pages, small payloads, no mandatory native app, SMS fallback for parents without data. At ₱0.56 per SMS, 1,000 parents × 4 messages a month is about ₱2,240 a month before VAT.
- A school-controlled channel lets teachers set office hours, which addresses the work-life balance complaints about Messenger.
- Parent access must handle guardians and multiple children, and follow NPC guidance on releasing records (custody and authorization).

### Gaps
- I found no recent (2024–2026) PH survey of what parents most want to see, how often they check portals, or app vs. web preference. Messenger studies are small and pandemic-era. I found no data on Viber usage among parents or Messenger Platform API constraints for schools.

## 4. LMS and learning tools; integrations that matter

### Takeaway
DepEd provisions Google Workspace for Education (1 million Education Plus licenses for teachers and staff announced in 2025, with learner accounts via School ICT Coordinators) and has also used Microsoft 365 for official email. Google Classroom roster and grade sync is the highest-value LMS integration. Microsoft 365/Teams support should be secondary. I found no evidence of an official DepEd LMS with an integration API.

### Cited Findings
- DepEd and Google are deploying 1 million Google Workspace for Education Plus accounts for teachers and non-teaching staff (Gmail, Classroom, Meet, Docs, Forms, Assignments) — [Inquirer](https://newsinfo.inquirer.net/2043335/1-million-google-workspace-accounts-for-teaching-non-teaching-staff-deped); [BusinessMirror, Mar 2025](https://businessmirror.com.ph/2025/03/15/deped-google-equip-teachers-with-workspace-for-education-plus-suite/); [InsiderPH](https://insiderph.com/one-million-deped-teachers-staff-to-get-google-workspace-for-education-plus)
- DepEd provides Google Workspace for Education accounts to public school employees **and learners**, provisioned from current learner status and distributed by the School ICT Coordinator — [DepEd G Suite training site](https://sites.google.com/deped.gov.ph/gsuitetraining/accounts); [Division ICT request page](https://sites.google.com/deped.gov.ph/ictota-divisionlevel/google-workspace-request)
- A DepEd guideline assigns regular employees and public school learners both a G Suite for Education and a Microsoft 365 Education account — [TeacherPH guidelines](https://www.teacherph.com/deped-guidelines-g-suite-microsoft-365/)
- **Conflict:** a school site says DepEd official email moved from Google Workspace to Microsoft 365 on Oct 1, 2023 — [Alapan 1 ES](https://alapan1es.com/2023/01/30/microsoft-365-adoption/). The 2025 Google Education Plus rollout came later. The current "official" identity provider is unclear.
- Storage caps on DepEd Google accounts since Jan 15, 2024: 100 GB for employees and schools, 20 GB for learners — [DepEd Laguna](https://depedlaguna.com/implementation-of-storage-limits-for-deped-google-workspace-for-education-account/)

### Inferences
- Must-have: "Sign in with Google" (and ideally Microsoft) for teachers and learners using deped.gov.ph or school-domain accounts. Roster push to Google Classroom (courses = sections × subjects, with teachers and students). Grade pull from Classroom coursework into the ECR as WW/PT items.
- Store file attachments in Google Drive or link to them instead of storing them locally, given storage caps and bandwidth.
- Private schools may run their own Workspace or M365 tenants, so make the identity provider configurable per school.
- Moodle and DepEd Commons/LRMDS are better treated as links to resources than as deep integrations (I found no evidence of usable APIs).

### Gaps
- I didn't research DepEd Commons/LRMDS status in 2026, DepEd's own LMS (if any), or Moodle usage in PH high schools. I found no data on the share of private high schools using Classroom vs. Teams.

## 5. Payments for private schools

### Takeaway
PayMongo publishes clear VAT-exclusive rates: GCash 2.23%, Maya 1.79%, QR Ph 1.34%, direct online banking 0.71% or ₱13.39, local cards 3.125% + ₱13.39. Xendit, Maya Checkout and Dragonpay rates come from third-party blogs and conflict. For tuition-sized amounts, QR Ph or online banking are much cheaper than cards or e-wallets. Over-the-counter and bank channels (Dragonpay, ECPay) still matter for unbanked parents.

### Cited Findings
- **PayMongo (official pricing page, VAT-exclusive; 12% VAT applies to the fee):** local cards 3.125% + ₱13.39; international cards 4.02% + ₱13.39; QR Ph 1.34% (2.23% with instant settlement); GCash 2.23%; Maya 1.79%; GrabPay 1.96%; ShopeePay 1.70%; direct online banking 0.71% or ₱13.39; BillEase BNPL 1.34%. No setup fee. Standard settlement takes 2–7 days. Payouts cost ₱10 via InstaPay/PesoNET. Worked example: a ₱1,000 card payment incurs a ₱44.64 fee + ₱5.36 VAT, so the merchant nets ₱950 — [PayMongo pricing](https://www.paymongo.com/pricing)
- **Xendit (third-party, conflicting):** cards 3.2% + ₱10 or 2.9% + ₱15 depending on source; GCash about 2.3%; GCash auto-debit 3.20% + ₱11. One source says Xendit applies its ₱11 fee to **every transaction attempt, including failed ones**, plus payouts and refunds. A Xendit rate card reportedly lists ECPay at ₱25 for loan and school payments — [checkoutflow](https://checkoutflow.co/ph-en/best-payment-gateway-ecommerce/xendit-philippines/); [paymentreview](https://paymentreview.com/comparisons/paymongo-vs-xendit/); [HitPay comparison](https://hitpayapp.com/blog/philippines-payment-gateway-comparison). Xendit's official pricing page returned HTTP 403 to my fetch, so verify directly.
- **Maya Checkout (third-party):** GCash about 2.00% MDR; cards 3.50% + ₱10 — [HitPay comparison](https://hitpayapp.com/blog/philippines-payment-gateway-comparison) (verify)
- **Dragonpay (third-party, conflicting):** over-the-counter about ₱15–₱20 and bank about ₱10 per transaction; mainly OTC and bank, not cards — [oliverrevelo](https://www.oliverrevelo.com/blog/payment-gateways-for-filipino-businesses); [PhotonPay](https://www.photonpay.com/hk/blog/article/payment-gateways-philippines?lang=en) (verify)
- Integration guide for GCash/Maya on business websites — [tul-id](https://tul-id.com/insights/gcash-maya-payment-website-philippines)

### Inferences
- On a ₱20,000 tuition installment: GCash via PayMongo costs about ₱446 + VAT, card about ₱639 + VAT, QR Ph about ₱268 + VAT, and online banking a flat ₱13.39 or 0.71% (about ₱142). The spec should support a per-channel **convenience fee pass-through** setting, and should default to QR Ph or online banking.
- Integration pattern: create a checkout or payment intent per invoice. Confirm payment via **signed webhook**, never the client redirect. Make webhook handling idempotent. Reconcile against gateway settlement reports, which arrive 2–7 days later and net of fees. Post fees as an expense, separate from the student ledger.
- Still support manual payment entry: a photo of a bank or GCash transfer receipt with registrar verification. Many PH parents pay by personal transfer, and duplicate or fake screenshots are a risk, so require reference numbers and dedupe on them.
- Avoid gateways that charge for failed attempts, or account for them, if parents retry often.

### Gaps
- I didn't verify official rates for Xendit, Maya Business, Dragonpay or GCash for Business, or school-specific (biller/education) MDR discounts. I found no data on what share of PH private-school tuition is paid online vs. over the counter.

## 6. Failure points and lessons from PH school IT projects

### Takeaway
Recurring lessons: peak-period load on centralized DepEd systems (LIS lag and timeouts at enrollment), poor connectivity and electricity in many schools, and data breaches involving education data. The worst was a 2024 DepEd voucher (OVAP) database with 210,020 student and parent records left with no password, including LRNs and family income. The NPC stresses that outsourcing to vendors does not transfer Data Privacy Act liability.

### Cited Findings
- **OVAP exposure (Feb 2024):** DepEd's Online Voucher Application platform for SHS vouchers had no password protection. 210,020 records (153.76 GB) were exposed: learner names, LRN, DOB, address, contact details, JHS attended, parent and guardian names, income sources, gross monthly income, sibling details and property owned. Researcher Jeremiah Fowler reported it to DepEd and the NPC. The NPC said it secured the database and was investigating, and the exposure duration is unknown — [Inquirer Technology](https://technology.inquirer.net/132322/ph-platform-ovap); [iTnews Asia](https://www.itnews.asia/news/philippine-education-ministry-hit-by-data-leak-exposing-210020-records-605321); [Newsbytes](https://newsbytes.ph/2024/02/24/unsecured-deped-cloud-database-of-students-parents-exposed/)
- **Claimed DepEd regional office hack (Feb 2024):** a threat actor claimed 750 GB including banking, student and teacher data. DICT doubted the claim, and CICC looked into it — [PhilStar](https://www.philstar.com/headlines/2024/02/15/2333485/deped-checking-data-breach-after-hacking); [GMA](https://www.gmanetwork.com/news/topstories/nation/897443/deped-verifying-possible-data-breach-among-students-teachers/story/); [PNA](https://www.pna.gov.ph/articles/1218862)
- **NPC case on DepEd Calamba** (breach notification NPC BN 18-054, database breach detected April 2018) — [NPC resolution PDF](https://privacy.gov.ph/wp-content/uploads/2025/12/NPC-BN-18-054-09.17.24-In-re-Department-of-Education-Calamba_Resolution.pdf)
- **Earlier NPC action:** NPC summoned school and government officials over defaced websites and asked why they hadn't notified within 72 hours. About 2,000 people's data (names, contacts, some passwords, school details) was downloadable via Facebook links — [Rappler](https://rappler.com/nation/national-privacy-commission-summons-officials-security-breach)
- **Nov 2026 breach wave:** a monitoring report covering Nov 5–7, 2026 names universities among up to 23 institutions with leaks (University of Camarines Norte, CvSU-General Trias, NEUST, University of St. La Salle; NPC hasn't confirmed). Data categories include "student files." The NPC reminded organizations that breach notification is mandatory under NPC Circular 16-03 and that **outsourcing IT does not remove Data Privacy Act obligations, including for data held by third-party vendors** — [PhilStar, Nov 12 2026](https://www.philstar.com/headlines/2026/11/12/2569565/npc-confirms-data-breach-10-government-agencies)
- **Data Privacy Act guidance for DepEd school heads** (RA 10173) — [NASH](https://nash.com.ph/blog/data-privacy-act-ra-10173-deped-schools)
- **Connectivity:** in his July 2025 SONA, Marcos said nearly 12,000 public schools lacked internet and pledged connectivity for all by end-2025 — [PhilStar](https://www.philstar.com/headlines/2025/07/28/2461427/marcos-vows-internet-access-all-public-schools-end-2025); [GMA](https://www.gmanetwork.com/news/topstories/nation/954010/marcos-vows-internet-for-all-public-schools-by-end-of-2025/story/). About 1,500–1,700 schools lacked electricity (2024–25), mainly in BARMM, North Cotabato, Palawan, Cebu, Zamboanga del Sur and Negros Oriental — [The Flame](https://abtheflame.net/news/2025/07/as-marcos-vows-internet-access-for-all-public-schools-over-a-thousand-still-lack-electricity/); [OpenGov Asia](https://archive.opengovasia.com/2025/02/06/the-philippines-power-and-connectivity-bolster-last-mile-education/?c=us). The proposed 2026 budget gives DepEd ₱1.5B for school internet and NEA ₱3.6B to electrify about 6,000 off-grid schools — [Maharlika NuMedia](https://maharlika.tv/2026-budget-boosts-free-internet-and-power-access-for-public-schools/); [PNA](https://www.pna.gov.ph/articles/1264119); UP CIDS policy paper — [UP CIDS](https://cids.up.edu.ph/wp-content/uploads/2023/12/02_Provision_Electricity_Internet_Access_DepEd_Schools_School_Performance_Digital_Inclusivity_Alampay_Navarro.pdf)
- **LIS peak-load problems (anecdotal):** blog reports of slow login, lag and "Gateway Timeout" at peak times — [ilovedeped](https://www.ilovedeped.net/2025/04/lisdepedgovph-login-guide-how-to-access.html). A DepEd advisory on an outage across DepEd websites and information systems (LIS, EBEIS) — [DepEd Club advisories](https://depedclub.com/learners-information-system-important-advisories-deped-lis/). 2020 online enrollment slowdowns and dry-run "glitches" — [Inquirer](https://newsinfo.inquirer.net/1292145/online-enrollment-slows-down-in-2nd-week/amp); [Inquirer](https://newsinfo.inquirer.net/?p=1319725)
- **Reporting lag:** DepEd blamed a "lag" in reporting for an apparent drop in private-school enrollment, a sign of data-sync gaps between schools and central systems — [Inquirer](https://newsinfo.inquirer.net/1497758/deped-blames-lag-in-reporting-for-private-school-enrollment-drop)

### Inferences
- Security baseline the spec should require: no publicly reachable databases or storage buckets; encryption at rest and in transit; MFA for staff; least-privilege roles (adviser, subject teacher, registrar, cashier, principal, parent); audit logs; a 72-hour breach-notification runbook (NPC Circular 16-03); a Data Protection Officer and NPC registration where applicable; data-sharing and outsourcing agreements with any hosting or SMS/payment vendor. Family income, LRNs and IDs are high-risk fields, so minimize collection.
- Design for enrollment-season peaks (load testing, queueing) and for intermittent connectivity: offline-tolerant grade entry or Excel import/export as a fallback, small pages, and SMS for critical notices.
- Keep the system's SF/LIS exports aligned with what DepEd reports, to avoid the reporting gaps behind the "lag" story.

### Gaps
- I couldn't find a final NPC decision imposing penalties on a private school for a student-data breach, or the outcome of the OVAP investigation. A targeted search of privacy.gov.ph decisions is needed. I found no post-mortems of failed private-school SMS deployments in the PH.
