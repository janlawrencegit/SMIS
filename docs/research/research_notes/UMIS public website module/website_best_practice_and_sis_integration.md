# University Public Website: Best Practice, Information Architecture and SIS Integration (for UMIS)

Scope note: researched November 2026. Budget-limited to ~20 tool calls. DLSU (dlsu.edu.ph) and Ateneo (ateneo.edu) returned HTTP 403 to the fetcher, so PH site IA could not be inspected directly. Edinburgh's homepage was fetched. Several CMS and integration questions rest on inference, not sources; these are labelled.

## 1. Information architecture, navigation and homepage composition; what higher-ed UX research says

### Takeaway
Prospective students mainly come for programs/majors, aid and cost, and admissions steps. The most common failures are programs that can't be found, deadlines that are hidden, missing outcome data, weak site search and org-chart navigation. Leading sites pair a short task/topic-based primary nav (Study, Research, About, Visit, News) with an audience utility bar (Students, Staff, Alumni) and put a degree finder near the top of the homepage.

### Cited Findings
- NN/g university study: 57 university sites tested with 33 users aged 16–68 (prospective undergrad/grad students and parents) in the US, Canada, UK and Taiwan. Published Jan 2014, updated Apr 2016. Conclusion: most sites "rank far below" expected usability — [NN/g, University Websites: Top 10 Design Guidelines](https://www.nngroup.com/articles/university-sites/)
- 48% of users didn't realise a university offered a program they wanted, even though it did. Users assumed a program wasn't offered when it wasn't under the school they expected — [NN/g](https://www.nngroup.com/articles/university-sites/)
- Users often couldn't tell which school or college owned a page. Vague labels (e.g. a "Do Stuff" heading hiding the Visit tab) and links placed far from related content went unnoticed — [NN/g](https://www.nngroup.com/articles/university-sites/)
- Students struggled to find application deadlines. Prospective students and parents wanted job-placement and outcome data, looked for it first under Alumni, and inferred poor outcomes when it was absent — [NN/g](https://www.nngroup.com/articles/university-sites/)
- Stock photos and trendy video or "cool" language reduced credibility. Dense text and contradictory duplicate content across departments hid facts. Frustrated users moved to Google, aggregators and forums, which they sometimes trusted more than the university site — [NN/g](https://www.nngroup.com/articles/university-sites/)
- NN/g's top 10 guidelines:
  1. Show the full university name on every page.
  2. Use authentic images.
  3. Make About pages informative, with a scannable facts list.
  4. Highlight rankings and achievements.
  5. Make majors and programs easy to browse, grouped by school or field, with degree names visible.
  6. Publish job-placement data and link it from Alumni.
  7. Show deadlines and a step-by-step application process.
  8. Test cross-department journeys with about 5 users.
  9. Avoid gimmicks.
  10. Strengthen internal search and keep external listings accurate.
  — [NN/g](https://www.nngroup.com/articles/university-sites/)
- NN/g's paid University Websites report (2nd ed.) has 152 guidelines and 297 screenshots from 100+ sites — [NN/g report page](https://www.nngroup.com/reports/university/)
- 2025 E-Expectations Trend Report (RNL, Halda and Modern Campus; 1,582 US high-school respondents, 47% seniors, 34% first-generation). What prospective students look for on college websites:
  - academic majors and course catalogs: 57%
  - scholarship and financial aid: 49%
  - specific program details: 46%
  - cost and tuition: 39%
  - admissions process and contact info: 38%
  - campus life: 33%
  - student support such as tutoring: 33%
  - housing: 30%
  - location: 29%
  - health and mental-health resources: 29%
  - campus photos: 28%; campus videos: 23%
  - virtual tours: 26%
  — [RNL/Modern Campus webinar deck summarising the report](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- Same report, top website frustrations (listed without percentages in the deck): hard to find info on specific majors or programs; missing admission statistics; no search tool; confusing admissions process; hard-to-use navigation or broken links; online forms asking for too much info; lack of personalisation — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- An earlier RNL/Modern Campus release (2021): 40% of high-school students lose interest in a college after a poor website experience — [Modern Campus newsroom](https://omniupdate.com/about/newsroom/new-survey-from-modern-campus-and-ruffalo-noel-levitz.html)
- EAB 2025 Student Communication Preferences Survey (~19–20k students; EAB's own reports give slightly different sample sizes). Most students look for a link to the specific school's website or another known site, and only 11% say they read AI-generated results — [EAB blog: students using AI to research your college](https://eab.com/resources/blog/enrollment-blog/students-using-ai-research-your-college/); [EAB: is email marketing dead](https://eab.com/resources/blog/enrollment-blog/is-email-marketing-to-prospective-students-dead-not-so-fast/)
- Site search: in NN/g's study, the correct page for "tuition" ranked first on only 33 of 54 sites (secondary citation) — [Evolving Web summary](https://evolvingweb.com/blog/surprising-stats-and-useful-facts-about-university-websites)
- Site search: a January 2025 Chronicle Studio survey of 225+ higher-ed web and marketing leaders found nearly half had weak insight into site-search performance (search snippet only) — [Chronicle/Untapped Insights brief](https://connect.chronicle.com/rs/931-EKA-218/images/Untapped%20Insights_Site%20Search%20Research%20Brief.pdf?version=0)
- University of Edinburgh homepage (fetched Nov 2026):
  - Primary nav: Study, Global, Visit, Research, News, About, Alumni, Local, Staff, Students.
  - Utility: Schools & departments (A–Z), MyEd (portal login), search.
  - Homepage order: Study with us → Graduation → **degree finder** (study-level dropdown + keyword) → Impact stories → Latest news → Events → Visit → Global → Local → Research & teaching → Visit/open days → About → Connect (contacts, jobs, alumni & donors, A–Z, press, social).
  - Footer: accessibility statement, FOI, data protection, privacy/cookies, complaints, modern slavery.
  — [ed.ac.uk](https://www.ed.ac.uk/)

### Inferences
- Recommended UMIS primary nav, which blends topics/tasks with an audience bar: **Admissions | Academics (Programs) | Research | Campus Life | About | News & Events**. Utility bar: **Students, Faculty & Staff, Alumni, Parents, Portal login, Apply (CTA), Search, EN/FIL toggle**. Footer: transparency/FOI (Philippine public institutions), Data Privacy notice, accessibility statement, procurement/bids, careers, contact directory, campus map.
- Avoid audience-only navigation as the main structure. Audience menus duplicate content and force users to classify themselves. NN/g's evidence on ownership confusion points to task-based and program-centric routes, with audience pages kept as curated link hubs.
- Mobile-first homepage order: hero carrying one primary CTA (Apply / Find a program) → program finder → admissions key dates (pulled from the SIS calendar) → announcements (urgent, e.g. class suspensions) → news → events → outcomes and rankings stats → campus life → footer.
- Every program has one canonical URL. Colleges link to it and never copy it, which fixes the contradictory-duplicates problem.

### Gaps
- PH university IA (UP, Ateneo, DLSU, UST, Mapúa) could not be fetched (403 on DLSU and Ateneo; others not attempted within budget). Their navigation needs manual review.
- No current EDUCAUSE or Terminal Four survey data was retrieved.
- Percentages for each "website frustration" were not extractable from the deck.

## 2. Program/degree pages, program finder and catalog-driven generation

### Takeaway
Program pages are the highest-demand content. They should be generated from the SIS program catalog (curriculum, units, duration, CHED/accreditation status) and enriched by editors (careers, outcomes, testimonials, media). A faceted finder should let users find a program without knowing which college owns it.

### Cited Findings
- Majors/catalogs (57%) and specific program details (46%) are the top things students seek. Hard-to-find program info is the top frustration — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- RNL's recommended content: graduate outcomes, step-by-step admissions guidance, admission stats and program rankings, personalised content and filtering, and video of recent grads discussing jobs and salaries — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- NN/g: offer a full browsable list of majors grouped by school or field with degree names visible, and publish placement data — [NN/g](https://www.nngroup.com/articles/university-sites/)
- schema.org `EducationalOccupationalProgram` properties map directly onto catalog fields: `programPrerequisites`, `timeToComplete`, `occupationalCredentialAwarded`, `offers` (tuition), `applicationDeadline`, `startDate`, `educationalProgramMode`, `financialAidEligible`, `salaryUponCompletion`, `termDuration`, `numberOfCredits`, `hasCourse`, `provider`, `occupationalCategory` (O*NET-SOC/ISCO-08) — [schema.org](https://schema.org/EducationalOccupationalProgram)
- Edinburgh's degree finder appears near the top of the homepage, with a study-level filter and keyword search — [ed.ac.uk](https://www.ed.ac.uk/)

### Inferences
- Program page template:
  - **SIS-sourced fields:** title, degree level, college, mode, duration, total units, curriculum by year/term (course codes, titles, units, prerequisites), CHED COPC/accreditation level (e.g. AACCUP/PAASCU), board-exam relevance, slots/quota, start term.
  - **Editor fields:** overview, why study here, career paths, licensure-exam passing rates vs national, employment outcomes, faculty highlights, facilities, testimonials, FAQs.
  - **Admissions-sourced fields:** requirements, deadlines, fees/tuition estimate, scholarships.
  - **CTAs:** Inquire, Apply, Visit, Download prospectus (PDF).
- Finder facets: level (SHS/UG/Grad/TESDA/short course), college, field/interest cluster, campus, mode (onsite/online/blended), licensure program (yes/no). Include keyword search with synonyms (e.g. "nursing" → BSN) and an A–Z list.
- Sync rule: the SIS owns academic facts and is read-only in the CMS. The CMS owns marketing content. A program unpublished or phased out in the SIS hides its page automatically or shows a "no longer accepting applicants" state.

### Gaps
- No PH-specific study on program-page content needs was found. Licensure passing-rate display practice was not verified from sources.

## 3. Admissions funnel: inquiry, CRM capture, application, status, visits, exams

### Takeaway
Students treat forms and email as "reaching out". They expect an email reply (68%) and often a text (40%), so every inquiry must be captured to a CRM with immediate confirmation and a clear next step. Forms that ask too much are a top frustration.

### Cited Findings
- How students think they reach out to a college: email 52%, **forms 51%**, follow social 27%, visit 27%, college-planning sites 20%, respond to print 18%, list school on a test 15%, mobile app 10%, call 10%. 7% won't connect — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- What students want after reaching out: email 68%, text 40%, phone 23%, print 22%, **confirmation screen with next steps 22%** — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- Favourite channels for college information: email 74%, print 33%, text 33%, phone 22%, in person 22%, video 16% — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- AI on websites: 68% are open to AI chatbots on college websites. RNL advises training them to drive concrete next steps rather than just installing them — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- RNL action steps: "Design every digital moment to offer a clear next step"; track engagement beyond form fills — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf)
- WCAG 2.2 SC 3.3.7 Redundant Entry (Level A) requires information already entered in a process to be auto-populated or selectable. This applies directly to multi-step applications — [W3C What's New in WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)

### Inferences
- Funnel stages and UMIS objects:
  1. **Inquiry** (short form: name, email, mobile, program interest, intended term, consent) → `Lead`/`Prospect` in a CRM table, plus UTM/source capture and an auto email/SMS reply.
  2. **Account creation / application start**, which pre-fills from the lead (Redundant Entry).
  3. **Requirements checklist**: uploads (Form 138/report card, PSA birth certificate, good moral, ID photo), with status per item.
  4. **Entrance exam scheduling**: slot booking with capacity, venue, permit PDF/QR.
  5. **Fees**: application fee via payment gateway (GCash/Maya/bank).
  6. **Application status tracker**: submitted → under review → for exam → results → admitted/waitlisted → confirmation/reservation fee → enrolment handoff.
  7. **Campus visit / open house booking**: event registration with reminders.
- Keep the application in the authenticated SIS/admissions module (Inertia SPA). Keep the public site's inquiry and visit forms server-rendered and light. Hand off via a signed link that carries the lead ID.
- PH context: SMS/Messenger follow-up matters. Facebook ad reach of 95.8M and Messenger 65.8M ([DataReportal 2026](https://datareportal.com/reports/digital-2026-philippines)) suggest offering Messenger/Viber/SMS opt-ins alongside email.
- Data Privacy Act (RA 10173) consent capture is needed on every form. This is an inference: the NPC guidance was not fetched.

### Gaps
- No PH-specific conversion benchmarks were found. Entrance-exam scheduling practices at UP (UPCAT), Ateneo (ACET), DLSU (DCAT) and UST (USTET) were not verified this session.

## 4. Content types: news, events, announcements, calendar, faculty/research, publications, alumni/giving, careers, bids/procurement, downloads

### Takeaway
A public university site needs a set of structured content types beyond pages. For Philippine SUCs this includes legally required procurement and transparency postings. Many of these types (calendar, faculty, publications, graduates) should be fed by SIS/HR data rather than typed by hand.

### Cited Findings
- Edinburgh exposes news, events, impact stories, graduation, jobs, alumni & donors, A–Z of units, press, and FOI/data-protection pages from its homepage and footer — [ed.ac.uk](https://www.ed.ac.uk/)
- NN/g found that faculty pages persuade prospective students (video title) — [NN/g video](https://www.nngroup.com/videos/university-faculty-pages/)
- Procurement posting under RA 9184 (GPPB Circular 01-2021): procurement documents are posted on PhilGEPS, at a conspicuous place in the procuring entity's premises, **and on the procuring entity's website, if any** — [GPPB Circular No. 01-2021](https://www.gppb.gov.ph/wp-content/uploads/2023/05/GPPB-Circular-No.-01-2021.pdf)
- RA 12009 (New Government Procurement Act, 20 July 2024) is the newer procurement law. SUC posting rules should be checked against it and its IRR — [RA 12009, Lawphil](https://lawphil.net/statutes/repacts/ra2024/ra_12009_2024.html)
- Transparency Seal: displayed on an agency website's main page as a certificate of compliance with GAA transparency posting requirements. SUC example page — [MinSU Transparency](https://minsu.edu.ph/good-governance/transparency); [judiciary e-library issuance](https://elibrary.judiciary.gov.ph/thebookshelf/showdocs/6/92743)
- WCAG 2.2 SC 3.2.6 Consistent Help (Level A): help mechanisms such as contact info and chat must appear in the same relative order across pages — [W3C](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)

### Inferences
- Content-type list for UMIS:
  - **News** (categories, college tag, featured image, author, scheduled publish)
  - **Announcement** (priority/urgent banner, expiry date, audience)
  - **Event** (start/end, venue/online, registration link or internal RSVP, iCal export)
  - **Academic Calendar** (read-only from the SIS term/calendar tables)
  - **Faculty Profile** (synced from HR/SIS: name, rank, department, degrees; self-editable bio, research interests, ORCID, Google Scholar)
  - **Research Project/Centre**
  - **Publication** (repository record with DOI, PDF, license; or a link to DSpace/an institutional repository)
  - **Program** (catalog-driven)
  - **Office/Unit directory**
  - **Job Posting** (HR: plantilla item, salary grade, qualifications, deadline, CSC posting reference for SUCs)
  - **Bid/Procurement notice** (ITB/REI, bid bulletins, notices of award, NTP, PhilGEPS reference, APP/PPMP, closing date, attachments)
  - **Download/Form** (versioned file, office owner, revision date)
  - **Alumni story** and **Giving campaign** (with payment gateway or pledge form)
  - **Transparency Seal page** (budget, BAR, APP, PhilGEPS, SALN index, citizen's charter, FOI manual)
- Plain-language summaries plus a "last reviewed" date on every page support governance.

### Gaps
- No current authoritative checklist of SUC website posting obligations under RA 12009 / the 2025–26 GAA was found. This needs legal or compliance review.

## 5. Search, multilingual, accessibility (WCAG 2.2 AA), performance (CWV), SEO structured data, mobile-first

### Takeaway
Target WCAG 2.2 AA. Its new AA criteria cover target size of at least 24×24 CSS px, focus not obscured, dragging alternatives and accessible authentication. Target Core Web Vitals "good" at p75 on mobile: LCP ≤2.5s, INP ≤200ms, CLS ≤0.1. Use schema.org markup knowing that Google retired Course Info rich results in 2025. The Philippines is overwhelmingly online through mobile and social.

### Cited Findings
- WCAG 2.2 became a W3C Recommendation on 5 Oct 2023. It adds 9 SC:
  - 2.4.11 Focus Not Obscured (Minimum), **AA**
  - 2.4.12 Focus Not Obscured (Enhanced), AAA
  - 2.4.13 Focus Appearance, AAA
  - 2.5.7 Dragging Movements, **AA**
  - 2.5.8 Target Size (Minimum) of 24×24 CSS px or sufficient spacing, **AA**
  - 3.2.6 Consistent Help, A
  - 3.3.7 Redundant Entry, A
  - 3.3.8 Accessible Authentication (Minimum), **AA**: no cognitive tests at login without an alternative
  - 3.3.9 Accessible Authentication (Enhanced), AAA
  - 4.1.1 Parsing is obsolete and removed.
  — [W3C What's New in WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)
- Core Web Vitals thresholds:
  - LCP: good ≤2.5s, poor >4s
  - INP: good ≤200ms, poor >500ms
  - CLS: good ≤0.1, poor >0.25
  - Assessed at the 75th percentile of page loads, segmented by mobile and desktop.
  - INP replaced FID as a stable Core Web Vital in 2024.
  — [web.dev Web Vitals](https://web.dev/articles/vitals); [web.dev Defining thresholds](https://web.dev/articles/defining-core-web-vitals-thresholds)
- Philippines, end of 2025 (DataReportal Digital 2026):
  - Internet users: 98.0M (83.8% penetration); 19.0M offline.
  - Cellular connections: 137M (117% of population).
  - Median download speed: mobile 59.64 Mbps (+77% YoY), fixed 105.17 Mbps.
  - Social media: 95.8M user identities; 97.7% of internet users on at least one platform.
  - The page does not give a mobile-vs-desktop traffic share.
  — [DataReportal Digital 2026 Philippines](https://datareportal.com/reports/digital-2026-philippines); [GMA on mobile connections](https://www.gmanetwork.com/news/topstories/nation/991809/ph-mobile-connections-report-2025/story/)
- Google (12 June 2025) phased out several rich-result types, including **Course Info**, to simplify search results. Search Console reporting for these was removed from 9 Sep 2025. Coverage says the markup can remain, does not affect ranking, and no longer produces rich results — [Google Search Central blog](https://developers.google.com/search/blog/2025/06/simplifying-search-results); [Search Engine Journal](https://www.searchenginejournal.com/google-drops-search-console-reporting-for-six-structured-data-types/555560/); [Search Engine Land](https://searchengineland.com/google-to-drop-support-for-several-rich-result-types-to-simplify-the-search-results-page-456969)
- `EducationalOccupationalProgram` properties (see Section 2) — [schema.org](https://schema.org/EducationalOccupationalProgram)
- RNL lists "no search tool" among top frustrations. NN/g recommends robust internal search — [RNL deck](https://www.ruffalonl.com/wp-content/uploads/2025/07/23D72-Decoding-Student-Preferences-Effective-College-Communications-and-Website-Strategies.pdf); [NN/g](https://www.nngroup.com/articles/university-sites/)

### Inferences
- **SEO:**
  - Server-render the public site with Blade, or Inertia SSR if Vue components are shared. Use clean URLs (`/programs/bs-computer-science`), canonical tags, XML sitemaps per content type, Open Graph tags (Facebook sharing dominates in PH), and `hreflang` if Filipino pages exist.
  - JSON-LD per type: `CollegeOrUniversity` (sitewide, with `sameAs` socials, address, logo), `EducationalOccupationalProgram` (program pages), `Course` (optional; rich result retired), `Event` (Google still supports Event rich results; not re-verified this session), `NewsArticle`, `BreadcrumbList`, `JobPosting` (careers), `Person` (faculty).
- **Performance on mid-range Android over mobile data:**
  - Responsive images (AVIF/WebP, `srcset`), a hero image under about 150KB with `fetchpriority=high`, and no autoplay hero video on mobile.
  - Minimal JS on public pages; hydrate islands only (finder, forms).
  - Self-hosted subset fonts, CDN/edge cache with HTML caching invalidated on publish, and lazy-loaded embeds such as Facebook and YouTube facades.
  - Use RUM (the web-vitals library) to track p75.
- **Accessibility:**
  - Tailwind design tokens with 44px tap targets, which exceed the 24px AA minimum.
  - Sticky headers must not cover focused elements (2.4.11).
  - Avoid CAPTCHA puzzles on inquiry and login forms (3.3.8); use honeypot or Turnstile-type invisible checks.
  - Keep help/contact in a consistent position (3.2.6).
  - Publish an accessibility statement.
  - Run axe/pa11y in CI.
- **Search:**
  - PostgreSQL full-text search (tsvector, `unaccent`, trigram for typos) is enough at launch. Meilisearch/Typesense via Laravel Scout is an option for faceting and synonyms.
  - Index programs, pages, news, people, offices and downloads with type facets.
  - Feature "best bets" (tuition, enrollment, calendar).
  - Log zero-result queries.
- **Multilingual:**
  - English primary. Offer Filipino for high-traffic admissions/FAQ/announcement pages rather than full parity.
  - Model translations per entry with a locale (`/fil/...`) and fall back to English.
  - Add regional languages only if analytics show demand.

### Gaps
- No PH-specific mobile traffic share (%) was found. DataReportal 2026 omits it.
- No source was found on Filipino-language demand on university sites.
- Google Event rich-result status was not re-verified after the Nov 2025 simplification update.

## 6. CMS approach, editorial roles/workflow, multi-site governance

### Takeaway
No sources were retrieved on this topic within budget. The recommendations below are inferences from the stack and the governance failures documented in Section 1.

### Cited Findings
- NN/g documents duplicated and contradictory content across departments and users' inability to tell which unit owns a page. Both point to governance and ownership problems — [NN/g](https://www.nngroup.com/articles/university-sites/)
- Edinburgh's footer exposes a "CMS login" next to MyEd. That suggests an integrated, centrally hosted CMS used by distributed editors — [ed.ac.uk](https://www.ed.ac.uk/)

### Inferences
- **Integrated vs headless:** for UMIS (Laravel monolith with PostgreSQL), an integrated CMS inside the same app (Filament-style admin, or custom Inertia admin, with Blade/SSR front end) avoids a second system and allows direct joins to SIS tables (programs, calendar, faculty). Choose headless only if a separate marketing team or JAMstack hosting is required. Laravel-native options to evaluate: Statamic (flat-file/Eloquent; multi-site, revisions, workflows in Pro), Twill, or custom models with a block editor. Not verified this session.
- **Content model:** typed entries (Section 4) plus a flexible "page" built from blocks (hero, rich text, CTA, accordion/FAQ, card grid, stats, program list, event list, news list, embed, file list). Blocks query the SIS live, so a page cannot hold stale copies.
- **Workflow:**
  - States: Draft → In Review → Approved → Scheduled/Published → Archived.
  - Roles: Contributor (unit), Editor (college), Publisher (central web office), Admin; plus SIS data steward roles that never edit synced fields.
  - Features: scheduled publish/unpublish (`publish_at`/`expire_at`, run by the Laravel scheduler), full revision history with diff/restore, preview links, audit log, required alt text, and a reading-level/a11y check on save.
- **Multi-site per college:** one install, with a `site_id` (or college) scope on content, subpaths (`/engineering/...`) rather than subdomains for SEO consolidation, shared global header/footer and design system, college-specific hero/news, and permission scoping per site. Central owners control program pages; colleges contribute fields.
- **Governance:**
  - Each page has a named owner and a review interval (e.g. 6–12 months), with automated stale-content reminders and broken-link checks.
  - Use a style guide and a single content source per fact (deadlines and fees live once and are referenced).

### Gaps
- No Modern Campus or Terminal Four CMS survey data was retrieved. Statamic, Twill and Filament capabilities were not verified. No higher-ed headless-vs-integrated studies were found.

## 7. SIS integrations

### Takeaway
The website should be a read-mostly consumer of SIS data (catalog, calendar, schedules, graduates, faculty) and a producer of leads and applications. It should also host a privacy-safe credential verification endpoint, matched against PH practice (school QR verification plus CHED eCAV).

### Cited Findings
- CHED runs an electronic Certification, Authentication and Verification (eCAV) system. Verifiers enter an application number and date on CHED's verification tab (announced in a testing-phase advisory, 13 Jan 2025) — [CHED advisory](https://legacy.ched.gov.ph/public-advisory-on-the-testing-phase-of-ched-electronic-certification-authentication-and-verification-ecav-web-application-system/); [YugaTech on eCAV launch](https://www.yugatech.com/news/ecav-system-launched-in-the-philippines-to-digitize-academic-records/)
- CHED and DICT announced digitisation of diploma, transcript and certification release (2023) — [ABS-CBN](https://abs-cbn.com/news/05/30/23/ched-dict-to-digitize-release-of-diplomas)
- PHINMA Education rolled out verifiable digital diplomas — [PHINMA](https://phinma.com.ph/phinma-education-rolls-out-verifiable-digital-diplomas-for-graduates)
- Legal commentary warns verifiers not to rely on a QR code or link printed on the document alone, and to confirm with the issuing registrar. A verification endpoint must therefore sit on the university's official domain and be discoverable independently of the document — [Respicio & Co.](https://www.respicio.ph/commentaries/how-to-verify-whether-a-diploma-is-authentic-in-the-philippines)
- DLSU publishes its CHED CAV request procedure as a registrar download — [DLSU PDF](https://www.dlsu.edu.ph/wp-content/uploads/pdf/registrar/ched-cav-requests-procedures.pdf)
- Some universities put QR codes on records that, when scanned, show document type, issue date and recipient details (search-snippet description, not verified at source) — [UAP announcement](https://my.uap.asia/bboard/comms_announcement_view.php?editid1=18)
- Research on blockchain diploma verification for PH HEIs exists — [UPOU repository](https://repository.upou.edu.ph/items/f800afbf-fe45-4bf7-8643-b54fb9cb93a4)

### Inferences
- **Program catalog sync:** the public site reads the SIS `programs`, `curricula`, `courses` and `prerequisites` tables directly in the monolith, or through a read model and materialized view. Fire domain events (`ProgramPublished`, `CurriculumRevised`) to purge cache and regenerate the sitemap. Only curricula flagged "public" are shown; the effective curriculum is chosen per intake year.
- **Admissions handoff:** a public inquiry creates a `Prospect`. "Apply" goes to the admissions module, with SSO/account creation pre-filled from the prospect. The application ID links back to the prospect for attribution (UTM, source). Admitted applicants convert to `Student` in the SIS without re-keying data (WCAG 3.3.7 spirit; data quality).
- **Public academic calendar:** publish SIS term events (enrolment periods, start of classes, exams, holidays, deadlines) marked `public=true`. Provide an HTML page, iCal (ICS) feed per audience, and JSON-LD `Event` for major items. Class suspensions are urgent announcements with expiry.
- **Document/diploma/TOR verification:**
  - Each issued document gets a random, non-guessable token (e.g. 128-bit) and an optional short code. The QR encodes `https://<univ-domain>/verify/<token>`.
  - The page shows minimal data: name, document type, program, date conferred/issued, SO number where applicable, valid/revoked status.
  - Optionally require the verifier to enter the student's surname or birthdate (2-factor matching) before showing details, to limit disclosure under the Data Privacy Act.
  - Rate-limit the endpoint, log verifications, and support revocation/reissue.
  - Optionally add a signed hash (Ed25519) of the document content so PDF tampering is detectable.
  - Link to CHED eCAV for authenticated copies.
- **Class schedule lookup:** a public, anonymised catalog of sections per term (course, section, schedule, room, instructor name if policy allows, slots remaining). Cache it heavily and show no student data.
- **Graduate directory / commencement list:** publish only graduates who opted in (consent flag in the SIS, captured at graduation application). Show name, degree, honours and year, with a withdrawal mechanism. Default to no listing.
- **Faculty profiles:** HR/SIS supplies name, rank and department. Faculty self-edit bio, interests and links. Publication lists come from the repository or ORCID.
- **Licensure exam results / outcomes:** curated by the registrar or QA office from PRC result data. Publish aggregate percentages vs national rates, never per-student data without consent.

### Gaps
- No authoritative source was found for a national standard linking school QR verification to CHED eCAV.
- The NPC's position on publishing graduate lists was not fetched. Legal review under RA 10173 is recommended.
- Class-schedule publication practices at PH universities were not verified.
