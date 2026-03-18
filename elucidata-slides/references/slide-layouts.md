# Elucidata Slide Layouts — Reference

All layouts follow the brand tokens in brand-system.md.
For any slide whose content does not fit a layout below, apply the brand system (fonts, colors, tokens, card style, rounded corners) but preserve the original structure as-is.

---

## Layout Catalog

### 1. Cover Slide (Full Bleed)
**When**: Deck opener — only include when explicitly requested.
**Structure**:
- `assets/cover-bg.png` as full-bleed background
- Text anchored to left side (the dark, empty region of the image)
- Title: Space Grotesk Bold 64–72px, white; accent word in `F78E12` (orange)
- Subtitle: Inter Regular 22px, `BD8FF7`
- Bottom-left: company name or deck context, Inter 15px, `BD8FF7` at 60% opacity
- No slide number, no logo mark overlay (logo is in the background image)

### 2. Agenda / Contents Slide
**When**: Table of contents, section list, agenda.
**Structure**:
- Light background `F8F7FC`
- Title: Space Grotesk SemiBold 36px, dark text
- Items as styled rows — orange left-border accent, Inter 22px, `2A263F`
- Optional: purple dot on active/current item

### 3. Title + Body (Full Text)
**When**: Explanation slides, guidelines, text-heavy content.
**Structure**:
- Light background
- Title top-left
- Body: 2–3 paragraphs or bullet points, Inter 18–21px, `434343`
- Optional: small colored left-border accent on first paragraph

### 4. 2 or 3 Column Comparison (Cards)
**When**: Comparing 2 or 3 concepts, features, options, or time periods.
**Structure**:
- Title top
- 2 or 3 equal-width cards side by side (card style: white bg, border `E1DFEC`, rectRadius 0.12, shadow)
- Each card: colored subheading + body text (2–3 lines)
- Card accent: left border or top bar in orange (general) or purple (Polly/brand content)
- For positive/negative comparisons: green accent on positive column, red on negative

### 5. Numbers + Pointers (Horizontal)
**When**: Numbered steps, ordered process, sequential explanations.
**Structure**:
- Title top
- 3 rows (or 2–4): large number on left (Space Grotesk Bold 60px, orange or purple) + title (Inter SemiBold 20px) + description (Inter Regular 18px) on right
- Subtle horizontal divider between rows

### 6. Title + Body + Highlights (Callout)
**When**: Key insights, important points to emphasize, featured stats alongside context.
**Structure**:
- Left ~55%: title + body text, Inter 18–21px
- Right ~40%: 2–3 highlight callout boxes (card style, colored tinted bg)
- Callout bg: `F1E8FD` for purple highlights, `FCEEDE` for orange highlights
- Callout text: Inter SemiBold 18px, accent color

### 7. Metrics / Numerics Slide
**When**: KPIs, stats dashboard, quantitative results.
**Structure**:
- Title top
- 2x2 or 1x3 grid of metric cards (card style)
- Each card: large number (Space Grotesk Bold 56–60px, orange or purple), label below (Inter 18px, `434343`)
- Optional: small trend description or delta in muted text

### 8. Team Cards Slide
**When**: Team introductions, speaker bios, stakeholder mapping.
**Structure**:
- Title top
- 4-up or 6-up grid of cards (card style)
- Each card: circular image placeholder (60x60px, bg `F1E8FD`), Name (Inter SemiBold 20px, `2A263F`), Designation (Inter Regular 17px, `434343`)

### 9. Thank You / End Slide
**When**: Closing slide — only include when explicitly requested.
**Structure**:
- White slide background `FFFFFF`
- `assets/thankyou-bg.png` positioned to fill top ~65-70% of slide
- Text block in the white area at the bottom:
  - "Thank" in Space Grotesk Bold 72px, `F78E12` orange + " You!" in `2A263F` dark — same line
  - Contact: `elucidata.io | info@elucidata.io`, Inter Regular 21px, `8E42EE`
- No slide number

---

## Layout Selection Guide

| Content type | Layout |
|---|---|
| Opening (if requested) | Cover |
| Agenda / TOC | Agenda |
| 2-3 features or options compared | Column Comparison (Cards) |
| Step-by-step process | Numbers + Pointers |
| Long explanation or bullets | Title + Body |
| Stats with context | Title + Body + Highlights |
| KPIs / metrics dashboard | Metrics / Numerics |
| Team or speaker bios | Team Cards |
| Closing (if requested) | Thank You |
| Anything else | Apply brand system, keep original structure |
