---
paths:
  - "Slides/**/*.tex"
  - "output/**/*.tex"
  - "scripts/**/*.R"
---

# Quality Gates & Scoring Rubrics

## Thresholds

- **80/100 = Commit** -- good enough to save
- **90/100 = PR** -- ready for deployment
- **95/100 = Excellence** -- aspirational

## Beamer Slides (.tex)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | XeLaTeX compilation failure | -100 |
| Critical | Undefined citation | -15 |
| Critical | Overfull hbox > 10pt | -10 |
| Major | Missing image file | -10 |
| Major | Text overflow / overstuffed slide | -5 |
| Major | Notation inconsistency | -3 |
| Minor | Font size reduction | -1 per slide |
| Minor | Long lines (>100 chars) | -1 (EXCEPT math formulas) |

## Converted Slides (output/**/*.tex)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Compilation failure | -100 |
| Critical | Missing extracted images | -15 |
| Critical | Equations left as images (when convertible) | -10 |
| Major | Tables not recreated in LaTeX | -5 |
| Major | Slide content dropped from source | -5 |
| Major | Wrong image aspect ratio | -3 |
| Minor | Suboptimal slide splitting | -1 |
| Minor | Minor text formatting differences | -1 |

## Conversion Accuracy (vs. source)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Content fabricated (not in source) | -20 |
| Critical | Key content missing | -15 |
| Major | Image quality degradation | -5 |
| Major | Equation transcription error | -5 |
| Major | Table data error | -5 |
| Minor | Minor text rephrasing | -1 |
| Minor | Layout differs from source | -1 |

## R Scripts (.R)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors | -100 |
| Critical | Domain-specific bugs | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing set.seed() | -10 |
| Major | Missing figure generation | -5 |

## Enforcement

- **Score < 80:** Block commit. List blocking issues.
- **Score < 90:** Allow commit, warn. List recommendations.
- User can override with justification.

## Quality Reports

Generated **only at merge time**. Use `templates/quality-report.md` for format.
Save to `quality_reports/merges/YYYY-MM-DD_[branch-name].md`.
