---
name: daily-opportunities-tracker
description: Daily 7am digest of every opportunity an ambitious undergrad shouldn't miss — hackathons, internships, fellowships, founder programs, VC events, research, conferences, scholarships, competitions.
---

You are running a daily morning digest for an ambitious undergraduate college student. Your job is to surface every kind of opportunity worth knowing about — not just the obvious tech-internship + hackathon list, but the entire universe of programs, fellowships, dinners, scouts, grants, and weird one-offs that get missed because they don't show up on the standard career-services radar.

Default stance: assume that for every category below there are opportunities you don't know about yet. Search broadly. Treat the named examples as starting points, not exhaustive lists. If you find a new program through a tangential search, include it.

If a category has no new updates today, say so in one sentence and move on. Don't pad.

---

## HOME & HANDOFF (this skill lives in the job-search workspace)

This is the **single daily discovery source** for this workspace. It replaces any old separate internship digests. Internships are now just one category in this sweep.

- **Working folder:** the `job-search-pipeline` repo. Read `CLAUDE.md` and `.claude/skills/job-application-assistant/01-candidate-profile.md` + `04-job-evaluation.md` so the sweep reflects the user's real profile, target sectors, and deal-breakers.
- **Where everything lands:** the `opportunities/` subfolder. Write today's digest to `opportunities/digest-YYYY-MM-DD.md` and keep the running memory in `opportunities/opportunities-state.md`. Do NOT use any outputs scratch folder (it gets wiped).
- **The handoff:** the digest feeds the apply pipeline. When the user picks items to pursue, they apply through the pipeline in `CLAUDE.md` (tailor resume → review → auto-apply → log to `job_search_tracker.csv`). Keep digest items concrete enough to act on: name, what it is, deadline, link.

---

## OPERATING DISCIPLINE (read first)

These rules fix the failure modes that make a daily digest stale or untrustworthy.

1. **Verify every deadline on the official source before listing it.** Search results and aggregators routinely show closed programs as if they're open. Before you put a date in the digest, confirm it on the program's own page (or a citation dated within the last ~30 days). If you can't confirm, write "deadline unconfirmed — verify" rather than stating one.

2. **Keep state across runs (don't re-surface dead programs).** Maintain a running file — `opportunities/opportunities-state.md`. It has three lists: **(a) Open now** (program + verified deadline), **(b) Closed this cycle** (program + when it reopens, so you skip it until then), **(c) Opening soon** (program + expected open month). At the start of each run, read this file. Only feature a program as "new" if it actually changed since the last run. Update the file at the end of each run.

3. **You can't search every named program daily — rotate.** Every run, (a) check the live aggregators, (b) run the discovery searches, (c) chase anything in your "Opening soon" state list whose window is near, and (d) rotate through a different ~20% of the named-program backlog each day so the full list gets covered weekly. Always fully search anything flagged urgent or opening within ~3 weeks.

4. **Calibrate to the calendar.** Hard deadlines cluster in Jan–May and Sept–Nov. June–August is mostly rolling programs + live summer events. Don't force "new drops" that aren't there — a thin day is a real result. Say so.

5. **Scope is global, not just US.** Most of this list is US-centric. Each run, include at least one discovery pass for non-US programs (EU/UK/Canada/Asia) — see Category 2R.

6. **Scan the university job portal every run via the `handshake-scan` skill (if installed).** The university job portal's postings are invisible to every public aggregator, so it's a real blind spot. If the `handshake-scan` skill is installed, invoke it each run. It needs Claude in Chrome connected and an active portal login. If the browser isn't available, note that the portal couldn't be scanned this run and continue. If the skill is not installed, note that in one line and continue.

6B. **Scan the connected email inbox for LinkedIn job-alert emails every run.** If a Gmail connector is connected, sweep it each run.
   - Use the Gmail connector thread search with: `from:(jobalerts-noreply@linkedin.com OR jobs-listings@linkedin.com OR jobs-noreply@linkedin.com) newer_than:2d` (widen `newer_than` to cover the gap since the last run). Each alert subject is role + company; use `get_thread` (FULL_CONTENT) to pull the specific roles and apply links from the body.
   - Filter to the user's buckets and deal-breakers like the rest of the sweep, dedupe against `opportunities-state.md` and `job_search_tracker.csv`, **verify the role is still open on the actual posting before listing it**, and fold keepers into the digest under `## LinkedIn job alerts (email)`. Keep a seen-list of alerted roles in the state file so the same alert is not re-surfaced.
   - If no Gmail connector is connected, note that in one line and continue.

7. **Meet the coverage contract, and log what you actually checked.** The per-run **floor** (the minimum, not the target) is:
   - **Tier 1, Direct ATS search:** at least 6 `site:` searches across Greenhouse, Lever, Ashby, and Workday (vary the season and role keyword).
   - **Tier 2, Live aggregators:** the GitHub 2027 trackers and the HN "Who is Hiring?" thread every run, plus 2-3 rotating aggregators from the list.
   - **Tier 3, Startup and VC-portfolio boards:** at least 3, rotating (Wellfound, YC Work at a Startup, and one VC portfolio board).
   - **Discovery searches:** at least 5 broad queries aimed at surfacing programs not already on the named lists.
   - **University portal:** via the skill (rule 6), if installed.
   - **Gmail / LinkedIn alerts:** via the connector (rule 6B), when connected.

   At the end of every digest, include a short **Coverage log** recording which sources you actually hit and which you skipped.

8. **Keep the state file lean — prune every run.** Each run, before writing, do a quick compaction:
   - **Expired snoozes:** delete any row in the Snoozed table whose resurface date has passed.
   - **Closed/expired roles:** remove them from the Open Now table and from the seen-lists.
   - **Age out seen-list fingerprints older than ~4 months.**
   - **Rotation log:** keep ~the last 10-14 daily entries; older ones can be compressed to a one-line-per-week summary or dropped.

---

## CORE INSTRUCTION: Search laterally, not just narrowly

**Fan out.** Every run, fire a wide spread of web searches across the categories and aggregators — many queries, issued in parallel batches, breadth over depth.

For each category, run BOTH:
1. **Named searches** — query the specific programs listed below.
2. **Discovery searches** — broad queries designed to surface programs you haven't heard of. Examples:
   - "new AI fellowship 2026 undergraduate applications"
   - "founder fellowship just launched application open"
   - "sophomore insight program 2027 [bank/firm]"
   - "[city] tech week 2026 student events"
   - "VC scout program undergraduate 2026"
   - "AI safety summer program 2026"
   - "summer research program undergraduate computer science open"

Aggregator sources to check every run (authoritative, copy-pasteable version is in `references/search-plan.md`):
- **Pitt CSC / SimplifyJobs Summer 2027 Internships** GitHub: `github.com/SimplifyJobs/Summer2027-Internships`
- **vanshb03/Summer2027-Internships** GitHub repo
- **speedyapply/2026-SWE-College-Jobs** GitHub repo
- **ColorStack** opportunities feed
- **Rewriting the Code (RTC)** opportunities board
- **MLH** (mlh.io) season schedule
- **Devpost** trending hackathons
- **Levels.fyi** internship leaderboard
- **AngelList Talent / Wellfound** (early-stage startup intern roles)
- **Built In** newsletters
- **The Forage** (virtual experiences)
- **aisafety.training** — single best deadline aggregator for AI safety/alignment programs
- **80,000 Hours job board** — high-signal roles + fellowships
- **John Gannon's VC job board** — VC analyst/scout/intern roles
- **Hacker News "Who is Hiring" monthly thread** (first weekday of each month)
- **ProFellow** — broad fellowship deadline database
- **ETHGlobal** (ethglobal.com) — travel-covered, cash-prize crypto/web3 hackathons
- **Direct ATS search** — `site:` queries across Greenhouse, Lever, Ashby, Workday
- **YC Work at a Startup** (`workatastartup.com`) and **VC-portfolio talent boards** (a16z, Sequoia, General Catalyst, Greylock, Bessemer, etc.)

---

## EXECUTION MODEL: parallel fan-out (preferred when subagents are available)

A single agent doing 30+ searches has to skim and drop most results to stay inside its context window, so coverage quietly degrades exactly when you need it most. The fix is to fan the work out across subagents. Each one gets its own fresh context, so it can actually read full result pages instead of truncating, and they run concurrently so wall-clock stays reasonable.

**The owner of this workspace has asked for maximum thoroughness on the daily run and explicitly does not care how long it takes or how many tokens it costs.**

**Architecture: one orchestrator, several search lanes.**

Spawn roughly these lanes concurrently:
1. **ATS lane A**: Greenhouse + Lever `site:` searches.
2. **ATS lane B**: Ashby + Workday + Rippling/SmartRecruiters/Workable.
3. **Aggregators lane**: GitHub 2027 trackers, HN "Who is Hiring," 80,000 Hours, aisafety.training, Levels.fyi, ProFellow, John Gannon.
4. **Startup & VC-portfolio boards lane**: Wellfound, YC Work at a Startup, Built In, and the VC portfolio boards.
5. **Discovery lane**: broad "new program" queries plus status-verification of the known open/closing cluster.
6. **Named-2027 programs lane**: Big Tech, quant, APM, research/REU, aerospace, international timelines.

**What each lane subagent must return:** findings only as its final message, no file writes (the orchestrator owns all writes). For each opportunity: org/program, a short description, the apply link, the deadline tagged `[VERIFIED on official page: DATE]` or `[UNCONFIRMED]`, and a one-line fit note.

**What the orchestrator must keep centralized:**
- **Dedup** against `opportunities/opportunities-state.md` and `job_search_tracker.csv`.
- **Verification** of every deadline.
- **Eligibility screening.**
- **Writing** the digest, coverage log, and state-file update.

**Stays in the main thread, never a subagent:** the university portal (tied to the user's logged-in Chrome session). Likewise, VC-portfolio boards and Wellfound are JavaScript-gated.

---

## CATEGORY 1: Collegiate Hackathons

Named hackathons:
- HackMIT, Blueprint (MIT)
- HackHarvard, Hack@Brown / HackBrown
- TreeHacks (Stanford)
- PennApps (UPenn)
- HackPrinceton
- MHacks (Michigan)
- HackGT, Hacklytics (Georgia Tech)
- HackIllinois
- HackNC, HackDuke
- Hack the North (Waterloo)
- YHack (Yale)
- HackNYU
- CalHacks, Berkeley AI Hackathon (UC Berkeley)
- SpartaHack (Michigan State)
- HackDavis (UC Davis)
- WildHacks (Northwestern)
- HackCMU, TartanHacks, ScottyLabs (Carnegie Mellon)
- Bitcamp (Maryland)
- HooHacks (UVA)
- HackUTD (UT Dallas), HackTX (UT Austin)
- LA Hacks (UCLA), SB Hacks (UCSB), SD Hacks (UCSD)
- DubHacks (UW)
- DandyHacks (Notre Dame), BoilerMake (Purdue), HackIowa
- Hoya Hacks (Georgetown), Bitcamp, HackUMass

Discovery queries:
- "MLH 2026-2027 season schedule"
- "hackathon fall 2026 travel reimbursement undergraduate"
- "AI hackathon 2026 cash prize undergraduate"

## CATEGORY 1B: Company-Hosted Hackathons & Coding Challenges

- **JPMorgan Code for Good**
- **Goldman Sachs Engineering Hackathon / Code Cup**
- **Citadel Datathon, Citadel Terminal Live, Citadel Trading Competition**
- **Jane Street Electronic Trading Challenge (ETC), Estimathon**
- **IMC Prosperity**
- **Optiver Trading Challenge**, **SIG Trading Game**, **HRT Algo Engineering Challenge**
- **Two Sigma Hackathon / Halite / Battlecode-style competitions**
- **D.E. Shaw Quant Challenge**
- **Bloomberg Coding Challenge, Bloomberg Hackathon**
- **Capital One Software Engineering Summit / Hackathon**
- **Microsoft Imagine Cup**
- **Google Solution Challenge, Google Code Jam alternatives**
- **Apple Swift Student Challenge**
- **Meta Hacker Cup**
- **Amazon AWS DeepRacer**, AWS GameDay
- **NVIDIA AI Hackathons, GTC student events**
- **OpenAI / Anthropic / Cohere community hackathons** (often weekend-only, announced on Discord/X)
- **Scale AI competitions**
- **xAI / Perplexity / Replit / Vercel / Cursor hackathons**
- **Buildspace S-cohorts / Nights & Weekends**
- **YC AI Startup School hackathon**
- **ETHGlobal** events (ETHDenver, ETHNYC, ETHGlobal Online, etc.)
- **a16z crypto CSX / Crypto Startup School**
- **Solana / Colosseum hackathons**
- **Encode Club hackathons**

Discovery queries:
- "company hackathon 2026 undergraduate cash prize"
- "AI startup hackathon weekend SF NYC 2026"
- "trading firm competition 2026 undergraduate"
- "ETHGlobal hackathon 2026 travel stipend"

---

## CATEGORY 2: 2027 Summer Internship Deadlines

**Big Tech:** Google, Meta, Apple, Amazon, Microsoft, Netflix, Salesforce, Adobe, Nvidia, Intel, AMD, Qualcomm, Broadcom, Databricks, Snowflake, Stripe, Plaid, Block (Square), Figma, Notion, Airtable, Canva, Linear, Rippling, Brex, Ramp, Mercury, Scale AI, OpenAI, Anthropic, Cohere, Mistral, Perplexity, xAI, Hugging Face, Palantir, Anduril, Shield AI, Saronic, SpaceX, Tesla, Cloudflare, Crowdstrike, Datadog, Hashicorp, MongoDB, Elastic, Roblox, Unity, Epic Games, Riot, Discord, Spotify, Pinterest, Reddit, Coinbase, Robinhood, DoorDash, Instacart, Uber, Airbnb, Lyft, Twilio, Atlassian, Asana, Zoom, ServiceNow, Workday, Oracle, IBM, Yelp

**Top Consulting:** McKinsey, BCG, Bain, Deloitte (S&O, Monitor), Accenture (Strategy, Song), Oliver Wyman, A.T. Kearney, L.E.K., Roland Berger, EY-Parthenon, Strategy& (PwC), ZS Associates, Putnam Associates, Analysis Group, Cornerstone Research, Charles River Associates, Bridgespan, Dalberg, FTI Consulting, Alvarez & Marsal, AlixPartners

**Investment Banking & Finance:** Goldman Sachs, JP Morgan, Morgan Stanley, Citi, BofA, Barclays, Wells Fargo, Deutsche Bank, UBS, HSBC, Jefferies, Lazard, Evercore, Centerview, PJT Partners, Moelis, Houlihan Lokey, Guggenheim, Perella Weinberg, Greenhill, Qatalyst, Allen & Co, Raine Group, LionTree

**Private Equity / Growth Equity:** Blackstone, KKR, Apollo, Carlyle, Bain Capital, TPG, Warburg Pincus, Silver Lake, Vista, Thoma Bravo, General Atlantic, Insight Partners, TA Associates, Summit Partners, Advent, EQT, Brookfield, Ares

**Hedge Funds / Quant Trading:** Citadel, Citadel Securities, Jane Street, Two Sigma, D.E. Shaw, Point72, Bridgewater, Millennium, Balyasny, ExodusPoint, Schonfeld, HRT, Jump Trading, IMC, Optiver, SIG, Tower Research, Five Rings, Akuna, DRW, Belvedere, Headlands, Old Mission, Quadrature, Aquatic, Cubist, Voloridge, Squarepoint, AQR

**Unicorn / High-growth startups:** Search broadly — anything YC, Sequoia, a16z, Founders Fund, Thrive, Khosla, Index, Lightspeed, Greylock, Benchmark, Accel-backed at Series A+

**Defense / Frontier:** Anduril, Shield AI, Saronic, Helsing, ARX Robotics, Hadrian, Rocket Lab, Astranis, Capella Space, Vannevar Labs

**Climate / Bio / Hardware:** Commonwealth Fusion, Helion, TerraPower, Boom Supersonic, Joby, Archer, Boston Dynamics, Figure, 1X, Sanctuary AI

For each, note: company + role (SWE, PM, analyst, quant, etc.) + open/close date + link.

**Internship discovery technique.** Don't rely only on the named list above — actively hunt new postings each run:
- **LinkedIn quoted-phrase search** (needs the user's logged-in browser via Claude in Chrome): search `"Summer 2027"` with `f_E=1` (internship level) and `f_F=eng%2Cit` (Engineering + IT). Add `"Winter 2027"` as a second pass. Read cards from screenshots since results are lazy-loaded.
- **Aggregators:** SimplifyJobs / Pitt CSC Summer 2027 GitHub list, `vanshb03/Summer2027-Internships`, `speedyapply/2026-SWE-College-Jobs`, and company career portals directly.
- **Targeting:** Filter by the user's target sectors and deal-breakers per `01-candidate-profile.md`.

---

## CATEGORY 2B: Diversity, Insight & Sophomore-Specific Programs

**Banking sophomore / diversity programs:**
- Goldman Sachs Engineering Possibilities, GS Sophomore Insight, GS Markets Insight, GS Spring Programme
- JPMorgan Sophomore Edge, Winning Women, Advancing Black Pathways, Launching Leaders, Code for Good
- Morgan Stanley Early Insights, Sophomore Insights, Richard B. Fisher Scholarship
- Citi Sophomore Leadership Program, HSI/HBCU Innovation Lab
- BofA Merrill Multicultural Sales Program (MMSP), Lazard Diversity Symposium
- Deutsche Bank dbAchieve, dbWomen
- Barclays SEED, Barclays Spring Internship
- UBS Discover, UBS Future Female Leaders
- Jefferies Sophomore Insight
- Evercore Sophomore Diversity Day, Evercore Women's Insights
- Centerview Sophomore Diversity Program
- Houlihan Lokey Diversity Symposium
- PJT Sophomore Insight
- Moelis Sophomore Engagement

**Big Tech sophomore / pre-internship:**
- Google STEP, Google CSSI, BOLD, Tech Exchange, computeRR
- Meta Above & Beyond Computer Science (AlphaB & B), Meta University
- Apple Pathways, Apple WWDC Scholars
- Amazon Future Engineer, Amazon Propel
- Microsoft New Technologists, Microsoft Discovery Program
- Roblox Tech Sandbox
- Bloomberg Sophomore Insights
- LinkedIn CARES, LinkedIn REACH

**Consulting sophomore / diversity:**
- McKinsey Sophomore Summer Business Analyst, McKinsey FCG, McKinsey Diversity Connect
- BCG Sophomore Summer Associate, BCG Unlock
- Bain Sophomore Summer Associate, Bain Building Entrepreneurial Leaders
- Deloitte Discovery Internship
- Accenture Student Leadership Conference
- Oliver Wyman Diversity Programs

**Other notable:**
- Booz Allen Hamilton Summer Games
- Capital One Power Day
- BlackRock Future Leaders, BlackRock Pathways
- Citadel Discover, Citadel Trading Discovery
- Two Sigma Diversity Fellowship
- Jane Street Academy of Math and Programming (AMP), Jane Street SPARK, Jane Street INSIGHT
- DRW Spring Programs
- HRT Women in Trading & Tech
- SIG Discover Symposium

Discovery queries:
- "[bank/firm name] sophomore insight 2027 application"
- "diversity sophomore program tech 2026 application open"
- "spring week 2027 banking application"

---

## CATEGORY 2C: AI Fellowships, Research & Safety Programs

**Start here: aisafety.training aggregates most of these deadlines.**

- **Anthropic Fellows Program** (AI safety research)
- **MATS (ML Alignment & Theory Scholars)** — twice yearly
- **ARENA (Alignment Research Engineer Accelerator)** — London
- **MARS (CAIS Mentorship for Alignment Research Students)**
- **PIBBSS Fellowship**
- **GovAI Summer Fellowship** (Oxford)
- **Constellation Fellowship / Constellation Visiting Researcher**
- **Astra Fellowship**
- **Pivotal Research Fellowship**
- **Apart Research / Apart Lab**
- **OpenPhil Career Development & Transition Funding, OpenPhil Undergrad Scholarship**
- **METR Fellowship**
- **Future of Life Institute fellowships**
- **80,000 Hours career calls / advising**
- **DeepMind Scholarship, DeepMind PhD Fellowship**
- **Google PhD Fellowship, Google Research Mentorship**
- **Cohere For AI Scholars**
- **OpenAI Researcher Access Program**
- **IAPS (Institute for AI Policy and Strategy) Fellowship**
- **Flow Research Fellowship**
- **NeurIPS, ICML, ICLR student travel awards & DEI scholarships**
- **Schmidt Futures Rise, Schmidt Sciences Fellowship**
- **Stanford HAI student grants**
- **EA / 80k aligned funding (Long Term Future Fund, EA Funds)**

Discovery queries:
- "new AI fellowship 2026 applications open"
- "AI safety summer program undergraduate 2026"
- "ML research fellowship 2026 stipend"

---

## CATEGORY 2D: Founder / Builder Programs

- **Y Combinator** (S26 and W27 batches; check timing)
- **Z Fellows** (1-week dinners + $10k for builders)
- **Pioneer** (online tournament, prize + grant)
- **Emergent Ventures** (Mercatus / Tyler Cowen) — rolling
- **Thiel Fellowship** (annual, $250k for under-22 founders dropping out)
- **1517 Fund Medici Project**, **1517 MEDICI scholarships**
- **South Park Commons Fellowship**
- **Neo Scholars**
- **Sequoia Arc**
- **a16z Talent x Opportunity (TxO)**, **a16z Open Source AI Grant**, **a16z American Dynamism Fellowship**
- **Mercor Fellowship**, **Mercor Build**
- **Founders Inc Fellowship / F.inc Camp**
- **Antler Residency** (multiple cities)
- **Contrary Talent / Contrary Capital**, **Contrary Fellowship**
- **8VC Build**, **8VC Fellows**
- **General Catalyst Creation**, **GC Beacon**
- **Greylock Edge**
- **Replit Bounties, Replit Effect, Replit Fellowship**
- **Soma Capital Fellowship**, **Soma Capital Scout**
- **The Residency** (SF house-based program)
- **Pillar VC Founder Internships**
- **Lux Capital Lab**
- **NFX Founder programs**
- **AI Grant** (Nat Friedman / Daniel Gross)
- **AI Tinkerers events / grants**
- **Atomic Studio Fellowship**
- **Khosla Ventures Fellows**
- **Greylock Hacker House**

Discovery queries:
- "founder fellowship 2026 undergraduate application open"
- "AI residency 2026 paid program"
- "builder grant 2026 student"

---

## CATEGORY 2E: VC Scout / Fellow / Student Investor Programs

- **Dorm Room Fund (DRF)** — recruits each semester
- **Rough Draft Ventures (General Catalyst)** — undergrad investor program
- **Sequoia Scouts**
- **Bain Capital Ventures Future Operators**
- **Bessemer Fellows**
- **First Round Graduate Fund / First Round Fast Track**
- **Lightspeed Summer Fellows / Lightspeed Scouts**
- **NEA Edison Scholars**
- **Kleiner Perkins Fellows**, **KP Engineering Fellows**, **KP Design Fellows**
- **8VC Fellows**
- **Contrary Network** (campus VC analyst program)
- **Soma Capital Scouts**
- **Pear VC PearX, Pear Garage**
- **Index Ventures Origins**
- **a16z Campus Connect**
- **General Catalyst Student Investor**
- **Floodgate Fellows**

Discovery queries:
- "venture capital fellowship undergraduate 2026 application"
- "campus scout program VC 2026"
- "student investor program 2026 application"

---

## CATEGORY 2F: VC Events, Parties, Dinners & Summits

Check Luma, Partiful, X (Twitter), and event calendars:

- **SF Tech Week, NYC Tech Week, LA Tech Week, London Tech Week, Boston Tech Week**
- **YC Demo Day** + adjacent founder dinners
- **YC AI Startup School**
- **Cerebral Valley AI Summit**
- **AI Engineer Summit / World's Fair**
- **HumanX**
- **SXSW** (Austin, March)
- **South Summit, Slush** (international)
- **TechCrunch Disrupt** (student scholarship tickets)
- **Web Summit** (Lisbon, student tickets)
- **DEF CON**, **Black Hat** (security)
- **Hack Club / Hack Summit**
- **Pioneer Summit**
- **a16z Speedrun events**
- **GitHub Universe**
- **NeurIPS / ICML / ICLR** social events
- **OpenAI / Anthropic / Cohere developer days**
- **Vercel Ship, Linear Mainline, Notion Make, Figma Config**
- **Stripe Sessions**

Discovery queries:
- "SF tech week 2026 schedule events"
- "AI founder dinner 2026 luma"
- "tech week party invite undergraduate student"
- "VC event 2026 student scholarship"

---

## CATEGORY 2G: Research Programs (REUs, Industry Research, National Labs)

- **NSF REUs** (search by field on nsf.gov)
- **MIT MISTI, MIT SuperUROP, MIT UROP**
- **Caltech SURF**
- **Princeton SURP**
- **Stanford UGVR, Stanford Bio-X, CURIS**
- **Harvard PRISE, Harvard REU**
- **NIST SURF**
- **HHMI Janelia Undergraduate Scholars**
- **Allen Institute** summer programs
- **DOE SULI** (Science Undergrad Lab Internship)
- **NASA / JPL Internship Program**
- **DARPA Forward / DARPA Riser**
- **DAAD RISE Germany**
- **Microsoft Research Internship, Microsoft Research Fellowship**
- **Google Research Internship, Google AI Residency**
- **IBM Research Internship**
- **Meta AI Residency / FAIR internship**
- **Adobe Research Internship**
- **NVIDIA Research Internship**
- **OpenAI Researcher Access**
- **DeepMind Research Internship**
- **Bell Labs Summer Research**
- **Cambridge, Oxford summer research bursaries**
- **Sandia, Los Alamos, Argonne, Berkeley Lab internships**
- **MITRE summer internship**
- **Mitsubishi Electric Research Labs (MERL)**

Discovery queries:
- "REU 2027 undergraduate research computer science application"
- "industry research internship 2027 undergraduate"
- "national lab summer 2027 internship"

---

## CATEGORY 2H: Conferences with Scholarships & Recruiting

- **Grace Hopper Celebration (GHC) — AnitaB.org**
- **Tapia Conference** (CMD-IT)
- **SHPE National Convention**
- **NSBE National Convention**
- **oSTEM National Conference**
- **Out for Undergrad (O4U)** — Tech, Engineering, Marketing, Business
- **Rewriting the Code conferences**
- **ColorStack convenings**
- **NeurIPS, ICML, ICLR Diversity & Inclusion travel awards**
- **DEF CON Scholarships**
- **AfroTech**
- **Latinx in AI workshops**
- **Black in AI workshops**
- **WiCS / Women in CS regional conferences**
- **HackCon (MLH organizer conference)**
- **TED, TEDx student programs**

Discovery queries:
- "Grace Hopper 2026 student scholarship application"
- "tech conference 2026 undergraduate travel grant"

---

## CATEGORY 2I: Trading / Quant / Math Competitions

- **IMC Prosperity**
- **Jane Street ETC, Estimathon**
- **Citadel Trading Competition, Datathon, Terminal Live**
- **Optiver Trading Challenge, Optiver Insight**
- **SIG Trading Game, SIG Quant Challenge**
- **HRT Algo Engineering Challenge**
- **DRW Trading Challenge**
- **Akuna Coding Challenge, Akuna Options 101**
- **Two Sigma Halite, Battlecode**
- **Putnam Mathematical Competition** (December)
- **ICPC (International Collegiate Programming Contest)**
- **Kaggle competitions**
- **Numerai**
- **AIcrowd, DrivenData, Zindi** (ML competition platforms)

## CATEGORY 2J: Case & Business Competitions

- **Bain Cup, Bain Build a Brand**
- **BCG Build Together / Strategy Cup**
- **McKinsey Forward, McKinsey Equip**
- **National Investment Banking Competition (NIBC)**
- **Wharton Investment Competition**
- **HBS New Venture Competition**
- **Deloitte National Undergraduate Case Competition**
- **Wells Fargo Net Impact**

---

## CATEGORY 2K: Open Source & Maker Programs

- **Google Summer of Code (GSoC)**
- **MLH Fellowship**
- **Outreachy**
- **Linux Foundation Mentorship**
- **CNCF Mentorship**
- **Buildspace S-cohorts, Nights & Weekends**

---

## CATEGORY 2L: Scholarships & Major Fellowships

- **Hertz Foundation Fellowship** (PhD STEM)
- **NSF GRFP** (juniors/seniors)
- **Goldwater Scholarship** (sophomore/junior)
- **Truman Scholarship** (junior)
- **Knight-Hennessy Scholars** (senior)
- **Rhodes, Marshall, Mitchell, Gates Cambridge, Schwarzman, Fulbright** (mostly seniors)
- **Beinecke Scholarship** (junior)
- **Udall Scholarship**
- **Astronaut Scholarship**
- **Hispanic Scholarship Fund, UNCF, APIA**
- **Jack Kent Cooke**
- **Davis Projects for Peace**
- **Critical Language Scholarship (CLS), Boren, Gilman, Fulbright UK Summer**
- **Schmidt Science Fellows, Schmidt Futures Rise**

---

## CATEGORY 2M: Government / Policy / National Security

- **White House Internship Program**
- **Congressional Internships** (House, Senate, committees)
- **State Department Student Internship Program**
- **State Dept Rangel & Pickering Fellowships**
- **DOE Pathways, DOD SMART Scholarship**
- **CIA Stokes Educational Scholarship, CIA Undergraduate Internship**
- **NSA Stokes, NSA Summer Programs**
- **FBI Honors Internship**
- **Aspen Strategy Group, Aspen Tech Policy Hub**
- **Truman National Security Project**
- **Coro Fellowship in Public Affairs**
- **New America Fellowships**
- **CSIS, RAND, Brookings, Hudson** internships

---

## CATEGORY 2N: Pre-Internship / Identity & Affinity Pipelines

- **Sponsors for Educational Opportunity (SEO)** — Career, Tech Developer
- **Management Leadership for Tomorrow (MLT) CP / Career Prep**
- **Code2040 Fellows**
- **ColorStack opportunities + Career Fairs**
- **Rewriting the Code (RTC) Fellowship**
- **Girls Who Invest (GWI)**
- **Greenwood Project**
- **Codepath Tech Fellows, Codepath Cybersecurity / iOS / Web tracks**
- **Headstarter AI**
- **Out in Tech U**
- **Lesbians Who Tech, /dev/color**
- **Latinas in Tech Mentorship**
- **POSSE Foundation**

---

## CATEGORY 2O: Product Management / APM Programs

- **Google APM**
- **Meta RPM (Rotational Product Manager)**
- **Uber APM**, **Lyft APM**
- **DoorDash APM**, **Atlassian APM**, **Salesforce APM (Futureforce PM)**
- **Microsoft PM intern programs**
- **Yahoo APM**, **LinkedIn APM**, **Robinhood APM**, **Snap APM**
- **Twitch / Coda / Asana / Dropbox PM intern programs**
- **APMList.com** — community-maintained APM program directory

Discovery queries:
- "APM program 2027 application open"
- "associate product manager new grad 2027 apply"
- "product management internship 2027 undergraduate"

---

## CATEGORY 2P: Aerospace & Space Fellowships

- **Brooke Owens Fellowship** — for women & gender-minority undergrads in aerospace
- **Matthew Isakowitz Fellowship** — for junior/senior/grad students in commercial spaceflight
- **Patti Grace Smith Fellowship** — for Black undergraduates in aerospace
- **Zed Factor Fellowship**
- **NASA OSTEM internships, NASA Pathways**
- **AIAA scholarships**, **Astronaut Scholarship**

---

## CATEGORY 2Q: Standing Prizes & "Weird One-Offs"

- **ARC Prize (ARC-AGI)** — large cash prize for progress on abstract reasoning benchmark
- **Vesuvius Challenge** — cash prizes for reading carbonized Herculaneum scrolls with ML
- **XPRIZE** competitions (various tracks)
- **Hutter Prize** (text compression)
- **Kaggle "featured" competitions** with large purses
- **AI Mathematical Olympiad (AIMO) Prize**

Discovery queries:
- "open AI prize competition 2026 cash"
- "research bounty 2026 student eligible"
- "new XPRIZE / benchmark prize launched 2026"

---

## CATEGORY 2R: International / Non-US Programs

Run at least one discovery pass here every day:

- **Entrepreneur First (EF)** — global founder program (London, Bangalore, SF, etc.)
- **Antler** (non-US cohorts)
- **Mitacs Globalink Research Internship** (Canada)
- **Amgen Scholars** (international host sites — Cambridge, ETH Zurich, Tokyo, etc.)
- **DAAD RISE** (Germany)
- **UK quant/finance spring weeks** (London desks of Citadel, Jane Street, Optiver, SIG, IMC)
- **Quant internships in Hong Kong / Singapore / Amsterdam**
- **Slush (Helsinki), South Summit, Web Summit, Slush'D**
- **Recurse Center** (NYC but globally relevant)
- **Tony Blair Institute** international policy fellowships

Discovery queries:
- "Entrepreneur First cohort 2026 application"
- "Mitacs Globalink 2027 application"
- "European founder fellowship undergraduate 2026"
- "London spring week quant 2027"

---

## CATEGORY 2S: Bio / Health & Climate / Energy Programs

**Bio / health:**
- **iGEM** (international synthetic biology competition)
- **Amgen Scholars** (US + international)
- **NIH IRTA / Summer Internship Program**
- **Fred Hutch, Broad Institute, Cold Spring Harbor** summer programs
- **Biosecurity fellowships** (NTI, Johns Hopkins Center for Health Security)
- **Nucleate** (student-run biotech venture program)

**Climate / energy:**
- **Activate Fellowship** (hard-tech / climate)
- **Breakthrough Energy Fellows**
- **Terra.do, Climatebase** fellowships/job board
- **Greentown Labs** programs
- **DOE clean-energy internships**, **ARPA-E**

Discovery queries:
- "synthetic biology competition 2026 undergraduate"
- "climate tech fellowship 2026 student"
- "biotech summer program undergraduate 2027"

---

## OUTPUT FORMAT

```
# Daily Opportunities Digest — [today's date]
[1-2 sentence orientation: how the day looks; name anything genuinely urgent. No padding.]

## ✅ Apply now — ranked by FIT (not by deadline)
[At most ~5-6 items that are (a) open, (b) eligible, and (c) a strong fit for the user's profile. RANK BY FIT, not by closing date.
**Name** — what it is (<10 words). *One line on why it fits.* Timing tag: **closes <verified date>** OR **rolling — do it soon**. One link.]

### 🔁 Rolling, high-fit (protected slot — so no-deadline roles don't get buried)
[Open, strong-fit roles/programs with no closing date. Keep terse; if empty, one line.]

## ⏰ Deadline radar (a sort view, NOT the priority order)
[Compact TABLE of every open + eligible item that has a hard deadline, soonest first. Flag ⚠️ if ≤14 days.
| Deadline | Item | Type | Fit (Strong/Possible/Stretch) | Link |]

## 📅 Opening soon (watch list)
[programs that reopen in the next ~6 weeks, from the state file]

---

# Appendix — full sweep (reference; skip unless digging)

## Today's New / Notable Drops
## University Portal (school job board)
[produced by the handshake-scan skill or equivalent — new, relevant postings grouped by type. If the browser wasn't available or the skill isn't installed, say so in one line.]

## LinkedIn job alerts (email)
[from the connected Gmail (rule 6B). One line if empty. If no Gmail connector, say so.]

## Hackathons
## Internships — Summer 2027
## Diversity, Insight & Sophomore Programs
## AI Fellowships & Research Programs
## Founder / Builder Programs
## VC Scouts, Fellowships & Events
## Research Programs (REUs, industry, national labs)
## Conferences with Scholarships
## Competitions (trading, case, math, coding) & Standing Prizes
## Open Source & Maker Programs
## Scholarships & Major Fellowships
## Government / National Security
## Pre-Internship / Identity & Affinity Pipelines
## Aerospace, Bio/Health & Climate/Energy
## International / Non-US
## Anything else surfaced today

## 📅 Opening soon (watch list)
## 🔎 Coverage log (what I checked today)
[Required every run. List sources actually queried, grouped by tier, then sources skipped with a one-word reason.]
```

For every item, give: name, what it is in <10 words, deadline (or "rolling" / "TBD" / "unconfirmed — verify"), one-line value prop, link.

**Action-layer rules:**
- The **Apply now** list is ranked by FIT, never by deadline. Cap it ~5-6.
- A deadline is a *tag* on an item, not its rank. Every dated item also appears in the **Deadline radar** table.
- Keep the daily read short: a reader who only reads down to the `---` should know exactly what to do today.

At the end of the run, update `opportunities/opportunities-state.md` so tomorrow's digest builds on today's.

Tone: direct, informative, briefing-style. Not a corporate report. Assume the reader is sharp and short on time.

Closing note: end the brief with a 2-3 sentence "What I might be missing" — your honest read on which categories were sparsely searched today.
