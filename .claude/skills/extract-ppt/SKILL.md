# Skill: Extract PowerPoint Content

**Command:** `/extract-ppt [file]`
**Description:** Extract all images and text from a PowerPoint file into the output directory.

## Arguments

- `file` (required): Path to `.pptx` file (typically in `master_supporting_docs/`)

## Procedure

1. **Validate input**: Confirm file exists and is `.pptx`

2. **Determine output name**: Sanitize filename → lowercase, underscores, no extension
   - `Lecture 01 - Introduction.pptx` → `lecture_01_introduction`

3. **Create output structure**:
   ```
   output/[name]/
   └── images/
   ```

4. **Extract using python-pptx**:
   ```python
   from pptx import Presentation
   from pptx.util import Inches, Emu
   import json, hashlib, os
   from datetime import datetime

   prs = Presentation(file_path)
   manifest = {
       "source_file": file_path,
       "source_hash": hashlib.sha256(open(file_path, 'rb').read()).hexdigest(),
       "extraction_date": datetime.now().isoformat(),
       "slides": []
   }

   for slide_idx, slide in enumerate(prs.slides, 1):
       slide_data = {"slide_number": slide_idx, "text": [], "images": [], "layout": ""}
       img_count = 0

       for shape in slide.shapes:
           if shape.has_text_frame:
               for para in shape.text_frame.paragraphs:
                   text = para.text.strip()
                   if text:
                       slide_data["text"].append(text)

           if shape.shape_type == 13:  # Picture
               img_count += 1
               img_name = f"slide_{slide_idx:02d}_img_{img_count:02d}.png"
               img_path = os.path.join(output_dir, "images", img_name)
               with open(img_path, 'wb') as f:
                   f.write(shape.image.blob)
               slide_data["images"].append(img_name)

       manifest["slides"].append(slide_data)

   with open(os.path.join(output_dir, "manifest.json"), 'w') as f:
       json.dump(manifest, f, indent=2)
   ```

5. **Validate extraction**: Check image count, file sizes, manifest completeness

6. **Report**: Print summary — slide count, image count, output path

## Rules to Follow

- `.claude/rules/ppt-extraction-protocol.md` — image quality, naming conventions
- `.claude/rules/single-source-of-truth.md` — output structure enforcement

## Output

- `output/[name]/images/*.png` — extracted images
- `output/[name]/manifest.json` — extraction manifest with text + metadata
