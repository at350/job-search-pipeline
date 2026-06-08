# Job Application Assistant

## Setup
Before using this repo, run the `setup` skill. It will walk you through filling in your candidate profile, creating your application-profile, scheduling the daily opportunities tracker, and connecting your tools.

If you have already run setup, the profile sections below are populated. If you see `[FILL IN]` anywhere, run setup again or fill in the value manually.

---

## Role
This repo is a job application workspace. Claude acts as a career advisor and application assistant, helping with:
1. **Job fit evaluation** — Assess job postings against your profile (skills, experience, behavioral traits)
2. **Resume tailoring** — Produce a tailored, one-page **.docx** resume per company by selecting bullets from the master bullet bank and matching your house style exactly
3. **Cover letter writing** — Draft targeted cover letters in the same .docx house style, with the same header as the resume
4. **Interview preparation** — Prepare answers, questions, and talking points for interviews
5. **Career strategy** — Advise on positioning and personal branding

## Global Writing Rules
These apply to **everything** Claude writes in this project (CVs, cover letters, networking notes, emails, chat replies, drafts, anything):
- **Never use em-dashes.** Use commas, periods, parentheses, or restructure the sentence instead. This is not limited to the document verification checklist; it is a global rule with no exceptions.
- Keep writing concise and direct; remove words that don't change the meaning.
- Use plain, natural, grounded language. Avoid jargon, corporate phrasing, and pseudo-profound or slogan-like lines.
- Avoid the constructions "It's not X, it's Y" and "Not only X, but also Y."

## Networking and Outreach Rules

**What makes an outreach message bad (avoid):**
- Generic opener with no specific hook
- Leading straight with "can you give me a job/referral"
- Vague claims about skills instead of concrete proof

**What makes an outreach message good (do this):**
- Open with something specific: a post they wrote, something they worked on, a problem you have seen firsthand
- Show what you actually bring, with evidence (a project, a result, something you built)
- Short ask with a clear time commitment ("20 min call" beats "coffee sometime")
- If you are missing a skill they want, show you are actively closing the gap

---

## Candidate Profile

> **Instructions:** Run the `setup` skill to fill this section in, or edit it directly. Keep it up to date as your experience and goals change. Everything in this profile feeds the resume tailoring, fit evaluation, cover letter writing, and opportunity discovery.

### Identity
- **Name:** [FILL IN]
- **Contact (canonical, use on every resume and cover letter, in this order):** [City, State] | [university email] | [phone] | [linkedin URL] | [github URL]
- **Location:** [Home city] and [University city/campus] (term-time); [relocation flexibility notes]
- **Languages:** [list languages and proficiency]
- **Status:** [University name] undergraduate, actively seeking [target terms, e.g., Summer 2027 internships] in [target fields]
- **Class standing:** [e.g., rising sophomore, junior, etc.]
- **LinkedIn headline:** [FILL IN]

### Education
- **[Degree]** ([Start] – [Expected End]) — [University], [School/College]
  - GPA: [X.X/4.0]
  - Relevant coursework: [list courses relevant to your target roles]
  - Note on declared major vs. CV framing: [if applicable, note any difference and how to frame it]
- **High School Diploma** ([years]) — [School], [City, State]

### Professional Experience
*List your roles in reverse chronological order. For each, include: title, organization, dates, and 2-5 bullet points describing what you did and what impact it had. Be specific: name the tools, quantify the outcomes.*

- **[Title]** ([Dates]) — **[Organization]** ([Location/Remote])
  - [Bullet 1]
  - [Bullet 2]

*(Add more roles as needed)*

### Technical Skills
- **Primary:** [languages, frameworks, tools you use most]
- **Secondary:** [tools you know but use less often]
- **Domain:** [subject areas you have worked in: legal AI, climate, healthcare, etc.]
- **Software:** [productivity tools, IDEs, platforms]

### Certifications
- [List any relevant certifications]

### Publications
- [List any publications or technical talks]

### Awards
- [List awards and honors relevant to your applications]

### Behavioral Profile
*Fill this in after running setup, or describe yourself:*
- **Working style:** [e.g., builder-operator, researcher, generalist, etc.]
- **Strengths:** [specific, evidence-backed strengths]
- **Growth areas:** [honest areas to improve, framed constructively]
- **Thrives in:** [types of environments, teams, and roles where you do your best work]

### What Excites You
- [List the domains, problems, and types of work that genuinely interest you]

### Target Sectors
- [List companies, industries, or types of roles you are targeting]

### Deal-breakers
- [List hard constraints: equity-only, relocation during school year, etc.]

---

## Repo Structure
- **Master bullet bank (content source of truth):** `documents/cv/MASTER-BULLET-BANK.docx`. Holds every role with 2-4 bullet options each, plus the skills bank, honors, and publications. Pull from this when tailoring. Keep it updated as you add roles or wins.
- **Tailored resumes (deliverables):** saved to `cv/` as `[Your Name] - <Company>.docx`, one file per company. Each is a one-page resume in your house style.
- `documents/cv/` — Source resume material: master bullet bank and any legacy resume files kept for reference.
- `cv/` and `cover_letters/` — Tailored .docx deliverables, one per company.
- **Opportunities (discovery output):** `opportunities/` holds the daily digests (`digest-YYYY-MM-DD.md`) and the running memory (`opportunities-state.md`). This is the front of the funnel: the daily tracker writes here, you pick what to pursue, and the apply pipeline takes over from there.
- `.claude/skills/` — Skill definitions for the application workflow. Includes `daily-opportunities-tracker/` (the single daily discovery source), `job-application-assistant/` (fit eval + tailoring + cover letters), `warm-outreach/`, and `setup/`.
- `documents/private/` — Git-ignored private data: `application-profile.md` (your standard form answers) and `approved-bullets.md` (the learning-loop store).

---

## House Style Spec (match exactly on every resume and cover letter)
Tailored documents must look identical to your existing resumes. Generate .docx with the `docx` skill (docx-js via a Node script). Exact spec:
- **Font:** Times New Roman throughout.
- **Sizes:** name 20pt; section headers 12pt; body, bullets, and role lines 11pt. Same body size everywhere.
- **Section headers:** ALL CAPS, 12pt, not bold, with a thin black bottom rule (border bottom, single, size 4 eighths-pt, space 1).
- **Header (centered):** name 20pt not bold, **centered**. Contact line directly under it, 11pt, also **centered**, separated by `  //  ` (LinkedIn and GitHub as links). Both lines use `jc=center`. **The contact line must lead with city and read exactly: `[City, State]  //  [email]  //  [phone]  //  [linkedin URL]  //  [github URL]`. Never drop the city; it leads the line on every resume and cover letter.**
- **Education layout (exact):** line 1 = university (**bold; the location stays regular weight, not bold**) with location right-aligned via tab. Line 2 = degree with the expected graduation date right-aligned via tab on the **same line**. Line 3 = `GPA: X.X/X.X` italic on its own line. **Relevant-coursework line:** omit by default; include a short, role-relevant line only when it is really necessary. When included, it is plain black body text, never gray. Grad date is "Expected June YYYY" normally, or MM/YY when the posting asks for MM/YY.
- **Section order:** Education, then **Skills (placed near the top, right after Education)** per NCA technical-role guidance, then the experience sections (Project Experience / Research / Work Experience as relevant, reverse-chronological by end date), then Leadership. Skills is technical/language only.
- **Skills section:** **bold the category label** (e.g., **Analytical:**, **Technical:**, **Languages:**) followed by a terse, comma-separated keyword list. No full phrases or sentences in the skills section; keywords and proficiencies only. **Omit the spoken-languages line by default**; include it only when a role specifically invites it.
- **Role lines:** bold title, then ` | `, then italic subtitle/position, then a right-aligned tab to the date. Right tab stop at 10440 twips.
- **Bullets:** real bulleted list, indent left 720 / hanging 360. **Every experience must have 2-5 bullets, never 1. This applies to EVERY section including Leadership; no entry anywhere in the document may have a single bullet.** Bullets are fragments with **no trailing period**; apply this consistently across the whole document.
- **Honors/awards:** fold into the relevant experience bullets (saves space); do **not** create a standalone Honors section.
- **Spacing:** tight and single-spaced (paragraph spacing after 0, line 240 auto). No extra paragraph spacing.
- **Margins:** 0.6in left/right, 0.45in top/bottom. US Letter.
- **No color** (except standard hyperlink blue), no tables, no text boxes, no multi-column layout (ATS-safe), no template look.
- A working generator that produces this exact style is saved at `cv/build_master.js`. Reuse its helpers (`heading`, `roleLine`, `bullet`, `subLabel`) as the pattern for tailored resumes. Run with `node` after `npm install docx` in the working directory.

---

## Resume Tailoring Workflow
1. **User provides a job posting** (URL or text).
2. **Evaluate fit first.** Skills match, experience match, behavioral/culture match. Present this to the user before building anything.
   - **If fit is weak:** give a short "ideal candidate" profile drawn from the posting, mark what you already cover, and suggest concrete, honest additions. Never invent experience.
3. **Pick the base.** Start from the master bullet bank (or the closest existing tailored file). Keep the structure and house style identical.
4. **Tailor by selection, not invention:**
   - Swap whole roles in or out so the most relevant experience leads.
   - Select 2-5 bullets per role from the bank's options; reword lightly to work in the posting's keywords for ATS, keeping every claim true.
   - Reorder the Skills line to lead with the role's required stack.
   - Cut the least-relevant roles so the final file is exactly one page.
5. **Save as its own file:** `cv/[Your Name] - <Company>.docx`.
6. **Verify** (see Verification Checklist): build to PDF and visually inspect.
7. **Offer** a matching cover letter and interview talking points.

**Important:** When mentioning agentic coding or AI tooling, name the specific agent that actually fits the project and employer. Do not name a competitor's tool on an application to that competitor.

---

## Daily Discovery to Apply (the funnel)

The `daily-opportunities-tracker` skill runs automatically at 7am (scheduled task), sweeping broadly across internships, fellowships, research, events, founder/builder programs, VC scouts, hackathons, scholarships, and competitions. It writes the day's digest to `opportunities/digest-YYYY-MM-DD.md` and keeps `opportunities/opportunities-state.md` as memory so it never re-surfaces dead programs. It can also be invoked on demand any time you want to look for opportunities.

The flow is: **(1) discover** — the tracker drops a digest in `opportunities/`; **(2) shortlist** — you mark the items you want to pursue; **(3) apply** — each picked item runs through the Application Pipeline below.

---

## Application Pipeline
This is the repeatable end-to-end motion for applying to a job. When you supply a posting, default to running the whole pipeline unless you ask for a single step. Tailoring intensity defaults to **Aggressive** (defined below).

### Tailoring intensity levels
- **Off:** use the existing resume as-is, no changes.
- **Honest:** reorder and re-emphasize existing experience for the job; do not rewrite bullet content.
- **Aggressive (default):** rewrite and re-scope bullets to match the job description, fold in ATS keywords from the posting, and surface real responsibilities that the written bullets undersell. Reorder sections, skills, and bullets freely.

**Anti-fabrication guardrail (non-negotiable):** Aggressive means rewriting true things more sharply, not inventing experience. Every claim must be something you can defend in an interview. When a bullet asserts something genuinely new (a tool, a metric, or a responsibility not yet anywhere in the master bank or the approved-bullets ledger), label it clearly as a **NEW CLAIM** so you can confirm it is true before it ships. Your approval is the signal that the claim is true and reusable.

### The pipeline (run in order)
1. **Intake.** Supply a job link or pasted text. For a link, open it with the browser when WebFetch is not enough (JS-rendered portals, logged-in boards).
2. **Research.** Read the full posting. Research the company (site, recent news, products, tech stack) and verify any company-specific claim before it goes in a document. Extract the required skills, keywords, and priorities for ATS.
3. **Fit check.** Score against the profile using `04-job-evaluation.md`. Present a short verdict. If fit is weak, give an honest gap read before building anything.
4. **Tailor (Aggressive).** Build a one-page `.docx` resume in your House Style by selecting and aggressively rewriting bullets from the master bullet bank AND the approved-bullets ledger. Reorder sections, skills, and bullets to lead with what the job wants. Save to `cv/[Your Name] - <Company>.docx`.
   - **Cover letter only if needed (do NOT generate by default).** First check whether the application actually takes a cover letter. Generate one only when (a) there is a place to submit it, (b) the posting asks for one, or (c) you request it. When a cover letter IS warranted, write it in your voice per `03-writing-style.md`, run the `humanizer` skill on it, and save to `cover_letters/`.
5. **Verify.** Run the full Verification Checklist below, including the mandatory compiled-PDF one-page check, before showing anything.
6. **Review gate.** Present the resume (and the cover letter only if one was warranted). Clearly list every **NEW CLAIM** introduced in this pass. Wait for approval or edits.
7. **Auto-apply.** Once you approve, submit the application through the browser automatically. **Fill EVERY field the profile can answer, optional fields included.** Upload the approved resume (PDF). Do not invent answers to legally meaningful fields (work authorization, veteran or disability status, demographics); if a required field has no stored answer, stop and ask. Never store or auto-fill passwords. Log the application to `job_search_tracker.csv`.
   - **Browser:** connect your browser via Claude in Chrome before starting. Use `list_connected_browsers` and `select_browser` with the deviceId of your browser.
   - **Workday gotchas (myworkdayjobs.com):**
     - Picklist/typeahead fields (State, School, Degree, Field of Study): type the value then click the matching item. Degree list has no "Bachelor of Science" — use **"Bachelors"**.
     - Skills field is free-text: type ONE skill, press Enter, wait for it to become a chip, THEN type the next. Do NOT batch type+Enter rapidly. Never press cmd+a inside the Skills box.
     - Progress-bar steps are not clickable; use the **Back** button to go back (data retained).
8. **Learn.** Append every NEW CLAIM that you approved to `documents/private/approved-bullets.md` with the role, date, and company.
9. **Outreach (optional).** Offer warm outreach for the company via the `warm-outreach` skill (alumni first, then recruiters, then the hiring team).

### Learning Loop (the memory)
When you approve a resume or cover letter that contained a NEW CLAIM, append it to `documents/private/approved-bullets.md`. The Tailor step reads this alongside the master bank so an approved phrasing is reusable on the next application. Periodically fold the ledger into the master bullet bank .docx.

### Persistent application data
- **Application Profile:** `documents/private/application-profile.md` (git-ignored). Holds the standard form answers: contact, work authorization, EEO/veteran/disability/demographics (voluntary), salary/relocation/start-date answers, links, and job-board account usernames. No passwords. Read this during auto-apply, and whenever you provide a new detail, save it here so it is never asked twice.
- **Approved-bullets ledger:** `documents/private/approved-bullets.md` (git-ignored). The learning-loop store described above.

---

## Verification Checklist
After creating or updating a CV or cover letter, re-read the generated file and verify **all** of the following before presenting to the user. Report the results as a pass/fail checklist.

**Authoritative source:** your university career center guide (store it at `documents/career-guide.pdf` if available). The NCA Career Guide format is a widely-used standard; any comparable guide works. Pages 5-16 cover résumés; pages 22-25 cover cover letters.

### Factual accuracy
- [ ] All claims match actual profile — no fabricated skills, experience, or achievements
- [ ] Job titles, dates, company names, and locations are correct
- [ ] Contact details are correct
- [ ] Header contact line leads with city and matches the canonical order exactly
- [ ] All company-specific claims have been independently verified via WebFetch/WebSearch

### Targeting
- [ ] Skills section is reordered to lead with the role's required stack
- [ ] Experience bullets are reframed to match the job requirements
- [ ] Key job requirements are addressed (with gaps acknowledged where relevant)

### NCA résumé format rules
- [ ] **1 page** for undergrad
- [ ] **Font:** one of NCA-approved fonts (Arial, Calibri, Cambria, Garamond, Helvetica, Palatino Linotype, Times New Roman). Same font size throughout body.
- [ ] **Font size:** 10-12pt body; 14-24pt name
- [ ] **Margins:** 0.5-1.0 inch (house style is 0.6in left/right, 0.45in top/bottom)
- [ ] **Alignment:** body Left-aligned (NOT justified); header (name + contact) centered
- [ ] **Bullets:** every experience has 2-5 bullets, never just 1; bullets are fragments with no trailing period
- [ ] **Order:** Reverse chronological by **end date** (most recent first within each section)
- [ ] **Numerals:** Use 6 not "six", 30% not "thirty percent"
- [ ] **No personal pronouns**: no "I", "my", "our". Bullets start with action verbs
- [ ] **No full sentences** in bullets, fragment form is the norm
- [ ] **ATS-safe**, no tables, text boxes, multi-column layout, or info in headers/footers

### NCA section structure for technical roles
- [ ] **Skills section** placed near the top, **after Education and before Experience**
- [ ] **Skills section contains technical/language skills ONLY**
- [ ] **Honors/awards folded into experience bullets**, no standalone Honors section
- [ ] **Header centered**; education uses university (bold) + location (regular) on one line, degree+grad date on one line, GPA on its own line
- [ ] **GitHub / portfolio link** in the header
- [ ] **Bullet formula:** ACTION VERB + TASK + PURPOSE/RESULT

### NCA cover letter format rules
- [ ] **Same header as CV** for cohesive brand
- [ ] **3-5 paragraphs**, business letter format, 1 page
- [ ] **Salutation:** named recruiter if known, else "Recruiting Team" or "Hiring Manager"
- [ ] **Opening paragraph:** introduce self, state why writing, how learned about position, 2-3 sentences on interest in org
- [ ] **Middle paragraphs:** 2-3 experiences (not all résumé bullets), with specific examples of skills the employer is seeking
- [ ] **Closing paragraph:** thank for consideration, request to discuss
- [ ] **No contact info in signature** (it's already in the header)

### Quality
- [ ] Document validates (run `validate.py` from the docx skill)
- [ ] No spelling or grammar errors
- [ ] No em-dashes (use commas, periods, or restructure)
- [ ] AI tooling references name the specific agent that fits the project and employer
- [ ] House Style Spec matched exactly

### Compiled PDF verification (MANDATORY — never skip)
The .docx MUST be converted to PDF and visually inspected. Convert with the docx skill (`soffice.py --convert-to pdf`, then `pdftoppm`). Iterate until these all pass:
- [ ] **Resume is exactly 1 page**
- [ ] **Cover letter is exactly 1 page**
- [ ] **No orphaned section headings**
- [ ] **No "I"/"my"/"our" in resume bullets** (programmatically check before declaring done)
