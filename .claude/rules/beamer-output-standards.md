---
paths:
  - "output/**/*.tex"
  - "Slides/**/*.tex"
---

# Beamer Output Standards

## Preamble Requirements

All generated `.tex` files MUST:
- Use `\input{../../Preambles/header}` (adjust relative path as needed)
- Set `\graphicspath{{images/}}` for converted slides
- Include `\bibliography{../../Bibliography_base}` if citations are used
- NOT redefine colors or theme settings already in `header.tex`

## Content Density Limits

| Element | Maximum | Action if Exceeded |
|---------|---------|-------------------|
| Bullet points per slide | 7 | Split into multiple slides |
| Nesting levels | 2 | Flatten structure |
| Words per bullet | ~15 | Tighten language |
| Equations per slide | 3 (display) | Use progressive buildup |
| Columns | 2 | Redesign layout |

## Image Inclusion Standards

```latex
% Standard full-width image
\begin{center}
  \includegraphics[width=0.9\textwidth]{slide_01_img_01}
\end{center}

% Image in column
\begin{column}{0.48\textwidth}
  \includegraphics[width=\textwidth]{slide_02_img_01}
\end{column}
```

- Always use relative widths (`\textwidth`, `\linewidth`)
- Never hardcode pixel dimensions
- Omit file extensions (LaTeX finds the right format)
- Preserve aspect ratio (use only `width=` OR `height=`, not both)

## Table Formatting

- Always use `booktabs` (`\toprule`, `\midrule`, `\bottomrule`)
- Use `\centering` before tabular
- For wide tables: use `\resizebox{\textwidth}{!}{...}` or `\small`
- Align numbers on decimal points where appropriate

## Environment Usage Guide

| Content Type | Environment | Notes |
|-------------|-------------|-------|
| Key definition | `\begin{block}{Title}` | Metropolis styled |
| Warning/caveat | `\begin{alertblock}{Title}` | Red-tinted |
| Example | `\begin{exampleblock}{Title}` | Green-tinted |
| Theorem | `\begin{block}{Theorem (Author)}` | With attribution |
| Proof sketch | `\begin{block}{Proof Sketch}` | Abbreviated |

## Compilation Test

After generating any `.tex` file in `output/`, verify with:

```bash
cd output/[name] && TEXINPUTS=../../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode [name].tex
```

Must compile with zero errors. Warnings acceptable but should be minimized.
