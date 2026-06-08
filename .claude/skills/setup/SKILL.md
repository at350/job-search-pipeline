---
name: setup
description: First-time setup for the job-search-pipeline. Walks new users through filling in their candidate profile, creating private application data files, scheduling the daily opportunities tracker, and connecting tools. Run this once when you clone the repo, then again whenever you want to update your profile. Triggers on: "run setup", "set up the pipeline", "configure the pipeline", "fill in my profile", "first time setup", "onboard".
---

You are running first-time setup (or a profile refresh) for the job-search-pipeline workspace.

Your job is to collect the information needed to make every other skill in this repo work correctly. Work through the sections below in order. Ask the user for each piece of information they haven't already provided, then write it into the right files. Be conversational — ask a few related questions at a time, not one by one.

---

## What you will build

By the end of setup, the following files will be populated or created:

1. **`CLAUDE.md` — Candidate Profile section** filled in with the user's identity, education, experience, skills, and targets.
2. **`documents/private/application-profile.md`** — Standard form answers (contact info, work authorization, salary preferences, job-board usernames). Git-ignored.
3. **`documents/private/approved-bullets.md`** — Empty ledger to track approved new claims. Git-ignored. (Create the file; do not add content yet.)
4. **`documents/cv/MASTER-BULLET-BANK.docx`** — Remind the user to create or migrate this. Provide instructions if they are starting fresh.
5. **Scheduled task** — Offer to schedule the `daily-opportunities-tracker` to run at 7am every day.
6. **Tool connections** — Check which tools are connected (Gmail, Slack, calendar, browser) and note which ones enhance which skills.

---

## Step 1: Collect the candidate profile

Ask the user for the following, in friendly batches (not one question at a time):

**Batch 1 — Identity and education:**
- Full name
- Contact info: city/state, university email, phone, LinkedIn URL, GitHub URL
- University name, school/college, degree(s), expected graduation year
- GPA (if they want to include it; anything ≥ 3.5 is worth listing)
- Current class standing (freshman, sophomore, junior, senior; or "rising X" if just finished a year)
- Any second major, minor, or relevant specialization track

**Batch 2 — Experience:**
- Their roles in reverse chronological order: title, org, dates, 3-5 bullet points describing what they did and the outcome. Tell them: "Be specific — name the tools, quantify the impact (e.g., 90% reduction, 15% lift, managed $20k budget). These bullets become the raw material for every tailored resume."
- Any independent research, publications, or significant projects
- Any hackathon wins or competitions

**Batch 3 — Skills and awards:**
- Programming languages and frameworks (primary = daily use; secondary = know well but use less)
- Domain knowledge areas they have worked in (legal AI, climate tech, healthcare, etc.)
- Notable awards, scholarships, or honors worth putting on a resume

**Batch 4 — Goals and preferences:**
- What terms they are targeting (e.g., Summer 2027 internship, Winter 2027)
- Target sectors and specific companies they are most excited about
- Deal-breakers (e.g., no relocation during school year, no equity-only roles)
- What types of work excite them vs. drain them

---

## Step 2: Write the candidate profile

Read the current `CLAUDE.md`. Replace every `[FILL IN]` placeholder in the **Candidate Profile** section with the information the user provided. Write the updated file back to `CLAUDE.md`.

Also update `.claude/skills/job-application-assistant/01-candidate-profile.md` with the same information, formatted for the job evaluation framework.

Also update `.claude/skills/job-application-assistant/02-behavioral-profile.md` with an inferred behavioral profile based on what the user described (working style, strengths, growth areas, ideal environment). Label each inference clearly as inferred, and invite the user to correct anything that doesn't fit.

Also update `.claude/skills/job-application-assistant/04-job-evaluation.md` — fill in the **Strong match areas**, **Moderate match areas**, and **Career goals** sections based on the user's profile.

---

## Step 3: Create application-profile.md

Create `documents/private/application-profile.md` (create the `documents/private/` directory if it doesn't exist). This file is git-ignored.

Populate it with:

```markdown
# Application Profile

## Contact
- Name: [from setup]
- Email: [from setup]
- Phone: [from setup]
- LinkedIn: [from setup]
- GitHub: [from setup]
- Address / City: [from setup]

## Work Authorization
- Legally authorized to work in the US: [Yes / No]
- Requires visa sponsorship: [Yes / No]
- Citizenship / status: [optional, fill if needed for government roles]

## Standard Screening Answers
These default answers apply to most employers. Update for any employer where the answer differs.
- Have you previously applied here: No
- Have you worked here before: No
- Do you have relatives employed here: No
- Commitments to another employer that conflict: No

## Salary / Relocation
- Target compensation: [e.g., "paid internship, amount flexible"]
- Relocation: [e.g., "open to relocation Summer only (mid-June to mid-September); not available to relocate during academic year Sept–June"]
- Availability: [start date, summer window, academic-year constraints]

## Diversity / EEO (voluntary, fill only what you are comfortable sharing)
- Gender: [optional]
- Race / ethnicity: [optional]
- Veteran status: Not a veteran
- Disability status: No disability

## Job-Board Accounts
- Workday: [username / email used]
- LinkedIn: [profile URL]
- Handshake: [university account]
- Others: [list any others]

## Browser for Auto-Apply
- Browser device ID: [run list_connected_browsers in Claude in Chrome and paste the deviceId here]
```

Ask the user to confirm or fill in any fields they skipped (especially work authorization and browser deviceId).

---

## Step 4: Create the approved-bullets ledger

Create `documents/private/approved-bullets.md` with just a header:

```markdown
# Approved Bullets Ledger

This file stores new claims approved by the user during the resume tailoring process.
Each entry records the claim, the role it belongs to, the date approved, and the company it was first approved for.
The job-application-assistant reads this alongside the master bullet bank to reuse approved phrasings.

---
```

---

## Step 5: Master bullet bank

Ask the user whether they:
(a) Already have a resume they want to use as the starting bullet bank, or
(b) Want to start fresh and enter their bullets during setup.

**If (a):** Ask them to drop their existing resume (PDF or .docx) into the `documents/cv/` folder as `MASTER-BULLET-BANK-SOURCE.[ext]`, and tell them you will extract bullets from it when they run their first tailoring job.

**If (b):** Walk them through creating `documents/cv/MASTER-BULLET-BANK.docx` using the `docx` skill. Use the bullets they provided in Step 1 (Batch 2) as the content. Build one role block per entry, with 2-4 bullet variants where possible. Save the file.

---

## Step 6: Schedule the daily tracker

Offer to schedule the `daily-opportunities-tracker` skill to run automatically at 7am every day. Tell the user: "This gives you a fresh digest of internships, fellowships, hackathons, founder programs, and other opportunities every morning. You can also trigger it manually any time."

If they agree, use the `schedule` skill (or the `mcp__scheduled-tasks__create_scheduled_task` tool) to create a daily 7am task that runs the `daily-opportunities-tracker` skill.

---

## Step 7: Tool connections check

Check which MCP connectors are connected:

- **Gmail / Google Workspace:** enhances the daily tracker (LinkedIn job alert emails). Note the email address the connector is authenticated to.
- **Chrome / Claude in Chrome:** required for auto-apply, Handshake scan, warm outreach, LinkedIn post staging. Ask the user to connect it and confirm which browser they use.
- **Slack:** optional, useful for sharing digests or logging status.
- **Notion / Google Drive:** optional, useful for linking documents.

For any that are missing, tell the user what functionality they would unlock and how to connect them (Settings → Connectors in Claude desktop).

---

## Step 8: Confirm and wrap up

Show the user a summary of what was set up:
- Candidate profile: [populated / partially filled — list any gaps]
- Application profile: [created]
- Approved-bullets ledger: [created]
- Master bullet bank: [created / pending migration]
- Daily tracker: [scheduled at 7am / not scheduled]
- Tools connected: [list]
- Tools missing: [list with what they unlock]

Tell them what to do next: "Run the daily-opportunities-tracker to see today's opportunities, or paste a job posting and I'll run the full application pipeline."
