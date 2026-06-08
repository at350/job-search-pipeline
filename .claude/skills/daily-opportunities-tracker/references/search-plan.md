# Search Plan: the portal & query directory

This is the operational backbone of the daily sweep. The main `SKILL.md` lists *what kinds* of opportunities to look for; this file lists *exactly where and how to look*, with copy-pasteable URL patterns and query templates.

Why this file exists: the failure mode of a daily research digest is doing a handful of generic web searches, finding the same well-indexed programs every time, and missing the long tail of roles that live on individual company boards no aggregator has crawled yet. A precise, repeatable search plan is what turns "I searched the web" into real coverage. Work through the tiers below. Tier 1 and Tier 2 are the per-run floor (see the Coverage Contract in SKILL.md); Tiers 3-4 rotate.

## Contents
1. Tier 1, Direct ATS search (highest leverage, often skipped)
2. Tier 2, Live aggregators & trackers
3. Tier 3, Startup & VC-portfolio job boards
4. Tier 4, Category-specific aggregators
5. Query template bank
6. How to read results (what counts as a real hit)

---

## Tier 1: Direct ATS search (do this every run)

Most companies post on a hosted applicant-tracking system (ATS) long before the role shows up on LinkedIn or a GitHub tracker. You can search across *all* companies on a given ATS with a search engine's `site:` operator. This is the single best way to find roles early, and it is the part most runs skip. Run each of these and read the first 2-3 pages of results.

**Greenhouse** (used by most mid-to-late startups and many funds):
- `site:job-boards.greenhouse.io "Summer 2027" intern`
- `site:boards.greenhouse.io "2027" (intern OR internship) (engineer OR "machine learning" OR data OR research)`

**Lever:**
- `site:jobs.lever.co "2027" intern`
- `site:jobs.lever.co (internship OR intern) ("machine learning" OR "AI" OR research)`

**Ashby** (common at newer AI startups, Cursor, many YC cos):
- `site:jobs.ashbyhq.com intern 2027`
- `site:jobs.ashbyhq.com (internship OR "early career") (AI OR ML OR research OR engineer)`

**Workday** (big tech / enterprise; URLs vary, but the pattern works):
- `site:myworkdayjobs.com "Summer 2027" intern software`
- `"2027 summer intern" (software OR "machine learning") site:myworkdayjobs.com`

**Rippling / SmartRecruiters / Workable** (rotate one per run):
- `site:jobs.rippling.com intern 2027`
- `site:jobs.smartrecruiters.com 2027 intern (AI OR data OR engineer)`

Tip: swap the season each run (`"Summer 2027"`, `"Winter 2027"`, `"Fall 2026"` for academic-year-aware ones), and swap the role keyword (`"machine learning"`, `"applied AI"`, `quant`, `data scientist`, `"forward deployed"`, `product`). One ATS x one season x one role keyword is one search; budget roughly 6-10 of these per run.

---

## Tier 2: Live aggregators & trackers (do this every run)

These are crawled or community-maintained, so they refresh on their own. Hit the GitHub trackers and HN thread every run; rotate the rest.

**GitHub internship trackers** (read the raw README, which is the actual list):
- SimplifyJobs Summer 2027: `https://github.com/SimplifyJobs/Summer2027-Internships` (raw: `https://raw.githubusercontent.com/SimplifyJobs/Summer2027-Internships/dev/README.md`)
- vanshb03 Summer 2027: `https://github.com/vanshb03/Summer2027-Internships`
- speedyapply: `https://github.com/speedyapply/2026-SWE-College-Jobs` (and any 2027 successor)
- Note: early in a cycle these repos may still be mostly the prior year, so check the dates rather than assuming freshness.

**Hacker News "Who is Hiring?"** (first weekday of each month; indexed by no aggregator):
- `https://hnhiring.com/` (current month), filter for "intern" and remote
- Algolia search within the monthly thread: `https://hn.algolia.com/?query=intern&type=comment`

**Other aggregators (rotate ~2-3 per run):**
- 80,000 Hours job board: `https://jobs.80000hours.org/`, high-signal AI/policy/research roles + fellowships
- aisafety.training: `https://www.aisafety.training/`, the single best AI-safety/alignment deadline board
- John Gannon's VC job board: `https://www.johngannonblog.com/vc-jobs/`, VC analyst/scout/intern roles
- Levels.fyi internship leaderboard: `https://www.levels.fyi/internships/`
- ColorStack / Rewriting the Code opportunity boards
- The Forage (virtual experience programs): `https://www.theforage.com/`
- ProFellow: `https://www.profellow.com/`, fellowship deadline database
- Devpost trending: `https://devpost.com/hackathons` · MLH season: `https://mlh.io/seasons`
- ETHGlobal: `https://ethglobal.com/events`, travel-covered crypto hackathons

---

## Tier 3: Startup & VC-portfolio job boards (rotate, ~3-4 per run)

This is the richest vein for the early-stage AI roles that match the candidate's profile, and almost nothing here is indexed by the generic trackers. Most VC firms run a shared "talent network" job board across their whole portfolio (frequently powered by Getro or Consider), so one board surfaces dozens of vetted startups at once.

**General startup boards:**
- Wellfound (formerly AngelList Talent): `https://wellfound.com/jobs`, filter Internship + remote/role
- Y Combinator Work at a Startup: `https://www.workatastartup.com/` (search `intern`; YC-vetted)
- Built In: `https://builtin.com/jobs/internships`

**VC-portfolio talent boards** (each is a single board spanning that firm's portfolio, rotate through them):
- a16z: `https://portfoliojobs.a16z.com/jobs`
- Sequoia: `https://jobs.sequoiacap.com/jobs`
- General Catalyst: `https://jobs.generalcatalyst.com/`
- Greylock: `https://jobs.greylock.com/`
- Bessemer (BVP): `https://jobs.bvp.com/`
- Lightspeed: `https://jobs.lsvp.com/`
- Index Ventures: `https://jobs.indexventures.com/jobs`
- Founders Fund / Khosla / Thrive / Benchmark, search `"<firm> portfolio jobs"` to find the current board URL.

Query template for these: open the board, filter to Internship + Engineering/Data/Research, and read role + dates. When a board has no internship filter, search the page for `2027` and `intern`.

---

## Tier 4: Category-specific aggregators (rotate, tie to the daily rotation slice)

Match these to whichever named-program category the run is rotating through that day (see the rotation discipline in SKILL.md):
- **AI fellowships / safety:** aisafety.training, 80,000 Hours, GovAI openings page, EA Forum opportunities.
- **Founder / builder:** firm pages directly (Z Fellows, Emergent Ventures, EF, Neo, Contrary, South Park Commons), plus Sifted for EU.
- **VC scouts / fellows:** Dorm Room Fund, Contrary, firm "fellows" pages.
- **Quant / trading:** firm career pages (Jane Street, Citadel, Five Rings, HRT, Optiver, SIG, IMC, Aquatic) plus their direct ATS.
- **Research / REU:** nsf.gov REU search, DOE SULI, NASA, lab pages.
- **Conferences / affinity:** GHC/AnitaB, Tapia, SHPE, NSBE, ColorStack, RTC, SEO, MLT.
- **APM / product:** APMList.com.
- **Aerospace:** Brooke Owens, Matthew Isakowitz, Patti Grace Smith, Zed Factor pages.

---

## Query template bank

Reusable shapes. Replace the bracketed parts each run.

**Season-specific internships (use quoted phrase, engines ignore unquoted years):**
- `"Summer 2027" [role] internship application open`
- `"Winter 2027" [AI OR ML OR data OR quant] intern`

**Discovery (find programs you don't know yet):**
- `new [AI fellowship OR founder program OR VC scout] 2026 application open undergraduate`
- `[city] tech week 2026 student events schedule`
- `[firm] sophomore [insight OR diversity] program 2027 application`

**LinkedIn quoted-phrase** (needs the user's logged-in browser via Claude in Chrome; read-only, scroll the lazy-loaded results pane and read cards from screenshots):
- `https://www.linkedin.com/jobs/search/?keywords=%22Summer%202027%22&f_E=1&f_F=eng%2Cit&sortBy=DD`
- Repeat with `keywords=%22Winter%202027%22`. `f_E=1` = internship level; `f_F=eng,it` = Engineering + IT.

**Handshake** (school portal): handled by the separate `handshake-scan` skill, do not hand-search it. See its scan-method notes in `opportunities/opportunities-state.md`.

---

## How to read results (what counts as a real hit)

- A "hit" is a specific, actionable opportunity: a named program/role with an apply path and a deadline (or an honest "rolling"/"unconfirmed, verify"). A blog post *about* internships is not a hit.
- Verify every deadline on the official source before listing it (search results lag reality, so closed programs often still show as open). See OPERATING DISCIPLINE rule 1 in SKILL.md.
- Dedupe against `opportunities/opportunities-state.md` and `job_search_tracker.csv` before listing, per the dedup rule in the state file.
- When a search returns only already-known items, that is still a useful result: it means coverage of that source is current. Log it in the run's coverage log (see SKILL.md) rather than silently dropping it.
