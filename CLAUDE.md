# CLAUDE.MD -- Academic Slide Builder

**Project:** Academic Slide Builder
**Institution:** Queen Mary University of London
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- PPT/PDF source files are authoritative; Beamer `.tex` is derived
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Folder Structure

```
academic-slide-builder/
├── CLAUDE.MD                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # Metropolis Beamer preamble
├── Slides/                      # Manually authored Beamer .tex files
├── output/                      # Converted slide output (per-lecture subdirs)
│   └── [lecture_name]/
│       ├── images/              # Extracted images
│       ├── [lecture_name].tex   # Generated Beamer .tex
│       └── manifest.json        # Extraction manifest
├── scripts/                     # Utility scripts
├── quality_reports/             # Plans, session logs, merge reports
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/      # Source PPTs, PDFs, papers
```

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# Compile converted slides (from output directory)
cd output/lecture_name && TEXINPUTS=../../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode lecture_name.tex

# Install Python dependencies
pip install -r scripts/requirements.txt

# Quality score
python scripts/quality_score.py output/lecture_name/lecture_name.tex
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/extract-ppt [file]` | Extract images + text from PowerPoint |
| `/convert-ppt [file]` | PPT → Beamer slides (full pipeline) |
| `/slides-from-paper [file]` | PDF paper → pedagogical Beamer slides |
| `/slides-from-chapter [file]` | PDF chapter/textbook → structured Beamer slides |
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/commit [msg]` | Stage, commit, PR, merge |

---

## Current Project State

| Source | Output | Status | Notes |
|--------|--------|--------|-------|
| *(no conversions yet)* | -- | -- | Ready to process PPT/PDF files |
