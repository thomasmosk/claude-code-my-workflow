---
paths:
  - "output/**/*.tex"
  - "Slides/**/*.tex"
  - "master_supporting_docs/**"
---

# Conversion Knowledge Base

## PPT Layout Patterns

| PPT Pattern | Beamer Mapping | Notes |
|-------------|---------------|-------|
| Title slide | `\titlepage` | Extract title, subtitle, author |
| Bullet list | `\begin{itemize}` | Max 7 bullets, 2 nesting levels |
| Two-column | `\begin{columns}` | Use `0.48\textwidth` per column |
| Full-image slide | `\includegraphics[width=\textwidth]` | Center with `\centering` |
| Image + text | `columns` environment | Image left/right, text opposite |
| Table | `\begin{tabular}` + `booktabs` | Use `\toprule`, `\midrule`, `\bottomrule` |
| Section header | `\section{}` | Creates Metropolis section slide |

## PDF Structure Mapping

| Paper Section | Slide Structure | Approach |
|---------------|----------------|----------|
| Abstract | 1 motivation slide | Key question + contribution |
| Introduction | 2-3 slides | Context → gap → contribution |
| Literature | 1 slide (table) | Key papers, positioned vs. this work |
| Model/Theory | 2-4 slides | Progressive equation buildup |
| Data | 1-2 slides | Summary stats, sample description |
| Results | 2-4 slides | Main tables/figures, interpretation |
| Robustness | 1-2 slides | Key checks only |
| Conclusion | 1 slide | Takeaways + future work |

## Beamer Environment Usage

| Environment | When to Use | Example |
|-------------|-------------|---------|
| `frame` | Every slide | Standard content |
| `block` | Grouped content | Definition, theorem |
| `alertblock` | Warnings/caveats | Assumptions, limitations |
| `exampleblock` | Worked examples | Numerical illustrations |
| `columns` | Side-by-side content | Image + text, comparisons |
| `itemize` | Bullet lists | Max 7 items |
| `enumerate` | Ordered steps | Procedures, algorithms |

## Conversion Pitfalls

| Pitfall | Impact | Prevention |
|---------|--------|-----------|
| Equations as images | Unscalable, ugly | Always convert to LaTeX math |
| Overstuffed slides | Poor readability | Max 7 bullets, split if needed |
| Missing images | Compilation fails | Verify all `\includegraphics` paths |
| Wrong aspect ratio | Distorted figures | Preserve original aspect ratio |
| Font size chaos | Inconsistent look | Use Metropolis defaults, avoid manual sizing |
| Nested bullets > 2 levels | Hard to read | Flatten or restructure |
