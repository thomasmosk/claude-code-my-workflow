# Workflow Quick Reference

**Model:** Contractor (you direct, Claude orchestrates)

---

## The Loop

```
Your instruction
    ↓
[PLAN] (if multi-file or unclear) → Show plan → Your approval
    ↓
[EXECUTE] Implement, verify, done
    ↓
[REPORT] Summary + what's ready
    ↓
Repeat
```

---

## I Ask You When

- **Design forks:** "Option A (fast) vs. Option B (robust). Which?"
- **Content ambiguity:** "Source slide unclear on X. Assume Y?"
- **Layout choices:** "Dense content — split into 2 slides or use smaller font?"
- **Scope question:** "Also convert appendix slides, or main deck only?"

---

## I Just Execute When

- Code fix is obvious (bug, pattern application)
- Verification (compilation checks, image validation)
- Documentation (logs, commits)
- Extraction (images, text from PPT/PDF)

---

## Quality Gates (No Exceptions)

| Score | Action |
|-------|--------|
| >= 80 | Ready to commit |
| < 80  | Fix blocking issues |

---

## Non-Negotiables

- **XeLaTeX only** — never pdflatex or lualatex
- **Output structure** — `output/[lecture_name]/` with `images/` subdirectory
- **Image quality** — minimum 150 DPI, PNG for raster images, preserve aspect ratio
- **Preamble** — always `\input{../../Preambles/header}` (or appropriate relative path)
- **Image paths** — always `\graphicspath{{images/}}`

---

## Preferences

**Image handling:** Extract at source resolution, scale in LaTeX
**Reporting:** Concise bullets, details on request
**Session logs:** Always (post-plan, incremental, end-of-session)

---

## Exploration Mode

For experimental work, use the **Fast-Track** workflow:
- Work in `explorations/` folder
- 60/100 quality threshold (vs. 80/100 for production)
- No plan needed — just a research value check (2 min)
- See `.claude/rules/exploration-fast-track.md`

---

## Next Step

You provide task → I plan (if needed) → Your approval → Execute → Done.
