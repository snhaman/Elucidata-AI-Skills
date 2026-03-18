---
name: elucidata-slides
description: >
  Creates Google Slides-compatible .pptx presentations that precisely follow the Elucidata / Polly
  brand system from the 2025 Master Template Guide. Use this skill whenever the user asks to create
  slides, a deck, a presentation, or any slide content for Elucidata, Polly, or internal/external
  company use. Trigger even if the user just says "make me some slides" or "create a deck" — always
  apply the Elucidata brand. Outputs a .pptx file that imports directly into Google Slides.
  Also trigger when the user says "Elucidata deck", "Polly slides", or wants branded slide content
  of any kind. Trigger when the user shares a Google Drive link, uploads a .pptx or .pdf, and
  wants it converted to Elucidata brand.
---

# Elucidata Slides Skill

Produces branded `.pptx` decks matching the Elucidata 2025 Master Template Guide.
Imports directly into Google Slides via File → Import slides or drag onto slides.google.com.

Before starting: Read [brand-system.md](references/brand-system.md) for colors and tokens.
Read [slide-layouts.md](references/slide-layouts.md) for the 9 available layouts.

**Bundled assets** (base64-encode and embed):
- `assets/cover-bg.png` — Full-bleed background for cover slides
- `assets/thankyou-bg.png` — Background for Thank You slide (art fills top ~65%, white below)

---

## Two modes of operation

### Mode A — New deck (from scratch or outline)
Full brand treatment: layout selection, fonts, colors, accent elements, slide numbers, logo mark.

### Mode B — Theme pass (converting existing content)
Apply brand surface only. Do not restructure, reorder, or regroup slides.

**What to apply in Mode B:**
- Fonts: Space Grotesk for titles, Inter for body — always
- Colors: map existing text colors to brand palette (titles → `2A263F`, body → `434343`, accents → orange or purple)
- Slide background → `F8F7FC`
- Slide number bottom-right (`BD8FF7`, Inter 14px) on every content slide
- Logo mark top-right (small `8E42EE` rounded shape, w=0.18, h=0.18, x=9.6, y=0.1)
- Rounded corners on any card or box shapes (`rectRadius: 0.12`)
- Card borders → `E1DFEC`, lineSize 0.5

**What NOT to apply in Mode B:**
- Do not move or reorganize content
- Do not snap to a layout unless the slide already matches one (see Layout Matching below)
- Do not add icon containers — use placeholders instead (see Icons below)

---

## Input sourcing

### Google Drive link
If the user provides a Google Drive or Google Slides URL, use the `google_drive_fetch` tool to pull the file content. Extract slide titles, body text, and structure from the result, then proceed with Mode B.

### Uploaded .pptx or .pdf
If a file is uploaded, it will be available at `/mnt/user-data/uploads/`. Extract content:

```bash
# For .pptx — extract text per slide
python3 -c "
from pptx import Presentation
prs = Presentation('/mnt/user-data/uploads/input.pptx')
for i, slide in enumerate(prs.slides):
    print(f'--- Slide {i+1} ---')
    for shape in slide.shapes:
        if shape.has_text_frame:
            for para in shape.text_frame.paragraphs:
                print(para.text)
"

# For .pdf — extract text
pip install pymupdf --break-system-packages -q
python3 -c "
import fitz
doc = fitz.open('/mnt/user-data/uploads/input.pdf')
for i, page in enumerate(doc):
    print(f'--- Slide {i+1} ---')
    print(page.get_text())
"
```

Extract only titles and body text. Do not attempt to reconstruct exact layouts from PDF — use the text content and proceed with Mode B, keeping the original slide count and structure.

---

## Layout matching (Mode B)

Only snap to a layout from [slide-layouts.md](references/slide-layouts.md) if the existing slide content already matches it structurally. Do not restructure to force a match.

| If the slide already has... | Use layout |
|---|---|
| 2–3 cards or columns side by side | Column Comparison (Cards) |
| 3+ numbered steps in sequence | Numbers + Pointers |
| Large KPI numbers in a grid | Metrics / Numerics |
| People names + roles in a grid | Team Cards |
| Agenda / TOC list | Agenda |
| Anything else | Brand pass only — fonts, colors, no restructuring |

---

## Icons

Never render icons. Instead, add a small labeled placeholder wherever an icon would go:

```javascript
// Icon placeholder — user fills in Google Slides
slide.addShape(pres.ShapeType.rectRounded, {
  x: iconX, y: iconY, w: 0.5, h: 0.5,
  fill: { color: "F1E8FD" },
  line: { color: "BD8FF7", width: 0.5 },
  rectRadius: 0.12
});
slide.addText("[icon]", {
  x: iconX, y: iconY, w: 0.5, h: 0.5,
  fontFace: "Inter", fontSize: 9, color: "8E42EE",
  align: "center", valign: "middle"
});
```

Tell the user at the end: "Icon placeholders are marked `[icon]` — replace them in Google Slides using Insert → Image or a Slides icon plugin."

---

## Critical pptxgenjs rules

- NEVER use `#` in hex colors — `"F78E12"` not `"#F78E12"` (causes file corruption)
- NEVER encode opacity in hex (no 8-char hex) — use `opacity` property separately
- NEVER reuse options objects across multiple addShape/addText calls — pptxgenjs mutates them
- Always use `fontFace: "Space Grotesk"` for titles, `fontFace: "Inter"` for body
- Always set `rectRadius: 0.12` on any rounded shape — never use plain `rect`
- Read `/mnt/skills/public/pptx/pptxgenjs.md` for the full API before writing code

**Base setup (always use this):**
```javascript
const pptxgen = require("pptxgenjs");
const fs = require("fs");
const pres = new pptxgen();
pres.layout = 'LAYOUT_16x9'; // 10" x 5.625"

const coverB64 = 'image/png;base64,' + fs.readFileSync('./assets/cover-bg.png').toString('base64');
const tyB64    = 'image/png;base64,' + fs.readFileSync('./assets/thankyou-bg.png').toString('base64');
```

**Key measurements (inches, 10" x 5.625"):**
- Left/right margin: x=0.5, max content width: w=9.0
- Slide title: x=0.5, y=0.3, w=8.7, h=0.55
- Content area: y=1.05 to y=5.1
- Slide number: x=9.4, y=5.3, w=0.5, h=0.2

---

## Workflow

### 1. Determine mode and source
- Is this a new deck or an existing one being converted? → Mode A or Mode B
- Is the source a Google Drive link, uploaded file, or user-provided outline?
- Fetch or extract content before writing any code

### 2. Plan slides
- Mode A: map each slide to a layout from [slide-layouts.md](references/slide-layouts.md). Vary layouts — do not repeat the same layout more than twice in a row. Cover and Thank You are optional — only add when explicitly requested.
- Mode B: use the layout matching table above. For anything that doesn't match, brand pass only.

### 3. Write and run the script in batches

**Never write the entire script in one block.**

Split into batches of 3–4 slides. For every batch:
1. Write the JS for that batch
2. Run it immediately to catch errors early
3. Fix any errors before moving to the next batch

For long decks (8+ slides), write a helper function per layout type:

```javascript
function addContentSlide(pres, { title, bullets }) {
  const slide = pres.addSlide();
  slide.addText(title, { x:0.5, y:0.3, w:8.7, h:0.55, fontFace:"Space Grotesk", fontSize:22, bold:true, color:"2A263F" });
  // ... body
}
```

### 4. QA
```bash
node generate-deck.js
python /mnt/skills/public/pptx/scripts/office/soffice.py --headless --convert-to pdf /mnt/user-data/outputs/deck.pptx
pdftoppm -jpeg -r 150 /mnt/user-data/outputs/deck.pdf /home/claude/slide
```
View slide images. Fix overflow, color, or layout issues. Re-run until clean.

### 5. Present
Present the .pptx and tell the user:
"Import into Google Slides by dragging onto slides.google.com or File → Import slides. For correct fonts, add Space Grotesk and Inter via More Fonts in Google Slides. Icon placeholders are marked `[icon]` — replace them using Insert → Image or a Slides icon plugin."

---

## Key design rules

- **Purple** = Polly / Elucidata brand identity
- **Orange** = Action, impact, emphasis — most slides have at least one orange element
- **Pink / Cyan** = Third-party content, or color relief on slides with no natural purple/orange
- **Green** = Positive outcomes, gains, success
- **Red** = Negative outcomes, risks, failure states
- Never mix purple and orange on the same card without clear hierarchy
- Titles: Space Grotesk, body: Inter — always
- Slide number bottom-right on every content slide (skip on cover and thank you)
- **Rounded corners everywhere** — rectRadius: 0.12 minimum on all shapes
- Cards: white fill, border `E1DFEC`, rectRadius 0.12
- Font sizes: default to the lower end of each range; reserve large sizes for callouts or stat-only slides
