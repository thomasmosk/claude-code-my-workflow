---
paths:
  - "output/**"
  - "master_supporting_docs/**/*.pptx"
---

# PPT Extraction Protocol

## Image Quality Standards

- **Minimum resolution:** 150 DPI
- **Format:** PNG for raster images (preserve transparency)
- **Aspect ratio:** Always preserve original aspect ratio
- **Naming:** `slide_NN_img_MM.png` (zero-padded, 1-indexed)

## Extraction Procedure

1. Parse PPT using `python-pptx`
2. For each slide:
   - Extract all images (shapes with `image` property)
   - Extract all text (shapes with `text_frame` property)
   - Record layout type (title, content, two-column, blank)
3. Save images to `output/[name]/images/`
4. Generate `manifest.json` with:
   - Source file path and hash (SHA-256)
   - Extraction timestamp
   - Per-slide: layout type, text content, image filenames
   - Total slide count and image count

## Naming Conventions

```
output/
└── lecture_name/            # Sanitized: lowercase, underscores, no spaces
    ├── images/
    │   ├── slide_01_img_01.png
    │   ├── slide_01_img_02.png
    │   ├── slide_02_img_01.png
    │   └── ...
    ├── lecture_name.tex
    └── manifest.json
```

## Quality Checklist

```
[ ] All images extracted (count matches source)
[ ] No corrupt/zero-byte images
[ ] Images ≥ 150 DPI (or source resolution if lower)
[ ] Aspect ratios preserved
[ ] Naming convention followed
[ ] Manifest is complete and valid JSON
[ ] Text content captured for all slides
```
