# Elucidata AI Skills

Version-controlled Claude AI skills for Elucidata / Polly. These are plug-and-play skill packages that extend Claude with Elucidata-specific capabilities.

---

## Skills

### `elucidata-slides`

Creates Google Slides-compatible `.pptx` presentations that precisely follow the Elucidata / Polly brand system from the 2025 Master Template Guide.

**Trigger phrases:** "make me slides", "create a deck", "Elucidata presentation", "Polly slides", "build a deck"

**What's inside:**
- `SKILL.md` — core instructions and slide-building logic
- `references/brand-system.md` — Elucidata brand colors, typography, and visual rules
- `references/slide-layouts.md` — all supported slide layout specs
- `assets/` — cover and thank-you background images

---

### `concept-note-to-deck`

Converts a concept note, brief, or proposal into a branded Elucidata slide deck by matching it to the closest use case(s) in the Elucidata Use Case Compendium.

**Trigger phrases:** "turn this into a deck", "build slides from this concept", "create a use case presentation", "match this to a case study"

**What's inside:**
- `SKILL.md` — matching and deck-generation logic
- `references/use-case-compendium.md` — full Elucidata use case library
- `references/slide-formats.md` — slide structure templates for use case decks

---

## How to install a skill

Skills are loaded into Claude via the Cowork desktop app. Place the skill folder in your `.skills/skills/` directory and it will be available automatically in your next session.

---

## Contributing

To update a skill, edit the files in the relevant folder and push to `main`. Changes take effect the next time the skill is loaded in a session.
