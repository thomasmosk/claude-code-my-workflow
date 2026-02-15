# Skill: Generate Slides from Textbook Chapter

**Command:** `/slides-from-chapter [file]`
**Description:** Read a PDF textbook chapter and generate structured Beamer slides preserving pedagogical flow.

## Arguments

- `file` (required): Path to PDF chapter (typically in `master_supporting_docs/`)
- Optional: page range (e.g., `pages=1-30`)

## Procedure

1. **Read the PDF**: Use Claude to read the chapter page by page
   - Identify: chapter title, sections, subsections, definitions, theorems, examples, exercises

2. **Extract figures**: Use `pdfimages` or PyMuPDF
   ```bash
   pdfimages -png chapter.pdf output/[name]/images/fig
   ```

3. **Preserve chapter structure**: Map sections to slide groups

   | Chapter Element | Beamer Mapping |
   |----------------|---------------|
   | Chapter title | `\title{}` + title slide |
   | Section heading | `\section{}` (Metropolis section divider) |
   | Subsection | `\subsection{}` or frame title |
   | Definition | `\begin{block}{Definition: Name}` |
   | Theorem | `\begin{block}{Theorem (Attribution)}` |
   | Proof | `\begin{block}{Proof Sketch}` (abbreviated) |
   | Example | `\begin{exampleblock}{Example}` |
   | Remark | `\begin{alertblock}{Remark}` |
   | Key equation | Centered `align` environment |

4. **Handle dense mathematical content**:
   - Use **progressive disclosure**: build equations across 2-3 slides
   - First slide: setup and assumptions
   - Second slide: key derivation steps
   - Third slide: final result + interpretation
   - Use `\pause` sparingly for step-by-step reveals within a frame

5. **Handle definitions and theorems**:
   - Each definition gets its own slide
   - Theorems: statement on one slide, proof sketch on next (if included)
   - Always follow with an example/application slide

6. **Content transformation**:
   - **Never dump paragraphs** — synthesize into bullets
   - **Exercises:** Select 1-2 representative examples, present as "Try This"
   - **Proofs:** Abbreviate to key steps unless proof technique is the learning objective
   - **Cross-references:** Note dependencies ("Recall Definition 2.3...")

7. **Generate `.tex`** with proper structure:
   ```latex
   \input{../../Preambles/header}
   \title{Chapter N: [Title]}
   \subtitle{[Textbook Name]}
   \graphicspath{{images/}}
   \begin{document}
   \maketitle
   \section{Section Title}
   % ... structured slides ...
   \bibliography{../../Bibliography_base}
   \end{document}
   ```

8. **Compile and verify**

9. **Report**: Slide count, section breakdown, flagged TODOs

## Rules to Follow

- `.claude/rules/pdf-paper-analysis.md` — PDF extraction, equation handling
- `.claude/rules/beamer-output-standards.md` — content density, environments
- `.claude/rules/quality-gates.md` — conversion accuracy rubric

## Output

- `output/[name]/[name].tex` — generated Beamer slides
- `output/[name]/images/` — extracted figures
- `output/[name]/manifest.json` — extraction manifest
