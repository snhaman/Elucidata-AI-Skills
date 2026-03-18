---
name: concept-note-to-deck
description: >
  Converts a concept note into a branded Elucidata/Polly slide deck by matching the note's problem
  and intent to the closest use case(s) in the Elucidata Use Case Compendium, then generating a
  properly formatted deck using the elucidata-slides skill. Use this skill whenever a user provides
  a concept note, brief, or proposal and wants it turned into a slide deck — even if they don't
  explicitly say "use case" or "compendium". Also trigger when the user says things like "turn this
  into a deck", "build slides from this concept", "match this to a case study", or "create a use
  case presentation from this note". Always use the compendium reference file bundled with this
  skill to find matching cases.
---

# Concept Note → Elucidata Slide Deck

Converts a free-form concept note into a branded use case or case study deck.

**This skill runs in two phases to stay within context limits. Complete Phase 1 fully before loading anything for Phase 2.**

---

## Phase 1 — Parse, Match, and Plan

Do all of the following before reading elucidata-slides or any brand files.

### Step 1 — Parse the Concept Note

Extract these fields. If any are missing, infer from context or mark as unknown — don't block on user input unless the note is completely unintelligible.

- **Problem statement**: What pain is the customer or prospect facing?
- **Domain / vertical**: Pharma, diagnostics, CDMO, academic core facility, TechBio, etc.
- **Data types**: omics, EHR, imaging, literature, regulatory docs, etc.
- **Solution hint**: What Polly capability is implied? (data harmonization, KG, GenAI automation, pipelines, data platform)
- **Desired outcome / KPIs**: Time savings, cost reduction, accuracy, throughput, etc.
- **Regulatory context**: IND-enabling, GxP, pre-clinical, clinical? Flag if yes.

---

### Step 2 — Match to the Compendium

Read [use-case-compendium.md](references/use-case-compendium.md) now.

Use this matching priority:
1. Problem type first (e.g., "fragmented omics data" → data harmonization cases)
2. Domain / vertical
3. Solution type (KG, pipeline, GenAI, data platform, LLM retrieval)
4. Data modality (single-cell, bulk RNA-seq, EHR, imaging, regulatory docs)

Select 1–3 cases. If mixing cases, note which case contributed what. Do not hallucinate cases — only use entries that exist in the compendium.

**After matching: you no longer need the full compendium in active context. Extract only what you need from the matched cases (title, solution steps, KPIs, domain framing) and carry those forward as a compact notes block.**

---

### Step 3 — Decide the Output Format

Based on the concept note content alone — do not load slide-formats.md yet:

- Concept note has concrete KPIs or outcome data → **Case Study format**
- Concept note is exploratory or forward-looking → **Use Case format**
- User explicitly asked for a one-pager → **One-pager format**

Then read only the relevant format section from [slide-formats.md](references/slide-formats.md):
- Use Case format → read "Format A" section only
- Case Study format → read "Format B" section only
- One-pager → read "Format C" section only

---

### Step 4 — Write the Deck Brief

Before touching elucidata-slides, write a compact structured brief in this format. This brief is what drives deck generation — keep it tight:

```
DECK BRIEF
----------
Title: [use case or case study title]
Format: [Use Case / Case Study / One-pager]
Matched case(s): [case name(s) from compendium]

SLIDES
------
[For each slide, one block:]

Slide N — [Slide Type]
Content: [2–5 bullet points of actual content, not instructions]
Layout hint: [card / stat callout / numbered list / diagram / narrative paragraph]
KPI treatment: [exact / directional / illustrative]

MATCHING RATIONALE (brief, for chat output only — not in deck)
--------------------------------------------------------------
Problem: [one sentence]
Why this match: [2–3 sentences]
What was adapted: [concept note vs. compendium contributions]
```

Write this brief in the chat before proceeding. It is your working document for Phase 2.

---

## Phase 2 — Build the Deck

Only start Phase 2 after the Deck Brief is written.

Read `/mnt/skills/user/elucidata-slides/SKILL.md` and follow it fully.

Pass the Deck Brief as the input — use it as the slide-by-slide content spec. Do not re-read the compendium or slide-formats during this phase.

**Slides to always include** (in this order):
1. Title / cover — use case name, one-line hook
2. Problem / Pain Point — customer situation, critical business issue
3. Key Challenges — 3–4 bullet challenges (card layout)
4. How We Helped / Solution — Polly capability walkthrough (workflow or step layout)
5. Architecture / Process — data flow or pipeline diagram if relevant
6. KPI / Impact — metric callouts (green stat boxes), before/after if possible
7. (Optional) Demo or Quick Peek — only if matched case has a demo reference
8. (Optional) One additional evidence slide — only if it adds weight

Do not add slides not justified by the concept note or matched cases.

---

## Key Rules

- Never fabricate a customer name. Use anonymized framing ("A US-based pharma company...") unless the concept note explicitly names the customer.
- Never invent KPIs. Use numbers from the concept note or matched cases only. If neither exists, use directional language ("up to 3x faster") and mark as illustrative.
- Regulatory framing (GxP, IND, FDA) must come from the concept note or be clearly marked as illustrative.
- Always use the elucidata-slides skill for the final PPTX. Never output HTML.
- If the concept note covers a domain not well represented in the compendium, pick the structurally closest case (same solution type) and note the gap in the matching rationale.
- The deck should feel like it came from the compendium — not like a generic AI-generated output.
