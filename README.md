# Job Search Pipeline

An AI-powered job search workspace for ambitious undergrads. Built on top of [Claude](https://claude.ai) (Anthropic's AI assistant), it automates the full funnel from daily opportunity discovery through tailored resume generation, cover letter writing, and auto-apply — while keeping you in control at every step.

---

## What this does

**Discover.** A daily automated digest surfaces internships, fellowships, hackathons, founder programs, VC events, research opportunities, scholarships, and competitions — drawn from hundreds of named programs and live ATS/aggregator sources. Runs every morning at 7am and writes to `opportunities/`.

**Tailor.** For any job posting, Claude researches the company, scores fit against your profile, builds a one-page .docx resume (selecting and aggressively rewriting bullets from your master bullet bank), and runs a full verification checklist before showing you anything.

**Apply.** Once you approve the resume, Claude auto-fills and submits the application through the browser — Workday, Greenhouse, Lever, and most other portals — logging each application to a tracker CSV.

**Outreach.** The warm-outreach skill finds university alumni and recruiters at target companies on LinkedIn and stages personalized connection notes for your approval before sending.

**Learn.** Any new claim you approve gets saved to a private ledger so it's reusable on future applications without re-approval.

---

## Requirements

- **[Claude desktop app](https://claude.ai/download)** — this repo is designed to run in Cowork mode (Claude's desktop agent mode).
- **[Claude in Chrome extension](https://chromewebstore.google.com/detail/claude-in-chrome/...)** — needed for auto-apply, LinkedIn outreach, and Handshake scanning.
- **Node.js** — for the .docx build scripts (`npm install docx` in `cv/`).
- **LibreOffice** (optional) — used by the docx skill to convert .docx to PDF for verification.

### Recommended plugins / skills
Install these from Claude's plugin marketplace or via the plugin manager:
- **docx** — generates Word documents in the house style
- **humanizer** — removes AI-writing patterns from cover letters
- **pptx** — if you want to create pitch decks or presentation materials
- **schedule** — to set up the 7am daily digest automation
- **handshake-scan** — scans your university's Handshake portal (requires logged-in browser)

---

## Getting started

1. **Clone this repo** into a folder on your computer.
2. **Open Claude desktop** and open the `job-search-pipeline` folder as your workspace (File → Open Folder, or via Cowork mode).
3. **Run setup:** type `run setup` in Claude. It will walk you through:
   - Filling in your candidate profile (education, experience, skills, awards, targets)
   - Creating your private application-profile file
   - Scheduling the daily opportunities tracker
   - Connecting your tools (Gmail, Chrome, calendar)
4. **Build your master bullet bank:** follow the setup prompts, or paste your existing resume and Claude will extract the bullets.
5. **Run the daily tracker:** type `run the daily opportunities tracker` to get today's digest. Paste a job posting to run the full application pipeline.

---

## Repo structure

```
job-search-pipeline/
├── CLAUDE.md                          # Workspace instructions and your candidate profile
├── README.md                          # This file
├── .gitignore
├── job_search_tracker.csv             # Log of every application submitted
├── outreach_tracker.csv               # Log of every outreach message sent
│
├── opportunities/                     # Daily digest output
│   └── opportunities-state.md         # Running memory (prevents re-surfacing dead programs)
│
├── cv/                                # Tailored resumes (one .docx per company)
│   └── build_master.js                # .docx generator (created during setup)
│
├── cover_letters/                     # Cover letters (one .docx per company)
│
├── documents/
│   ├── cv/
│   │   ├── MASTER-BULLET-BANK.docx   # Your bullet bank (created during setup)
│   │   └── MASTER-BULLET-BANK-TEMPLATE.md  # Template to guide bullet bank creation
│   └── private/                       # Git-ignored private data
│       ├── application-profile.md     # Standard form answers for auto-apply
│       └── approved-bullets.md        # Learning loop ledger
│
└── .claude/
    └── skills/
        ├── setup/                     # First-time onboarding skill
        ├── daily-opportunities-tracker/   # Daily digest skill
        │   └── references/
        │       └── search-plan.md     # Exact URLs and query templates for the sweep
        ├── job-application-assistant/ # Fit eval + tailoring + cover letters + auto-apply
        └── warm-outreach/             # LinkedIn outreach automation
```

---

## The pipeline in full

### 0. Discover
The `daily-opportunities-tracker` runs at 7am and writes a digest to `opportunities/digest-YYYY-MM-DD.md`. It sweeps hackathons, internships, fellowships, founder programs, VC events, research, conferences, scholarships, and competitions. It reads your profile to filter by your target sectors and deal-breakers.

You can also trigger it any time: just type "run the daily opportunities tracker."

### 0.5. Shortlist
Review the digest and tell Claude which items you want to pursue.

### 1. Intake
Paste a job posting URL or text. Claude opens JS-gated portals in the browser when needed.

### 2. Research
Claude reads the full posting, researches the company, verifies any company-specific claims, and extracts required skills and ATS keywords.

### 3. Fit check
Claude scores the role against your profile across five dimensions (technical skills, experience match, behavioral fit, location, career alignment) and gives you a short verdict. If fit is weak, you get an honest gap read before anything gets built.

### 4. Tailor (Aggressive by default)
Claude builds a one-page .docx resume in your house style, selecting and rewriting bullets from your master bullet bank to match the posting. Cover letter is only written when the application actually has a field for one.

### 5. Verify
Claude runs the full verification checklist — format rules, no personal pronouns, no em-dashes, correct order — and compiles to PDF to confirm it's exactly one page.

### 6. Review gate
You see the resume (and cover letter if applicable), plus a list of any **NEW CLAIMs** introduced. You approve or request edits before anything ships.

### 7. Auto-apply
On your approval, Claude submits the application through the browser, filling every field it can from your application profile. Logs the application to `job_search_tracker.csv`.

### 8. Learn
Any new claim you approved gets saved to `documents/private/approved-bullets.md` for reuse on future applications.

### 9. Outreach (optional)
Claude offers to find and message relevant people at the company via the warm-outreach skill.

---

## Privacy

Files in `documents/private/` are git-ignored. They contain your contact details, standard form answers, and the learning-loop ledger — none of which should be committed to a public repo. Tailored resumes and cover letters are also git-ignored.

The `opportunities/digest-*.md` files are personal and also git-ignored. Only `opportunities/opportunities-state.md` (the running memory, which contains no personal info) is tracked.

---

## Contributing

This pipeline was built for one person and then generalized. If you find ways to improve it — better search strategies, tighter verification rules, new skill variants — pull requests are welcome.

A few things that would improve the pipeline for everyone:
- A `salary_lookup.py` script and `salary_data.json` with compensation benchmarks by company
- A Handshake-scan skill for your specific university's portal URL patterns
- Cover letter templates for specific industries (finance, consulting, research)
- A university-specific section in `CLAUDE.md` with career center resources

---

## License

MIT — use it, fork it, build on it.
