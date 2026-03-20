---
name: concept-note-to-deck
description: >
  Converts a concept note into a branded Elucidata/Polly slide deck for internal team use — a
  first-draft working document to align on the solution approach and enable brainstorming. Deeply
  parses the concept note to understand the life sciences context, data environment, and problem
  nuances, then designs a solution using Polly's capabilities as building blocks assembled for the
  specific problem. Use this skill whenever a user provides a concept note, brief, or proposal and
  wants it turned into a slide deck — even if they don't explicitly say "use case" or "compendium".
  Also trigger when the user says things like "turn this into a deck", "build slides from this
  concept", "match this to a case study", or "create a use case presentation from this note".
  Always use the compendium reference file bundled with this skill to find matching cases. Never
  expose real customer or company names in any output.
---

# Concept Note → Elucidata Slide Deck (Internal Working Draft)

Converts a free-form concept note into a branded internal first-draft deck.

**Purpose**: Internal working document for team alignment and brainstorming. The solution is the hero — products are mentioned to show how the solution was built, not as the headline. The team reviews before any deck is produced.

**Two phases. Phase 1 ends with a team review checkpoint. Do not start Phase 2 until the user confirms.**

---

## Phase 1 — Understand, Research, Match, Plan, and Review

### Step 1 — Extract What You Can, Identify What's Missing

The input may not be a well-structured concept note. It could be a call transcript, a quick summary someone typed up after a discovery call, a few bullet points, a forwarded email, or a loosely written brief. That's fine. Your job is to extract signal from whatever format it arrives in.

**Read the input carefully and pull out everything you can infer, even indirectly.** A transcript where someone says "we're spending two weeks per study just cleaning metadata" tells you the data state, the modality type, and the friction cost — even if none of those were labeled explicitly. A call summary mentioning "their computational team is small" implies the end user and organizational constraint. Work with what's there.

Extract the following. For each field, note whether it is **stated**, **inferred**, or **missing**:

- **Lifecycle stage** — early discovery / target ID / preclinical / IND-enabling / clinical / regulatory / manufacturing / commercial
- **Org type** — large pharma / mid-size biotech / CDMO / academic lab / core facility / diagnostics / TechBio / CRO / AMC
- **End user** — who does the work day-to-day: bioinformatician / computational biologist / data scientist / bench scientist / regulatory team / IT / clinical ops
- **Organizational pressure** — what's driving this: pipeline decision / submission deadline / cost / scaling a capability / enabling a new modality
- **Data location** — public repos / in-house databases / instrument outputs / EHR / spreadsheets / documents / CRO deliveries
- **Data state** — raw / unharmonized / metadata-poor / scattered / locked in PDFs / mixed formats
- **Data modality** — bulk RNA-seq / scRNA-seq / proteomics / metabolomics / spatial biology / imaging / clinical-EHR / regulatory text / chemical-compound / manufacturing
- **Scale** — order of magnitude: samples, datasets, patients, records
- **Analysis needed** — what workflow or analysis they want to run
- **Definition of done** — what the output looks like when the problem is solved; what decision or action it enables
- **Friction and blockers** — every constraint mentioned or implied
- **Desired outcome / KPIs** — time, cost, accuracy, throughput, reproducibility, compliance
- **Regulatory context** — IND-enabling / GxP / clinical / FDA/EMA? Flag if present.

**After extraction, apply this decision rule:**

**Tier 1 — Blocking gaps** (cannot produce a useful deck without these): lifecycle stage, end user, definition of done. If any of these are missing AND cannot be reasonably inferred, stop and ask before proceeding.

**Tier 2 — Important but inferrable** (make a best guess, flag it clearly in the review document): org type, data modality, analysis needed, key blockers. If you infer these, state your assumption explicitly — the team can correct it during review.

**Tier 3 — Nice to have** (proceed without, note as unknown): exact scale, KPIs, regulatory specifics. Do not block on these.

**When asking questions**: ask only what you actually need from Tier 1. Group all questions into a single message. Do not ask about Tier 2 or 3 — infer and flag those instead. Fewer questions asked means faster review cycles and less friction for the user.

Example: if the input is a rough call transcript and you can infer it's a preclinical oncology biotech with a data harmonization problem but you can't tell who will actually use the output or what decision it feeds, ask only those two things in one message.

---

### Step 2 — Research the Domain

Run 2–3 web searches to understand the problem from the outside. You need this for a credible introduction slide and to sense-check the solution.

- What the broader scientific or industry community says about this challenge — is it a known bottleneck?
- What teams are doing today and why it's still a problem
- Domain-specific technical context if the note involves a specific disease, assay type, or regulatory pathway

Summarize in 4–6 sentences. Write like a practitioner explaining the problem, not a marketing opener.

---

### Step 3 — Match, Design, and Choose Format

Read [use-case-compendium.md](references/use-case-compendium.md), [polly-capabilities.md](references/polly-capabilities.md), and [voice-and-language.md](references/voice-and-language.md) together in this step.

**Compendium matching**
Match by problem type first, then domain, then data modality. Look for structural similarity — same kind of friction, same kind of output — not exact domain match. Select 1–3 cases. Extract only: solution approach, KPI benchmarks, transferable domain framing. Do not carry forward the full compendium. Never use any customer or company name in output — use generic framing ("a mid-size oncology biotech", "a global pharma translational team").

**Solution design**
Using the blockers from Step 1 and the capabilities table, assemble the solution:
- Map each blocker to the capability that addresses it
- Sequence the capabilities in the order the problem demands — there is no fixed pipeline
- For each step: what capability, what goes in, what comes out, why it's needed here
- Note explicitly where the solution generalizes beyond the specific modality or domain in the note
- Describe the final output concretely (e.g., "a harmonized atlas of 40+ scRNA-seq studies queryable by disease and cell type")
- Apply voice-and-language.md patterns throughout — product names in sub-labels, not headlines; step verbs; output labels at each stage

**Pipeline flowchart planning**
One slide must be a simple pipeline diagram. Plan it now:
- Left: data sources (separate public and in-house)
- Middle: capability steps in sequence with transformation labels (e.g., "Ontology harmonization", "Automated ingestion + QC")
- Right: final output state
- Sub-label each step with the Polly component name in smaller text
- Keep to 3–6 nodes. This maps to the Architecture / Data Flow slide.

**Impact framing**
- Use matched case metrics as directional benchmarks — label as "comparable engagements"
- Use "up to" / "typically" — never present borrowed numbers as confirmed for this customer
- Where no data exists, describe impact qualitatively: "eliminates the manual curation bottleneck", "makes this reproducible and auditable for the first time"

**Output format** (decide here, read only the relevant section of slide-formats.md)
- Concept note has concrete KPIs or outcome data → **Case Study** → read Format B
- Concept note is exploratory or forward-looking → **Use Case** → read Format A
- User asked for a one-pager → **One-pager** → read Format C

---

### Step 4 — Output the Review Document

**Steps 1, 2, and 3 run silently. Do not show working, intermediate outputs, extracted fields, search results, or compendium notes in the chat.** The only output is the review document below. Users should not need to read through reasoning to review — they should only see what requires a decision.

Write this in chat. This is the team checkpoint — do not start Phase 2 until the user confirms direction.

Format for scannability. Every section is a tight summary or bullets. No prose walls.

---

**REVIEW: [Title]**
`[Use Case / Case Study / One-pager]` | `[Lifecycle stage]` | `[Org type]`

---

**Use case articulation**
[2–4 sentences. Written for a knowledgeable life sciences audience — not a lay summary, not a marketing opener. Cover: what space this sits in scientifically or operationally, why it matters in the current R&D landscape, and what kind of team or program would encounter this challenge. This becomes the deck's introductory slide — it sets context before the problem is stated. Draw from Step 2 research and the concept note. Write it in Elucidata's voice: specific, practitioner-facing, no hype.]

**The problem in one sentence**
[Sharp, specific statement of the core business friction — what decision is being blocked or what cost is being paid]

**Why this matters**
- [Bullet: domain/industry context from research — 1–2 lines max each]
- [Bullet: what teams are doing today and why it fails]
- [Bullet: the consequence if it stays unsolved]

**What we understood from the note**
| Field | Value |
|---|---|
| Stage | [e.g., lead optimization / pre-IND] |
| End user | [e.g., computational biology + medicinal chemistry] |
| Data in | [e.g., in-house proteomics MS + public compound libraries] |
| Data state | [e.g., unharmonized instrument outputs; sparse paired data] |
| Analysis needed | [e.g., multimodal toxicity prediction across 4 organ endpoints] |
| Output | [e.g., compound-level toxicity scores with pathway annotations] |
| Regulatory context | [e.g., pre-IND, feeds pipeline go/no-go decisions] |
| Assumptions made | [anything inferred that the team should confirm] |

---

**The solution we're proposing**

[One sentence: what Elucidata builds and what it enables]

| Problem understood | Solution step | Output | Polly product |
|---|---|---|---|
| [Field from "what we understood" table — e.g., data state: unharmonized MS outputs] | [Verb + what we do — e.g., Ingest and preprocess raw instrument files] | [Concrete output — e.g., Standardized protein abundance matrix] | [e.g., Polly Ingest, Polly Pipelines] |
| [e.g., data in: public proteomics repos, quality unknown] | [e.g., Discover and QC-assess relevant public studies] | [e.g., Ranked, QC-scored study list] | [e.g., Polly Scout] |
| [e.g., data state: heterogeneous metadata across sources] | [e.g., Harmonize metadata against controlled ontologies] | [e.g., Linked, schema-consistent corpus] | [e.g., Polly Harmonize] |
| [e.g., analysis needed: multimodal model training] | [e.g., Build versioned paired training corpus] | [e.g., AI-ready, queryable atlas] | [e.g., Polly Atlas] |
| [e.g., analysis needed: toxicity prediction pipeline] | [e.g., Train and deploy multimodal model] | [e.g., Organ-specific toxicity scores + pathway annotations] | [e.g., Polly Pipelines, Polly Infrastructure] |
| [e.g., output: decision-support for medicinal chemistry] | [e.g., Deliver compound exploration interface] | [e.g., Scaffold-queryable toxicity dashboard] | [e.g., Polly Insights] |

Final output: [concrete, specific]
Generalizes to: [other modalities or domains]

---

**Compendium matches used**
- [Case name] — contributed [solution approach / KPI benchmarks / domain framing]

**Impact framing**
- [Metric or outcome] — [exact / directional (comparable engagements) / illustrative]

---

**Proposed slide structure**
1. Title / Cover
2. Use Case Articulation — [topic in 4 words, sets context before problem]
3. Introduction — [problem space framing]
4. Problem / Pain Point
5. Key Challenges
6. How We Solve It
7. Pipeline / Architecture
8. Impact / KPIs
[+ any additional slides with one-line justification]
N-1. Open Questions
N. Assumptions & Next Steps

---

**Flags for team discussion**
- [Flag 1: positioning, framing, or engagement-type question]
- [Flag 2: data or credibility gap that affects how a slide is written]
- [Flag 3: anything structurally ambiguous that needs a decision before the deck makes sense]

---

**[TEAM: Review the above and confirm, or tell me what to change. Once confirmed I'll build the deck.]**

---

## Slide Copy Rules

These rules apply to every slide in the deck and to all slide content described in the Step 4 review document. Violating these is a quality failure.

**Density**
- No prose paragraphs on slides. Exception: the Use Case Articulation slide (slide 2) uses 2–4 flowing sentences only.
- All other slides use bullet points or short labeled items only.
- Max 3–4 bullets per slide. If content requires more, split into two slides.
- Each bullet: max 10–12 words. Lead with the key fact, cut the rest.
- Callout stats (the large-number cards like "30%") count as one item and are encouraged — they replace a bullet, not add to it.

**Headlines**
- Slide title: 3–5 words. Active or noun phrase. No full sentences.
- Section sub-headers: same rule.

**"How We Solve It" steps**
- Step headline: verb + object, max 6 words. Example: "Harmonize metadata across all sources" ✓ / "We harmonize heterogeneous metadata from public and in-house sources against controlled ontologies" ✗
- Step description: one line max, input → output format. Example: "Raw MS files → standardized protein matrix per compound" ✓

**Problem and Challenge slides**
- Left column: 2–3 bullets max, each under 12 words
- Right column: one callout stat or one "Critical Issue" card with 2–3 lines
- No paragraph text on either side

**Pipeline / Architecture slide**
- Node labels only: 2–4 words per node
- Transformation arrows: 2–3 words max ("ontology mapping", "QC filter", "model training")
- No descriptive sentences inside nodes

**Review document (Step 4)**
- The solution table already enforces structure — keep entries tight, one line per cell
- Flags: one sentence each, max 20 words
- Impact framing: stat + source label only, no explanatory prose

---

## Phase 2 — Build the Deck

Start only after the user confirms the review document.

Do not re-read the compendium, polly-capabilities, slide-formats, voice-and-language, or the elucidata-slides SKILL.md. Everything needed is already in the confirmed review document. Carry forward only:
- The confirmed slide structure (list of slides and their layouts)
- The solution table (capability steps, outputs, Polly products)
- The use case articulation text
- The pipeline flowchart plan
- The impact metrics and their confidence labels
- The flags (for the last two slides)

Read `brand-system.md` and `slide-layouts.md` from `/mnt/skills/user/elucidata-slides/references/` only if you need to look up a specific token or layout spec you are not sure of. Do not read them by default.

Then follow the elucidata-slides workflow directly: write the full deck script in one pass, run once, one QA cycle, present.

**Slide copy**: Follow all rules in the Slide Copy Rules section above — density limits, bullet-only slides, short step headlines, one-line step descriptions. Products named in sub-labels, not headlines. Steps start with verbs. Outputs labeled at each stage.

**Use Case Articulation slide** (slide 2, always present): 2–4 sentences from the use case articulation in the review document. No bullet points — flowing paragraph, Title + Body layout. This is the deck's context-setter: it tells the audience what space this is in and why it matters before the problem is introduced. Tone: practitioner-to-practitioner, not a product pitch.

**Architecture / Data Flow slide**: Build as a pipeline diagram using the flowchart plan from Step 3. Left = data sources, middle = capability steps with transformation labels + Polly component sub-labels, right = final output. Use Numbers + Pointers layout or a simple left-to-right flow with arrow connectors. Keep it to 3–6 nodes.

**Flags slides (always include, always last two slides)**:

*Slide N-1 — Open Questions*
Each flag from the review document becomes a card. Format: flag title as card header (bold, orange accent), one-sentence description of what needs to be decided and why it matters for the deck. Use Column Comparison layout if 2–3 flags, Title + Body if more. These are honest gaps — do not soften or hide them.

*Slide N — Assumptions & Next Steps*
Two sections:
- Assumptions made: bullet list of everything inferred rather than stated — what the team should verify before this goes external
- Suggested next steps: 2–3 concrete actions (e.g., "Confirm proteomics MS pipeline experience with the delivery team", "Decide whether patient response prediction is in scope for this engagement", "Validate directional KPIs with a comparable closed deal")

---

## Key Rules

- **Slide copy must be sparse.** Bullet points and short items only. No prose paragraphs except on the Use Case Articulation slide. See Slide Copy Rules section for full constraints.
- **No real customer or company names.** Generic framing only: "a mid-size oncology biotech", "a global pharma translational team". Applies everywhere.
- **No fabricated customer names**, even fictional ones.
- **No invented KPIs.** Borrow directionally from matched cases (label "comparable engagements") or describe qualitatively.
- Regulatory framing (GxP, IND, FDA) must come from the concept note or be marked illustrative.
- Always use the elucidata-slides skill for PPTX. Never output HTML.
- The solution is the hero. Polly products are mentioned to show how it was built, not as the lead.
- One slide must be a pipeline/architecture diagram showing capability sequence and Polly components.
- Solution descriptions must be specific: name the capability and what it does in this context. "Polly can help with harmonization" is not acceptable. "Polly Harmonize standardizes metadata from 40+ heterogeneous proteomics studies against UniProt and controlled cell line ontologies, producing a linked, schema-consistent training corpus" is the right level.
- If lifecycle stage, end user, regulatory context, or definition of done is unclear — ask. Do not guess.
- Do not start Phase 2 without user confirmation on the review document.
