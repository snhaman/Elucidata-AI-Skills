# Elucidata Slide Formats — Compendium-Derived Templates

These formats are derived directly from the Case Study / Use Case Compendium (2025 Master Deck).
Use them to map concept note content to the correct slide structure before building the PPTX.

---

## Format A: Use Case Format

Used for: Prospect-facing decks, solution demos, early-stage proposals.
Characteristics: Solution-forward, lighter customer framing, emphasis on Polly capability and architecture.

### Slide Order

**Slide 1 — Title / Hook Slide**
- Large use case title (e.g., "Advancing Target ID & Validation in AML")
- One-line outcome statement below (e.g., "Elucidata helped a Boston-based therapeutics company ID & validate 2 targets in 6 months")
- Minimal — no logos or company names unless explicitly provided

**Slide 2 — Problem / Pain Point**
- Brief narrative paragraph: who the customer is, what they're trying to do, what's blocking them
- May include a "Critical Business Issue" callout box (orange or purple accent)
- Keep to 3–5 sentences max

**Slide 3 — Solution Architecture / How We Helped**
- Numbered list (1–4 steps) of what Elucidata did
- OR a workflow/pipeline diagram showing data flow from input to output
- Polly component labels where relevant (Polly Atlas, Polly Harmonize, Polly Scout, Polly Insights, Polly KG)

**Slide 4 — Architecture Detail (if relevant)**
- Data flow diagram: Public Data + In-house Data → Processing stages → Output/Atlas
- Label each stage (Metadata harmonization, ETL, Human-in-loop QC, etc.)
- Show output (AI-ready dataset, KG, ranked gene list, etc.)

**Slide 5 — Impact / Results**
- 2–4 large metric callouts (stat boxes in orange or green)
- Before/after framing where possible ("X months → Y months", "X hrs → Y hrs")
- Short supporting text below each metric

**Slide 6 (Optional) — Quick Demo / Quick Peek**
- Screenshot placeholder or "Demo" label
- Brief 1–2 sentence description of what the demo shows

---

## Format B: Case Study Format

Used for: Validated wins, customer evidence, sales enablement, detailed proposals.
Characteristics: Evidence-led, customer-specific (named or anonymized), metric-heavy. Includes a dedicated framing slide.

### Slide Order

**Slide 1 — Title / Hook**
- Case study title (e.g., "Optimizing CHO Cell Line Productivity Using Multi-Omics Insights")
- One-line summary of the outcome

**Slide 2 — Company / Pain Point / Approach (3-column card slide)**
Three cards side by side:
- **Company**: Who they are, their focus area, scale
- **Pain Point**: What specific problem they faced
- **Approach**: What Elucidata delivered at a high level

Also includes:
- **Critical Business Issue** box: often a quote from a customer stakeholder (Director, VP R&D, etc.) describing the problem
- **Key Challenges**: 3–4 bullet points listing specific blockers

**Slide 3 — How We Helped**
- Numbered steps (1–4), each describing a specific action Elucidata took
- Specific and technical — name the Polly component used
- May be combined with an architecture diagram

**Slide 4 — Architecture / Data Pipeline**
- Visual representation of data flow
- Show: input sources (public + in-house), processing stages, output
- Label Polly platform components explicitly

**Slide 5 — KPIs & Impact**
- Bold metric callouts: cost savings, time reduction, sample throughput, accuracy %
- Source: ideally from the customer. If not confirmed, label as "illustrative" or "directional"
- May include a before/after timeline visual

**Slide 6 (Optional) — Demo / Quick Peek**
- Screenshot or placeholder for product demo
- Brief caption

**Slide 7 (Optional) — Additional Evidence Slide**
- Secondary metric or technical detail that adds credibility
- E.g., methodology details, data scale, accuracy benchmarks

---

## Format C: One-Pager Format

Used for: Quick leave-behinds, compact sales materials, reference cards.
Characteristics: Single dense slide with all information. Heavy use of small cards.

### Single Slide Layout (all sections on one slide)

**Top Section (2 columns):**
- Left column: Company, Pain Point, Approach (stacked, small card format)
- Right column: Critical Business Issue (quote callout in orange/purple box)

**Middle Section:**
- Key Challenges: 3–4 bullet points (small, tight)
- How We Helped: Numbered list (1–5 steps), concise

**Bottom Section:**
- KPIs & Impact: 3–4 metric callouts in a horizontal row
- Use green stat boxes or orange callout chips

**General rules for one-pagers:**
- Font sizes must be smaller — body text at 10–12pt equivalent to fit everything
- No full-bleed images or diagrams — text-only with accent color chips
- Every section must be present — no optional slides

---

## Slide Content Mapping Guide

Use this table to pull content from the concept note and matched case study:

| Slide Section | Source: Concept Note | Source: Matched Case |
|---|---|---|
| Customer description | Who the prospect/customer is | Anonymized framing template |
| Pain Point | Problem statement from note | "Critical Business Issue" framing |
| Key Challenges | Specific blockers mentioned in note | Challenge bullets from matched case |
| Solution approach | Proposed Polly capability | "How We Helped" steps from matched case |
| Architecture | Solution hint in note | Architecture diagram logic from matched case |
| KPIs | Specific metrics if stated | Matched case metrics (label as directional if borrowed) |
| Critical Business Issue quote | Paraphrase from note if possible | Stakeholder role from matched case (e.g., "Director, R&D") |

---

## Common Polly Component Labels (use these consistently)

- **Polly Scout** — AI-assisted dataset discovery across 50+ public databases
- **Polly Harmonize** — Metadata harmonization, ETL, and standardization engine
- **Polly Atlas** — Domain-specific repository of analysis-ready data
- **Polly Insights** — Notebooks, apps, and visualization tools for data consumption
- **Polly KG** — Multi-modal Knowledge Graph for reasoning across biological entities
- **Polly Co-Scientist** — Conversational AI research assistant (AML-focused use cases)
- **Polly Ingest** — Automated ingestion pipeline from machines or external sources

---

## KPI Treatment Rules

1. **Exact**: Use when the concept note or matched case has confirmed customer data — use as-is
2. **Directional**: Use when borrowing from a matched case — prefix with "up to", "as much as", or "typically"
3. **Illustrative**: Use when no real data exists — add a footnote "(illustrative)" or "(based on comparable engagements)"

Never present illustrative numbers as confirmed outcomes.
