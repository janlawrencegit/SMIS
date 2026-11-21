# State of Philippine HEI Websites ("Meron pa bang university na walang website?")

Research date: 2026-11-21. Most sources are abstracts, news reports, or search-result snippets; full-text PDFs for several academic papers could not be opened (noted per item). webometrics.info and i-scholar.in were not reachable from the research environment, and legacy.ched.gov.ph returned HTTP 503 on direct fetch.

## 1. How many HEIs exist, and what share have an official website vs. only a Facebook page?

### Takeaway
CHED counts about 2,334 HEIs for AY 2024-25 (campus-level count, excluding 92 BARMM HEIs), or about 1,977 institutions at a January 2024 institution-level count. No study or directory was found that measures what share have an official website vs. only a Facebook page. The best proxy, Webometrics, listed only 365 PH HEIs in January 2023 (about 15-19% of the total), which suggests many HEIs, mostly small private and local colleges, have little or no independent web presence that crawlers can detect.

### Cited Findings
- **AY 2024-25 (CHED, as of June 26, 2025):** grand total of **2,334 HEIs**. The table's columns read 1,619 | 154 | 6 | 113 | 442 | 2,334, which likely map to private | LUC | OGS/special | SUC main | SUC satellite | total, but the column headers were not visible. BARMM HEIs are excluded (85 private and 7 other government HEIs). Adding them gives about 2,426, but CHED does not state that sum. — [CHED Statistics (archived page, via search snippet)](https://legacy.ched.gov.ph/statistics/)
- **As of January 4, 2024 (PCO release):** 113 SUCs, 137 LUCs, 1,714 private HEIs, and 13 OGS/CHED-supervised/special schools, about **1,977 HEIs**. This count appears to leave out SUC satellite campuses, which explains the gap with the 2,334 figure. — [PCO News Release](https://mirror.pco.gov.ph/?p=186572) (seen via search snippet; the direct fetch returned 403)
- **Conflicting LUC count:** GMA reports 179 LUCs nationwide, of which only 101 qualify for free tuition (i.e., CHED-recognized under RA 10931). — [GMA News](https://www.gmanetwork.com/news/topstories/nation/957206/2-3-million-filipino-students-benefit-from-free-college-ched/story)
- **2020 (older):** 1,975 HEIs (246 public, 1,729 private), excluding SUC satellite campuses. — [Wikipedia: Higher education in the Philippines](https://en.wikipedia.org/wiki/Higher_education_in_the_Philippines)
- **Enrollment:** 4.79 million total HE enrollment as of December 31, 2023, with 2.74 million (57.2%) in public HEIs (the share is per the report). No national AY 2024-25 figure was found. — [Malaya](https://malaya.com.ph/news/women-enrolled-in-masters-programs-outnumber-men-7-to-3-ched)
- **Webometrics coverage of PH:** the January 2023 edition listed **365** PH HEIs. January 2020 listed **277**, and July 2016 listed **271**. — [UPOU (2023/2020 counts, via search)](https://www.upou.edu.ph/news/up-leads-countrys-webometrics-world-ranking-upou-ranks-22nd); [Varsitarian (2016)](https://varsitarian.net/?p=15572). The 2024-2025 editions (UP Diliman ranked #1 in PH in January 2025) were reported without a total count. — [UP](https://up.edu.ph/upd-leads-january-2025-webometrics-rankings-up-system-upm-websites-also-in-top-ten/); [PhilStar 2025](https://www.philstar.com/headlines/2025/02/10/2420455/diliman-tops-philippines-universities-webometrics-list)
- **SUCs (top tier):** a 2018 study (Ventayen, Pangasinan State University, *Indian Journal of Science and Technology* 11(35)) evaluated **all 114 SUC websites** in four categories; UP and Visayas State University ranked at the top. This implies every SUC had a site to evaluate in 2018. The full text was not opened, so broken or unavailable sites, if any, are not confirmed. — [i-scholar abstract](https://i-scholar.in/index.php/indjst/article/view/180149); [PDF](https://sciresol.s3.us-east-2.amazonaws.com/IJST/Articles/2018/Issue-35/Article2.pdf)
- **SUCs must have websites:** under NBC 542 / GAA Sec. 93 (2012), SUCs must post a Transparency Seal on their official websites, and this is tied to PBB eligibility. — [BMB](https://bmb.gov.ph/?p=848); [EVSU](https://www.evsu.edu.ph/?p=155)
- **Facebook reach:** 4icu ranks PH colleges by Facebook following; for example, Arellano University has about 276,000 followers. — [4icu Facebook PH](https://4icu.org/facebook/ph)
- **Aggregator coverage:** Edukasyon.ph claims 2,000+ universities, 80,000+ courses, and 4,000+ scholarships in its directory. — [Manila Bulletin 2021](https://mb.com.ph/2021/03/12/school-reviews-ratings-introduced-to-enhance-students-school-search-experience)

### Inferences
- Short answer to "Meron pa bang university na walang website?": all SUCs effectively have a website, because Transparency Seal and PBB rules require one and the 2018 census-style study covered all 114. Many small private colleges and some LUCs likely do not have a proper website. Webometrics, which crawls any HEI domain, only detected about 365 PH HEIs in 2023, against about 2,000-2,400 HEIs. Treat this as an upper-bound proxy for weak web presence, not a measure of "no website": Webometrics may skip tiny sites or sites without academic outputs, and its counts are by institution, not by campus.
- The Facebook-only phenomenon is plausible and widely observed anecdotally (e.g., UP Visayas announced its own defacement on its Facebook page), but no quantified source was found.
- Use "about 2,000 institutions / about 2,400 campuses" with an explicit definition when citing totals.

### Gaps
- No survey, CHED directory field, or academic study gives the % of PH HEIs with a website vs. Facebook-only. A feasible method: sample the CHED HEI directory and check domains.
- No current (2024-2026) Webometrics PH total; webometrics.info was unreachable from this environment.
- The column headers of the CHED AY 2024-25 table could not be verified directly (503), so the type mapping above is inferred.
- No national AY 2024-25 enrollment figure was found.

## 2. Studies on PH HEI/SUC website quality, usability, accessibility (WCAG) and Transparency Seal compliance

### Takeaway
Every study found reports poor accessibility. A June 2026 study of 17 SUCs (one per region) found **0 of 17 fully compliant** with WCAG 2.1 and national standards, and only **2 of 17** at an "Enhanced Web Presence" maturity level. Earlier studies (2018-2025) likewise found no SUC achieving acceptable WCAG compliance, "regardless of academic prestige."

### Cited Findings
- **Lagura et al. (2026)**, "Web Accessibility and Institutional Readiness for Inclusive Governance in Philippine Higher Education," *Public and Private Management* 33(1), published June 9, 2026 (Davao del Norte State College). Sample: 17 SUC websites, one per region. Methods: mixed methods, automated tools plus qualitative usability analysis, against WCAG 2.1, RA 10754, and DICT MC 2017-004. Findings: **none of the 17 fully compliant**; **only 2/17 reached "Enhanced Web Presence."** The abstract states PH websites "have failed to comply with the basic accessibility standards." — [TCI-ThaiJo](https://so03.tci-thaijo.org/index.php/ppmjournal/article/view/294027); [PDF](https://so03.tci-thaijo.org/index.php/ppmjournal/article/download/294027/194298/1403521)
- **Agtang & Nisperos (2025)**, "Web Accessibility Assessment and Ranking of State Universities and Colleges in the Philippines," *JISEM* 10(43s), May 7, 2025. Tools: WAVE and TAW against WCAG 2.0. Reports significant challenges under the Perceivable and Operable guidelines. MPSPC had the lowest mean error rate (0.33), followed by PRMSU and GSU. The sample size was not visible on the abstract page. — [JISEM](https://jisem-journal.com/index.php/journal/article/view/8289)
- **Ilocos Region SUC study:** applied WCAG-EM with TAW and WAVE (WCAG 2.0) and found that **all SUC websites tested failed to achieve acceptable accessibility compliance, regardless of academic prestige** (per search summary; author and year not confirmed, possibly the same research group as Agtang & Nisperos). — [search result cluster incl. MDPI/preprints; unconfirmed attribution](https://jisem-journal.com/index.php/journal/article/view/8289)
- **Ventayen (2018):** evaluated all 114 SUC websites in four categories; UP and VSU ranked at the top. — [IJST PDF](https://sciresol.s3.us-east-2.amazonaws.com/IJST/Articles/2018/Issue-35/Article2.pdf)
- **Chua (2014, Batangas State University):** digital governance across SUC websites, descriptive-correlational design with a questionnaire applied to each SUC site. — [core.ac.uk](https://core.ac.uk/download/234644762.pdf) (details not verified)
- **Other:** "Web Satisfaction Rating and Comparison of State University and Colleges Web Rankings" (PSU journal) — [IJSTE PSU](https://ijste.psu.edu.ph/index.php/about/article/view/2); "A comparative study of websites of selected colleges and universities in Manila" (DLSU) — [Animo Repository](https://animorepository.dlsu.edu.ph/faculty_research/11668). Findings not extracted.
- **Legal and standards baseline:** DICT memo circular adopting WCAG 2.0 as the PH government web standard — [DICT MC 2019-04 text](https://www.pwag.org/wp-content/uploads/2020/01/DICT-Memo-Circular-2019-04-txt-format.txt); counter-example of good practice: UP Baguio publishes an accessibility statement — [UPB](https://www.upb.edu.ph/accessibility-statement)
- **Transparency Seal:** required on SUC official websites under GAA 2012 Sec. 93 / NBC 542; typical contents include mandate, officials, budgets, and PBB scorecards. — [BMB](https://bmb.gov.ph/?p=848); [NISU example](https://nisu.edu.ph/index.php/administration/good-governance/transparency-seal); [UA example](https://www.antiquespride.edu.ph/ua-transparency-seal). PBB under AO 25 continues: the 2026 DBM resolution covers FY 2024 PBB, and EO 61 (2024) had suspended AO 25 pending review. — [DBM Res. 2026-1](https://www.dbm.gov.ph/wp-content/uploads/Issuances/2026/Resolution/RESOLUTION-NO.-2026-1-and-MEMORANDUM-CIRCULAR-NO.-2026-1-updated.pdf); [DBM EO 61 TWG](https://www.dbm.gov.ph/wp-content/uploads/Issuances/2025/Resolution/THE-EO-NO.-61,-s.-2024-TWG.pdf). One SUC (DMMMSU) reported ongoing non-compliance in some accountability requirements, resolved on appeal. — [DMMMSU](https://www.dmmmsu.edu.ph/?p=33167)

### Inferences
- Typical quality problems, synthesized from the studies: WCAG failures in perceivability (alt text, contrast) and operability (keyboard), low digital maturity (mostly "basic presence"), and compliance-driven content (Transparency Seal PDFs) rather than user-centered admissions info.
- A public website module that meets WCAG 2.1 AA, ships Transparency Seal pages out of the box, and is mobile-first would directly address documented gaps.

### Gaps
- No study found that measures Transparency Seal compliance rates across SUCs (% compliant).
- No studies found that cover private HEI or LUC website quality at scale.
- Exact error counts and scores from Lagura 2026 and Agtang & Nisperos 2025 need the full PDFs.

## 3. How PH students find program/admissions info; role of Facebook pages vs official websites

### Takeaway
No Philippine-specific study quantifying information sources for admissions was found. Evidence is indirect: Facebook is near-universal among Filipino students, HEI Facebook pages have large followings, CHED itself treats its Facebook page as a primary official channel, and aggregators such as Edukasyon.ph claim large audiences. Fake and impostor Facebook pages are a recurring problem, which strengthens the case for an authoritative official website.

### Cited Findings
- 98% of surveyed (Leyte Normal University tourism) students access Facebook daily (2019, learning context). — [Zenodo PDF](https://zenodo.org/records/5559530/files/Facebook%20as%20a%20Learning%20Management%20System%20for%20Filipino%20JES%202019%20pp65-72.pdf)
- HEI Facebook following ranking (e.g., Arellano University about 276,000). — [4icu](https://4icu.org/facebook/ph)
- CHED lists three official channels: Facebook (PhCHED.gov), X (@PhCHED), and the website ched.gov.ph. It repeatedly warns against unofficial Facebook pages posting fake scholarship info and urges the public to rely on official websites and verified accounts. — [Inquirer](https://newsinfo.inquirer.net/1867070/ched-warns-vs-unofficial-fb-pages-posting-false-info-on-scholarships); [Rappler fact check](https://www.rappler.com/newsbreak/fact-check/education-subsidy-application-links-not-ched-unifast/); [VERA Files](https://verafiles.org/articles/fact-check-fb-posts-from-ched-impostors-promote-fake-scholarship-offer)
- CHED (November 2025) points the public to the official website and Regional Offices for verified lists of programs (diploma-mill crackdown), and with DepEd and PRC plans an online national registry. — [MB Nov 5, 2025](https://mb.com.ph/2025/11/05/ched-warns-public-against-diploma-mills-vows-crackdown-on-unauthorized-graduate-programs); [MB Nov 12, 2025](https://mb.com.ph/2025/11/12/ched-deped-prc-to-launch-online-national-registry-to-curb-diploma-mills-ensure-quality-teacher-education)
- Edukasyon.ph: 650,000 registered users and 10 million visitors (time frame unstated); 3,500+ school reviews after ReviewED launched (2021). — [Manila Bulletin 2021](https://mb.com.ph/2021/03/12/school-reviews-ratings-introduced-to-enhance-students-school-search-experience)
- Google data: engineering was the most-searched college degree in PH (2023), showing that search engines are a discovery channel. — [PhilStar 2023](https://philstar.com/nation/2023/04/13/2258479/engineering-philippines-most-searched-college-degree-google-data)
- The DFA advises verifying HEI and program status through CHED (official channels). — [DFA London](https://londonpe.dfa.gov.ph/advisories/1697-verification-of-status-of-higher-education-institutions-heis-and-their-programs)

### Inferences
- In practice, Facebook pages are the day-to-day announcement channel (admissions schedules, results, suspensions), while websites serve as the authoritative reference (programs, requirements, Transparency Seal, portals). Integrating Facebook (e.g., auto-crossposting announcements, with the website as the canonical source) matches student behavior.
- Impostor-page problems give an official domain (.edu.ph) a trust and verification role.

### Gaps
- No PH survey found with percentages of students using Facebook vs. websites vs. aggregators for admissions info.

## 4. Notable incidents: hacked/defaced sites, breaches, NPC cases

### Takeaway
PH university websites and portals have a long incident history: defacements (UP 2012, UP Visayas 2018, Cebu Normal University subdomain), a wave of mass defacements in 2018 that drew NPC summonses, a cluster of student-portal breaches in 2020 (PUP, FEU, San Beda), plus DLSU and USeP incidents. The NPC has issued formal resolutions against universities (e.g., UP Visayas, NPC BN 18-045, 2022).

### Cited Findings
- 2012: UP website defaced; UP said no sensitive data was compromised. — [Inquirer](https://newsinfo.inquirer.net/181613/university-of-the-philippines-hits-hacking-of-its-website/amp)
- 2018: NPC summoned officials of agencies and schools (Taguig City University, Republic Central Colleges, Laguna State Polytechnic University, among others) after website attacks exposed data of about 2,000 people (names, addresses, phones, emails, some passwords), and asked why the NPC and data subjects were not notified. The DPA requires notifying the NPC within 72 hours. — [PhilStar Apr 2018](https://www.philstar.com/other-sections/education-and-home/2018/04/26/1809404/government-agencies-schools-summoned-over-data-breach); [Rappler](https://www.rappler.com/nation/200936-national-privacy-commission-summons-officials-security-breach); [NPC](https://privacy.gov.ph/?p=9953)
- 2018: UP Visayas site (upv.edu.ph) defaced and taken down; announced via its Facebook page. — [Rappler](https://www.rappler.com/technology/263568-up-visayas-down-after-defacement/). NPC resolution: In re UP Visayas, NPC BN 18-045 (November 10, 2022). — [NPC PDF](https://privacy.gov.ph/wp-content/uploads/2024/04/NPC-BN-18-045-2022.11.10-In-re-University-of-the-Philippines-Visayas-Resolution-Final.pdf)
- 2020: PUP and FEU student portals hacked, with FEU reporting possible exposure of about 1,000 students' data; San Beda student portal hacked. — [MB June 19, 2020](https://mb.com.ph/2020/06/19/pup-feu-probe-hacking-of-student-portals); [MB June 7, 2020](https://mb.com.ph/2020/06/07/san-beda-student-portal-hacked/)
- Cebu Normal University suspended a subdomain after an "Anonymous" hack. — [Rappler](https://rappler.com/technology/cebu-normal-university-suspends-subdomain-anonymous-website-hack)
- DLSU: a data security incident took down its online systems. — [Unbox](https://unbox.ph/news/data-security-incident-downs-dlsu-online-systems/)
- USeP: breach with malicious redirection codes; it migrated servers and suspended the affected system. — [SunStar Davao](https://www.sunstar.com.ph/davao/usep-upgrades-cybersecurity-after-breach)
- Older: Indian hackers leaked data from Panpacific University North Philippines. — [Softpedia](https://news.softpedia.com/news/Indian-Hackers-Leak-Data-from-Panpacific-University-North-Philippines-269806.shtml). UST's Varsitarian commented on repeated campus hacks and the need for investment. — [Varsitarian](https://varsitarian.net/hacked-here-hacked-there-investments-needed-to-repel-cyberattacks/)

### Inferences
- Security requirements for a public site plus portal: hardened CMS (no outdated plugins), separation of the public site from the student portal, WAF/CDN, malicious-redirect and defacement monitoring, a DPA 72-hour breach notification workflow, privacy notice and DPO contact, and subdomain inventory (to prevent abandoned subdomains).

### Gaps
- No 2024-2026 PH university incidents surfaced in searches; the NPC site was not searched exhaustively.
- No sources found on expired or lapsed .edu.ph domains.

## 5. Do rankings or accreditation consider web presence?

### Takeaway
Webometrics is entirely web-based (visibility via backlinks is the dominant weight). QS uses the Webometrics "Web Impact" indicator (5%) only in some regional rankings (Arab Region, Latin America), not in QS Asia or World as far as found. THE does not use web presence. No evidence was found on whether AACCUP, PAASCU or CHED autonomy criteria explicitly score websites; for SUCs, the website is indirectly mandatory through the Transparency Seal and PBB.

### Cited Findings
- Webometrics methodology: Visibility (backlinks via Ahrefs/Majestic) about 50%, plus Transparency/Openness and Excellence (top-cited papers). Weights have changed across editions and the Presence indicator was discontinued; sources disagree on current weights. — [IREG Observatory](https://ireg-observatory.org/en/news/webometrics-the-most-inclusive-global-ranking); [AUEB](https://www.aueb.gr/en/node/17506)
- QS: 5% Webometrics Web Impact in the QS Arab Region and Latin America & Caribbean rankings. — [QS Support](https://support.qs.com/hc/en-gb/articles/4404752116882)
- PH universities publicize Webometrics results (UP, DLSU, Silliman, etc.). — [UP 2025](https://up.edu.ph/upd-leads-january-2025-webometrics-rankings-up-system-upm-websites-also-in-top-ten/); [PhilStar DLSU 2024](https://philstar.com/headlines/2024/08/07/2376002/la-salle-tops-philippines-university-webometrics-ranking-2024); [Silliman](https://su.edu.ph/?p=17582)
- CHED reports a growing number of globally ranked PH HEIs (173). — [The Post](https://thepost.net.ph/news/nation/phs-globally-ranked-heis-up-by-82-at-173-ched/); [Inquirer](https://newsinfo.inquirer.net/1991435/ched-more-ph-heis-globally-ranked-accelerating-internationalization)

### Inferences
- A good website directly improves the Webometrics standing (backlinks, open repository, Google Scholar profiles) and supports internationalization goals that CHED tracks. For SUCs, PBB money depends on website-hosted Transparency Seal content.

### Gaps
- AACCUP, PAASCU, PACUCOA and CHED autonomy/deregulation criteria (CMO 12 s. 2021?) were not verified for explicit website or web-presence indicators. Searches returned nothing.
- Whether QS Asia includes a web indicator was not confirmed.
