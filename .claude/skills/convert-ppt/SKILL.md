# Skill: Convert PowerPoint to Beamer

**Command:** `/convert-ppt [file]`
**Description:** Full pipeline: extract PPT content, generate Beamer `.tex`, compile to verify.

## Arguments

- `file` (required): Path to `.pptx` file (typically in `master_supporting_docs/`)

## Procedure

1. **Run extraction first**: Execute the `/extract-ppt` skill on the file

2. **Read the manifest**: Load `output/[name]/manifest.json`

3. **Generate Beamer `.tex`**: Create `output/[name]/[name].tex` with:

   ```latex
   \input{../../Preambles/header}

   \title{[Extracted Title]}
   \author{[Author if found]}
   \date{}

   \graphicspath{{images/}}

   \begin{document}
   \maketitle
   ```

4. **Convert each slide** based on content type:

   | Source Content | Beamer Output |
   |---------------|--------------|
   | Title only | `\section{Title}` |
   | Bullets | `\begin{frame}{Title}\begin{itemize}...\end{itemize}\end{frame}` |
   | Image only | `\begin{frame}{Title}\centering\includegraphics[width=0.9\textwidth]{img}\end{frame}` |
   | Image + text | Two-column layout with `\begin{columns}` |
   | Table | Recreate with `tabular` + `booktabs` |
   | Two-column PPT | Map to `\begin{columns}` |

5. **Apply content limits**:
   - Max 7 bullet points per slide (split if more)
   - Max 2 nesting levels
   - Add `\note{}` for presenter notes if found in PPT

6. **Close document**:
   ```latex
   \bibliography{../../Bibliography_base}
   \end{document}
   ```

7. **Compile to verify**:
   ```bash
   cd output/[name] && TEXINPUTS=../../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode [name].tex
   ```

8. **Report**: Summary with slide count, any compilation warnings, output path

## Rules to Follow

- `.claude/rules/ppt-extraction-protocol.md` — extraction standards
- `.claude/rules/beamer-output-standards.md` — content density, image inclusion
- `.claude/rules/single-source-of-truth.md` — output structure
- `.claude/rules/quality-gates.md` — converted slides rubric

## Output

- `output/[name]/[name].tex` — generated Beamer file
- `output/[name]/[name].pdf` — compiled PDF
- `output/[name]/images/` — extracted images
- `output/[name]/manifest.json` — extraction manifest
