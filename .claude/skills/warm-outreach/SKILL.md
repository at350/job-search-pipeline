---
name: warm-outreach
description: For a company where you have an open application, an offer, or a target role, this skill finds who to reach out to (university alumni first, then recruiters, then the hiring team), drafts a personalized LinkedIn connection note for each, shows you the list for approval, and then, only after you approve, sends the connection requests via Chrome. Use it whenever you want to network into a company, get a referral, "reach out to people at [company]", "connect with someone at [company]", "find a warm intro", "who should I message at [company]?", or follow up on a role you already applied to.
---

## What this skill is for

Referrals and warm intros come from people, not portals. When you already have a foothold at a company — applied, interviewing, offer in hand, or just decided it's a target — this skill finds the right people to talk to and gets the outreach out the door. It does the research and drafting, then sends after a single approval checkpoint.

Two ground rules:
- **Find people only through LinkedIn (via Claude in Chrome) or public web search.** No sales tools or CRMs.
- **Sending requires your explicit go.** You draft and stage everything, show it to you, and send connection requests only after you say yes in that run. Connection requests can't be unsent, and a clumsy note to a recruiter or alum reflects on you personally. The approval step is non-negotiable.

## Inputs

Name the **company** (and ideally the **role/term**, e.g. "Salesforce, Summer 2027 SWE intern"). If the role isn't clear:
- Check `job_search_tracker.csv` and the most recent `opportunities/digest-*.md` for companies you've applied to or shortlisted, and ask which one you mean.
- If still unclear, ask directly, don't guess.

## Working folder and context

The repo root is the `job-search-pipeline` folder. Read first:
- `CLAUDE.md`: candidate profile (so messages are specific and accurate).
- `.claude/skills/job-application-assistant/03-writing-style.md`: the voice for the notes (no em-dashes, no clichés, warm and specific).
- `outreach_tracker.csv`: people already contacted (columns: `date,company,role,contact_name,contact_title,university_alum,linkedin_url,status,notes`). Never double-contact someone already in here for the same company.

## Step 1, Confirm the target and connect to Chrome

Confirm the company/role. Then connect to the user's logged-in Chrome (list connected browsers; if more than one, ask which has LinkedIn logged in). If Chrome isn't connected or LinkedIn isn't logged in, stop and tell the user — this skill needs their session.

## Step 2, Find who to reach out to

Find **2-4 people** at the company using LinkedIn (read public profiles only; do not connect or message yet). Priority order, warmest first:
1. **University alumni** at the company — use LinkedIn's school alumni filter, or the "School alumni from [university name]" panel on the company's people pages. A shared-school intro is the strongest angle.
2. **Recruiters / university recruiting / talent** for the relevant org or role.
3. **The hiring manager or a team member** on the function you applied to.

For each person capture: name, title, whether they're a university alum, and their LinkedIn profile URL. Skip anyone already in `outreach_tracker.csv` for this company. Favor people who are 2nd-degree connections — they're likelier to accept.

## Step 3, Draft a connection note for each

Follow `03-writing-style.md`. Per good networking practice, a good outreach message covers: who you are (brief intro), how you found them, what you have in common, why you're reaching out, and one light specific ask. Treat it as connecting and learning, not asking for a job — don't ask for a referral in a first message; it follows naturally once they know you.

For each person write a **connection-request note under 300 characters** (LinkedIn's limit) that:
- Is specific to the person and the role/company (not a template).
- Names the tie if they're a university alum or shares a concrete reason for reaching out.
- States the ask lightly: that you applied / are interested in [role], and would value their perspective.
- Sounds like a sharp undergrad wrote it — warm and brief.

Optionally draft a short follow-up message to send if they accept, but the connection note is the thing that gets sent.

## Step 4, Show the list and get approval (required checkpoint)

Present a compact table: Name · Title · Alum? · why this person · the exact connection note. Ask the user to approve, edit, or drop individual entries. **Do not proceed to send until they give a clear go.** If they edit notes, use their versions.

## Step 5, Send the approved connection requests

Only for the people the user approved, and only after their go: in Chrome, for each profile, open it, click **Connect**, choose **Add a note**, paste the approved note, and **Send**. Go one at a time. If a profile only offers "Follow" or routes through "More", handle it gracefully or skip and report back.

## Step 6, Log and wrap up

- Append each person to `outreach_tracker.csv` with `status` = `sent` (or `skipped`/`failed` with a note).
- Give a one-line summary: e.g. "Sent 3 connection requests at Salesforce (2 university alumni, 1 recruiter); 1 skipped (no Connect button), logged in outreach_tracker.csv."
