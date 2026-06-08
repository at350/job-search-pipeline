# CV Templates and Tailoring Guide

**Authoritative source:** your university career center guide (store at `documents/career-guide.pdf` if available). When in doubt, defer to the career guide.

## Output format: .docx (via the `docx` skill)

NCA's guidance: "Avoid templates; they are overused and hard to customize, and they often do not upload correctly to employers' application portals." The right CV is a clean, ATS-friendly, plain-serif document. We produce this as a .docx file using the `docx` skill (docx-js via a Node script).

**Output file:** `cv/[Your Name] - <Company>.docx`
**Build script:** `cv/build_master.js` — this is the canonical generator for your house style. Run with `node build_master.js` after `npm install docx` in the `cv/` directory.

## Document Structure (House Style)

The exact spec lives in the **House Style Spec** section of `CLAUDE.md`. The key points:

- **Font:** Times New Roman throughout.
- **Sizes:** name 20pt; section headers 12pt; body/bullets/role lines 11pt.
- **Section headers:** ALL CAPS, 12pt, not bold, with a thin black bottom rule.
- **Header (centered):** name 20pt not bold, centered. Contact line directly under it, 11pt, centered, separated by `  //  `.
- **Role lines:** bold title, ` | `, italic subtitle/position, right-aligned date (right tab at 10440 twips).
- **Bullets:** indent left 720 / hanging 360; fragments with no trailing period; 2-5 per entry.
- **Spacing:** tight and single-spaced; paragraph spacing after 0; line 240 auto.
- **Margins:** 0.6in left/right, 0.45in top/bottom. US Letter.
- **No color** (except hyperlink blue), no tables, no text boxes, no multi-column layout.

## NCA Formatting Rules

| Rule | Value |
|------|-------|
| Length | **1 page** for undergrad |
| Body font size | 10-12pt (same throughout) |
| Name font size | 14-24pt |
| Approved fonts | Arial, Book Antiqua, Calibri, Cambria, Centaur, Century Gothic, Garamond, Helvetica, Palatino Linotype, **Times New Roman** |
| Margins | 0.5-1.0 inch |
| Alignment | Left-aligned, NOT justified |
| Bullets per experience | 2-5 |
| Numbers | Always numerals (6, not "six"; 30%, not "thirty percent") |
| Section order | Reverse chronological by **end date** |
| Phrasing | No full sentences; no personal pronouns (I, my, our) |

## NCA Bullet Formula

```
ACTION VERB + TASK + PURPOSE/RESULT
   (skill)     (what)    (why or impact)
```

Use the NCA action verb list: Analytical (Analyzed, Conducted, Designed, Evaluated, Modeled, Solved, Synthesized), Communication (Authored, Collaborated, Presented), Leadership (Led, Managed, Spearheaded, Streamlined), Quantitative (Allocated, Budgeted, Forecasted, Reduced), Technical (Constructed, Designed, Developed, Engineered, Programmed, Prototyped).

## Section Order

### For technical roles (NCA guidance)
1. Header (name + contact, **with GitHub/portfolio link**)
2. **Education** (school, location, degree, expected grad, GPA, relevant coursework)
3. **Skills** (technical/language only, placed near top per NCA technical-role guidance)
4. **Project Experience** (reverse chrono by end date)
5. **Experience** (work, reverse chrono by end date)
6. **Leadership** (student orgs, reverse chrono by end date)

### For non-technical / general roles
1. Header
2. Education
3. Experience (work + projects mixed, reverse chrono)
4. Leadership
5. Activities / Community Involvement
6. Additional Information / Skills (at bottom)

## Profile Statements / Summary

**NCA does not require a summary statement at the top** for undergrads. The Education + Skills sections do that job. Only experienced candidates use a "Professional Summary." If a specific recruiter pipeline expects a summary, keep it to 2-3 lines max.

## Section-by-Section Tailoring

### Education
- Always list school name + location + degree + anticipated grad date
- GPA, relevant coursework, and honors are optional; include if strong (GPA ≥ 3.5 generally)
- Tailor the coursework list to the role's technical focus

### Skills (technical roles only, placed after Education)
- Technical/language only. **No** "communication," "leadership," "teamwork."
- Suggested sub-categories: Programming, Quantitative & ML, Systems, Languages
- Reorder to lead with the role's required stack

### Project Experience / Experience
- Reverse chronological by **end date**
- 2-5 bullets each; action verb + task + purpose/result
- Quantify wherever possible (90%, 86%, $20k, 65-person, 1,000+)
- Mention specific tools used

### Leadership
- 1-3 bullets per role; same action-verb structure
- Quantify scope (budget size, headcount, awards won)

## Compile-and-Inspect Loop (MANDATORY)

After writing the CV and before presenting to the user:

1. Run the docx skill to build the file and convert to PDF
2. Use `soffice.py --convert-to pdf` then `pdftoppm` to render it
3. Read the rendered PDF via the Read tool and visually inspect
4. Verify:
   - No "I"/"my"/"our" anywhere (programmatic check)
   - Exactly 1 page
   - No section heading orphans
   - Reverse chronological order in every section
   - All bullets start with action verbs
   - No trailing periods on bullets
   - 2-5 bullets per entry (never 1)

### Fixing common page-overflow problems

**Problem: content overflows to page 2**
1. First combine multi-bullet entries into single bullets where appropriate
2. Then drop low-relevance bullets
3. Then tighten Skills section
4. Then drop entire low-relevance sections
5. Last resort: shrink margins (minimum 0.5in)

**Problem: empty space at the bottom of the page**
- Restore the highest-relevance bullet you cut, or expand a key one

## Page Budget, Hard 1-Page Limit

| Section | Max budget |
|---------|-----------|
| Header | 2 lines (name + contact) |
| Education | 1 entry, 3-4 lines |
| Skills | 3-4 lines (bold category labels) |
| Most recent project / role | 3-4 bullets |
| Previous project / role | 1-2 bullets |
| Older role | 1-2 bullets |
| Leadership | 1-2 entries, 1-2 bullets each |

**If in doubt, cut rather than squeeze.** Clean readable spacing beats cramped content.

## Relevance-Weighted Cutting (when overflow happens)

Score each candidate line by:
1. **Relevance to THIS posting** — does it hit a named tool/keyword/responsibility?
2. **Uniqueness** — only place this claim appears?
3. **Narrative load** — does the cover letter lean on it?

Cut lowest-total-score first, regardless of section.
