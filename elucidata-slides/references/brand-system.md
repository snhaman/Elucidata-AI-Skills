# Elucidata Brand System — 2025 Token Reference

## Fonts

| Role | Font | Weight | Size |
|------|------|--------|------|
| Intro/breaker title | Space Grotesk | Bold (700) | 60–72px |
| Slide title | Space Grotesk | SemiBold (600) | 32–38px |
| Card title / pointer heading | Inter | SemiBold (600) | 22–26px |
| Body copy (primary) | Inter | Regular (400) | 18–21px |
| Body copy / image titles / notes | Inter | Regular (400) | 16–18px |
| Body copy / source links | Inter | Regular (400) | 14–16px |

**Font size guidance**: Most decks are text-heavy. Default to the lower end of each range. Use the upper end only when a slide is intentionally light on content and needs visual weight. Intro and breaker titles are the exception — always keep these large.

Google Fonts import URL:
```
https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&family=Inter:wght@400;600&display=swap
```

---

## Color Palette

### Core Theme Colors (use these for primary UI)

| Name | Hex | Usage |
|------|-----|-------|
| Deep Purple | `#2B0061` | Darkest purple bg, dark slides |
| Brand Purple | `#501899` | Primary purple accent, card fills (Polly/Elucidata) |
| Purple Mid | `#8E42EE` | Interactive purple, highlights |
| Purple Light | `#BD8FF7` | Light purple accents |
| Purple Tint | `#F1E8FD` | Purple-tinted card backgrounds |
| Deep Orange | `#904E00` | Darkest orange |
| Brand Orange | `#CB6E00` | Primary orange accent |
| Orange Mid | `#F78E12` | Default orange (most slides) |
| Orange Light | `#FFC27A` | Light orange highlights |
| Orange Tint | `#FCEEDE` | Orange-tinted card backgrounds |
| Teal Dark | `#016379` | External/cyan dark |
| Teal Mid | `#1D93AD` | External accent |
| Cyan Light | `#6CCADE` | Cyan highlight |
| Cyan Tint | `#CDF4FC` | Cyan-tinted background |
| Cyan Pale | `#EDF9FB` | Very light cyan bg |
| Pink Deep | `#8E1F75` | External/partner dark |
| Pink Mid | `#CA4BAE` | Pink accent |
| Pink Light | `#E587D0` | Light pink |
| Pink Tint | `#FBE3F5` | Pink-tinted bg |
| Pink Pale | `#FCF1F9` | Very light pink bg |

### Neutral / UI Colors

| Name | Hex | Usage |
|------|-----|-------|
| Dark Text | `#2A263F` | Primary text color (near-black, purple-tinted) |
| Light Background | `#F8F7FC` | Slide background (off-white with slight purple) |
| Card Border | `#E1DFEC` | Subtle border on cards, chart frames |
| White | `#FFFFFF` | On dark backgrounds, card fills |
| Body Text | `#434343` | Secondary / body text |

### Chart Colors (use in this order for data viz)

Primary: `#7235BE`, `#F78E12`, `#BD3A7A`, `#06B6D4`, `#99002E`, `#304AB5`, `#24CF35`, `#C6B512`
Offset/muted: `#C7A0F7`, `#FCD2A0`, `#F5A3CC`, `#9BE2EE`, `#FFB2CA`, `#B1BEF3`, `#BDF1C2`, `#FBF18B`
Neutral: `#CCCCCC`, `#D2C6FA`, `#E9E3FC`

---

## Color Usage Rules

**Purple** = Polly and Elucidata brand identity — the primary brand color
- Brand announcements, Polly product cards, Elucidata identity slides, breaker slides for brand sections
- Slide titles can use purple text when it's a Polly/Elucidata-specific section

**Orange** = Action and impact — the main accent color
- Use for highlights, CTAs, key stats, emphasis, and anything you want the eye to land on
- Orange is the primary accent; most slides will have at least one orange element

**Cyan / Pink** = Two roles:
1. Third-party content (customer quotes, partner integrations, external tool references, agent UI)
2. Color relief — on a slide that has no natural reason to use purple or orange, pink or blue can break visual monotony. Use sparingly.

**Green** = Positive outcomes, gains, improvements, success states

**Red** = Negative outcomes, risks, losses, failure/warning states

**Never**: Mix purple and orange on the same card/element without clear hierarchy

---

## Slide Dimensions (pptxgenjs inches, LAYOUT_16x9 = 10" x 5.625")

- Left/right margin: x=0.5, max content width: w=9.0
- Slide title: x=0.5, y=0.3, w=8.7, h=0.55
- Content area: y=1.05 to y=5.1
- Slide number: x=9.4, y=5.3, w=0.5, h=0.2

---

## Decorative Elements

### Accent line under section titles
A short colored bar (width: 40px, height: 4px, border-radius: 2px) placed immediately below the slide title on breaker slides. Color matches the slide theme (orange for general, purple for brand).

### Card style (pptxgenjs)
- Background: white (`FFFFFF`) or tinted color bg
- Border: color `E1DFEC`, lineSize 0.5
- Always use `rectRounded` shape with `rectRadius: 0.12` — never plain `rect`
- Shadow: not natively supported in pptxgenjs — rely on border for card separation

### Shapes and text boxes
- All rectangles, text boxes, and shape containers must use rounded corners
- Minimum border-radius: 8px for small elements, 12px for cards and panels
- In pptxgenjs: always set `rectRadius: 0.12` (or higher) on any `rectRounded` shape — never use plain `rect`

### Icon containers
- Circle or rounded-square background in the theme accent color (tinted version)
- Icon inside in the full accent color
- Size: 48×48px container, 24×24px icon

### Slide number
- Bottom-right of every slide
- Font: Inter 14px, color `#BD8FF7` (light purple)
- Format: just the number, e.g. `4`

### Elucidata logo mark
- A small colored diamond/hexagon shape in top-right corner of every slide
- Color: `8E42EE` (purple mid)
- In pptxgenjs: use a small `rectRounded` or `ellipse` shape, w=0.18, h=0.18, x=9.6, y=0.1

---

## Bundled Background Images

### Cover Slide — `assets/cover-bg.png`
- Full-bleed: dark purple deep-space hexagonal 3D art, Elucidata logo centered-right
- Text sits on the LEFT half where the background is dark — ensure contrast
- In pptxgenjs: `slide.addImage({ data: coverB64, x:0, y:0, w:10, h:5.625 })`

### Thank You Slide — `assets/thankyou-bg.png`
- Art fills the top ~65-70% of the slide; bottom ~30-35% is pure white
- In pptxgenjs: `slide.addImage({ data: tyB64, x:0, y:0, w:10, h:3.7 })`
- "Thank You!" text and contact sit in the white area below the image (y ~3.9 onward)
- "Thank" in Space Grotesk Bold 54px, `F78E12` orange + " You!" in `2A263F` dark — same text box using color runs
- Contact: `elucidata.io | info@elucidata.io`, Inter Regular 18px, `8E42EE`



## Text Emphasis Patterns

In slide titles, one word is often highlighted in a different color:
- "**Master** Template Guide" → "Master" in orange, rest in dark
- "**Brand** Theme" → "Brand" in orange
- "**Extended** Colour Library" → "Extended" in orange

This pattern: first word or key word of the title gets the accent color. Apply to content slides — not breaker slides (those use single-color titles).
