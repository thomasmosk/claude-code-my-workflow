---
paths:
  - "master_supporting_docs/**/*.pdf"
  - "output/**"
---

# PDF Paper Analysis Protocol

## Paper Section → Slide Mapping

| Paper Section | Target Slides | Key Content to Extract |
|---------------|--------------|----------------------|
| Title/Abstract | 1 title + 1 motivation | Research question, key finding |
| Introduction | 2-3 slides | Context, gap, contribution |
| Literature Review | 1 slide (table format) | Key papers, positioning |
| Model/Theory | 2-4 slides | Key equations, assumptions, intuition |
| Data | 1-2 slides | Sample, summary statistics |
| Methodology | 2-3 slides | Estimation strategy, identification |
| Results | 2-4 slides | Main tables/figures with interpretation |
| Robustness | 1-2 slides | Key checks only (not exhaustive) |
| Conclusion | 1 slide | Takeaways, implications, future work |

## Figure Extraction

1. Use `pdfimages` (from poppler-utils) to extract embedded images
2. Fallback: use PyMuPDF (`fitz`) for page-level rendering
3. Save extracted figures to `output/[name]/images/`
4. Name as `fig_NN.png` (matching paper figure numbers where possible)

## Citation Handling

1. Extract cited references from the paper
2. Match against `Bibliography_base.bib`
3. Add missing entries to bibliography
4. Use `\cite{}` / `\citep{}` / `\citet{}` in generated slides

## Equation Handling

- **Inline equations:** Convert to LaTeX `$...$`
- **Display equations:** Convert to `\begin{equation}...\end{equation}` or `align`
- **Equations in figures:** Flag with `% TODO: convert equation from image` comment
- **Numbered equations:** Preserve numbering with `\tag{}`

## Content Transformation Rules

1. **Never copy-paste prose** — synthesize into bullet points
2. **Tables:** Recreate in LaTeX with `booktabs`, not as images
3. **Figures:** Include as images with proper captions
4. **Progressive disclosure:** Build complex ideas across multiple slides
5. **Interpretation slides:** Add "What does this mean?" after results
