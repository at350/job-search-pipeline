---
name: job-application-assistant
description: Runs the end-to-end application pipeline — research a posting, aggressively tailor a one-page .docx resume and a human-voiced cover letter, verify formatting, auto-apply through the browser after approval, and feed approved new bullets back into the bullet bank. Triggers on keywords like: job posting, job application, CV, cover letter, resume, tailor, apply, auto-apply, interview prep, job fit, career.
allowed-tools: Read, Glob, Grep, WebFetch, WebSearch, Edit, Write, AskUserQuestion
---

## Authoritative spec

The full pipeline lives in the repo's `CLAUDE.md` under **Application Pipeline** (intensity levels, the 9-step motion, the anti-fabrication guardrail, the Learning Loop, and the persistent-data files). That section is the source of truth. This file is the quick operational summary; if the two ever disagree, CLAUDE.md wins.

**Default intensity is Aggressive:** rewrite and re-scope bullets to match the posting and fold in ATS keywords, but only ever sharpen true things the user can defend. Anything genuinely new gets flagged as a **NEW CLAIM** at the review gate and, once approved, is saved to the approved-bullets ledger.

## Workflow (run the whole thing unless the user asks for one step)

1. **Intake.** Take the link or pasted text. Open links in the browser (Claude in Chrome) when WebFetch is not enough (JS portals, logged-in boards).
2. **Research.** Read the full posting, research the company, verify any company-specific claim, and extract required skills + ATS keywords.
3. **Fit check.** Score with `04-job-evaluation.md`; present a short verdict and an honest gap read if fit is weak.
4. **Tailor (Aggressive).** Build a one-page `.docx` resume in the user's House Style (see CLAUDE.md House Style Spec) using the **docx** skill, pulling and rewriting bullets from `documents/cv/MASTER-BULLET-BANK.docx` AND `documents/private/approved-bullets.md`. Reorder sections/skills/bullets to lead with what the job wants. Write the cover letter in the user's voice per `03-writing-style.md`, then run the **humanizer** skill on it. Save to `cv/[Name] - <Company>.docx` and `cover_letters/`.
5. **Verify.** Run the full Verification Checklist in CLAUDE.md, including the mandatory compiled-PDF one-page check, before showing anything.
6. **Review gate.** Present both documents and list every NEW CLAIM. Wait for approval or edits.
7. **Auto-apply.** On approval, submit through the browser automatically (full auto-submit). Fill fields from `documents/private/application-profile.md`; upload the approved files. Do not guess legally meaningful fields (work authorization, veteran/disability, demographics) or anything the profile lacks; stop and ask instead. Never store or auto-fill passwords. Log the application to `job_search_tracker.csv`.
8. **Learn.** Append approved NEW CLAIMs to `documents/private/approved-bullets.md`.
9. **Outreach (optional).** Offer the **warm-outreach** skill for the company.

---

## Reference Files

| File | Purpose |
|------|---------|
| `01-candidate-profile.md` | Education, experience, skills, publications, awards |
| `02-behavioral-profile.md` | Behavioral assessment, strengths, ideal environments |
| `03-writing-style.md` | Tone, structure, do's and don'ts (no em-dashes, human voice) |
| `04-job-evaluation.md` | Scoring framework for job fit |
| `05-cv-templates.md` | CV structure and tailoring rules (house style reference) |
| `06-cover-letter-templates.md` | Cover letter structure and tailoring rules |
| `07-interview-prep.md` | STAR format, tough questions, roleplay guidelines |

---

## Quick Commands

The user may also ask for individual steps:
- "Evaluate this job posting" — Step 1-3 only
- "Tailor a resume for [company]" — Step 4 (resume) only
- "Write a cover letter for [role] at [company]" — Step 4 (cover letter) only
- "Apply to this for me" — assumes an approved resume + cover letter, runs Step 7
- "Help me prepare for an interview at [company]" — use `07-interview-prep.md`
