# Skill: Generate Slides from Academic Paper

**Command:** `/slides-from-paper [file]`
**Description:** Read a PDF academic paper and generate pedagogical Beamer slides.

## Arguments

- `file` (required): Path to PDF paper (typically in `master_supporting_docs/`)

## Procedure

1. **Read the PDF**: Use Claude to read the paper page by page
   - Identify: title, authors, abstract, sections, key equations, figures, tables

2. **Extract figures**: Use `pdfimages` or PyMuPDF to extract embedded images
   ```bash
   pdfimages -png paper.pdf output/[name]/images/fig
   ```
   - Rename to `fig_01.png`, `fig_02.png`, etc.
   - Match to paper figure numbers where possible

3. **Design slide structure** following the mapping:

   | Paper Section | Slides | Content |
   |---------------|--------|---------|
   | Title | 1 | Title, authors, date |
   | Motivation | 1 | Research question, why it matters |
   | Contribution | 1 | What this paper does (3-4 bullets) |
   | Literature | 1 | Key papers in table format |
   | Model/Theory | 2-4 | Equations with intuition, progressive buildup |
   | Data | 1-2 | Sample description, summary stats |
   | Results | 2-4 | Key tables/figures with interpretation |
   | Robustness | 1-2 | Main checks only |
   | Takeaways | 1 | Key findings, implications |

4. **Handle equations**:
   - Convert all equations to LaTeX notation
   - Use `align` for multi-line equations
   - Add intuition below key equations: "where $X$ is..."
   - Flag any equations that are images: `% TODO: convert equation from image`

5. **Handle citations**:
   - Extract references cited in the paper
   - Check against `Bibliography_base.bib`
   - Add missing BibTeX entries
   - Use `\citet{}` for "Author (Year)" and `\citep{}` for "(Author, Year)"

6. **Generate `.tex`**:
   ```latex
   \input{../../Preambles/header}
   \title{[Paper Title]}
   \subtitle{[Journal, Year]}
   \author{[Authors]}
   \graphicspath{{images/}}
   \begin{document}
   \maketitle
   % ... slides ...
   \bibliography{../../Bibliography_base}
   \end{document}
   ```

7. **Compile and verify**

8. **Report**: Slide count, flagged TODOs (equations as images), missing citations

## Rules to Follow

- `.claude/rules/pdf-paper-analysis.md` — section mapping, citation handling
- `.claude/rules/beamer-output-standards.md` — content density, formatting
- `.claude/rules/quality-gates.md` — conversion accuracy rubric

## Output

- `output/[name]/[name].tex` — generated Beamer slides
- `output/[name]/images/` — extracted figures
- `output/[name]/manifest.json` — extraction manifest
