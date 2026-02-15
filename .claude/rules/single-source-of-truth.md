---
paths:
  - "output/**"
  - "Slides/**/*.tex"
  - "master_supporting_docs/**"
---

# Single Source of Truth: Enforcement Protocol

**PPT/PDF source files are the authoritative source for ALL converted content.** Beamer `.tex` is derived.

## The SSOT Chain

```
PPT/PDF Source Files (SOURCE OF TRUTH)
  ├── output/[name]/images/        (extracted images — derived)
  ├── output/[name]/manifest.json  (extraction manifest — derived)
  ├── output/[name]/[name].tex     (generated Beamer — derived)
  ├── Bibliography_base.bib        (shared, manually curated)
  └── Slides/**/*.tex              (manually authored — independent)

NEVER modify generated .tex without re-checking against source.
ALWAYS re-extract when source PPT/PDF is updated.
Slides/ directory is for manually authored slides (independent SSOT).
```

---

## Conversion Freshness Protocol (MANDATORY)

**Before modifying any converted slide, verify it matches the current source.**

### Freshness Check Procedure

1. Check the extraction manifest (`manifest.json`) for source file hash
2. Compare against current source file
3. If source has changed: re-extract images, regenerate .tex
4. Only then make manual edits to the generated .tex

### When to Re-Extract

Re-extract ALL content when:
- The source PPT/PDF file has been modified since last extraction
- Image quality issues are reported
- Before any commit that includes converted slide changes

---

## Output Structure Enforcement (MANDATORY)

**Every conversion MUST follow this directory structure:**

```
output/
└── [lecture_name]/
    ├── images/
    │   ├── slide_01_img_01.png
    │   ├── slide_02_img_01.png
    │   └── ...
    ├── [lecture_name].tex
    └── manifest.json
```

1. Lecture name derives from source filename (sanitized: lowercase, underscores)
2. Images use `slide_NN_img_MM.png` naming convention
3. Manifest records source file, extraction date, slide count, image inventory

---

## Content Fidelity Checklist

```
[ ] Slide count: source slides ≈ Beamer frames (± reasonable consolidation)
[ ] Image check: every source image extracted and included
[ ] Text check: all key text content preserved
[ ] Equation check: equations rendered in LaTeX (not as images)
[ ] Table check: tables recreated in LaTeX where feasible
[ ] No invented content: Beamer does not add content not in source
[ ] No dropped content: every source idea appears in Beamer
```
