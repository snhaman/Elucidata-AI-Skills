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

**Option 1 — Via the Cowork Customize panel (recommended for most people)**

1. Download or clone this repo to your computer.
2. Open the Claude desktop app and go to **Cowork → Customize**.
3. In the **Skills** section, click **Add skill** (or the `+` button).
4. When prompted, select the skill folder you want to add (e.g. `elucidata-slides` or `concept-note-to-deck`). The folder must contain a `SKILL.md` file at its root.
5. The skill will appear in your skills list and be active immediately in your next Cowork session.
6. Repeat for each skill you want to install.

**Option 2 — Manual file placement**

Place the skill folder directly into your `.skills/skills/` directory (the folder Claude watches for skills). It will be picked up automatically on the next session start. No restart needed if Cowork is already running — just start a new conversation.

---

## Contributing

To update a skill, edit the files in the relevant folder and push to `main`. Changes take effect the next time the skill is loaded in a session.
