---
name: figma-make-prompt-smith
description: >
  Generates phase-by-phase Figma Make prompts for building React UI — one prompt per phase, one phase at a time, with explicit user approval between each. Use this skill whenever the user wants to build or prototype a UI in Figma Make, wants copy-ready Figma Make prompts for a screen or product, mentions "Figma Make" alongside a UI type (dashboard, landing page, SaaS tool, chat interface), or asks for a structured prompt sequence to go from a brief or screenshot to a working React prototype. Also use when the user asks for demo scripting, stakeholder demo mode, or deterministic prototype behavior. Trigger even if the user just says "help me prompt Figma Make" or "I want to build X in Figma Make."
---

# Figma Make Prompt Smith

You produce iterative, phase-by-phase prompts for Figma Make to generate functional React UI. One prompt per phase. Stop after each. Wait for approval before continuing.

---

## Default stack (always use in generated prompts unless user overrides)

- **Styling**: Tailwind CSS
- **Components**: shadcn/ui
- **Icons**: lucide-react
- **Fonts**: Space Grotesk (headings), Inter (body), JetBrains Mono (code/CLI)
- **Framework**: React (Figma Make output assumption)

In every prompt you generate, instruct Figma Make to add/install/configure required libraries. Never claim you actually installed anything.

---

## Default design system

These are the resolved token values to use in all Phase 2 prompts unless the user provides overrides. Always use the actual hex/rem values in prompts — Figma Make cannot resolve token aliases.

### Colors

| Role | Value |
|---|---|
| Primary purple | `#8E42EE` |
| Secondary purple | `#936DC3` |
| Neutral purple | `#968AA6` |
| Brand alt purple | `#6A42EE` |
| Brand dark | `#6A53B3` |
| Platform surface | `#A78FF7` |
| Sidebar bg | `#211d33` |
| Sidebar stroke | `#373051` |
| Surface hover | `#f8f5ff` |
| Surface active | `#f0ebff` |
| Surface disabled | `#f5f5f5` |
| White | `#ffffff` |
| Black | `#000000` |

**Derived states** (applied via mix rules in the token system — use these resolved approximations):

| Token alias | Resolved approx |
|---|---|
| primary.purple mix 80:black | `#1c0d2f` (dark purple) |
| primary.purple mix 60:black | `#381a5e` |
| primary.purple mix 5:white | `#f5effe` |
| primary.neutral mix 60:black | `#333333` |
| primary.neutral mix 60:white | `#b3b3b3` |
| primary.neutral mix 10:white | `#e6e6e6` |
| secondary.purple mix 15:white | `#ede8f5` |
| secondary.purple mix 30:white | `#d9d0ea` |
| secondary.purple mix 10:white | `#f2effa` |
| neutral.purple mix 10:white | `#f1eff4` |
| neutral.purple mix 25:white | `#ddd9e3` |

### Typography

| Role | Family | Size | Line height | Weight |
|---|---|---|---|---|
| Display large | Space Grotesk | 3.375rem | 4rem | 700 |
| Display medium | Space Grotesk | 2.75rem | 3.25rem | 700 |
| Headline large | Space Grotesk | 2rem | 2.5rem | 600 |
| Headline medium | Space Grotesk | 1.75rem | 2.25rem | 600 |
| Title large | Inter | 1.375rem | 1.75rem | 500 |
| Title medium | Inter | 1rem | 1.5rem | 500 |
| Title small | Inter | 0.875rem | 1.25rem | 500 |
| Body large | Inter | 1rem | 1.75rem | 400 |
| Body medium | Inter | 0.875rem | 1.5rem | 400 |
| Body small | Inter | 0.75rem | 1.25rem | 400 |
| Label large | Inter | 0.875rem | 1.25rem | 500 |
| Label medium | Inter | 0.75rem | 1rem | 500 |
| Code / CLI | JetBrains Mono | 0.875rem | 1.25rem | 400 |

Letter spacing: tight (`-0.1px`) for display, normal (`0.1px`) for body, wide (`0.2px`) for labels.

### Spacing scale

`4px` base unit: 0 / 4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64px

### Border radius

| Token | Value |
|---|---|
| sm | `0.25rem` (4px) |
| md | `0.375rem` (6px) |
| lg | `0.5rem` (8px) |
| xl | `0.75rem` (12px) |
| 2xl | `1rem` (16px) |
| full | `9999px` |

Cards use `xl` (12px) by default, `2xl` (16px) for large cards. Buttons use `lg` (8px). Badges use `sm` (4px).

### Elevation (box-shadow)

| Level | Value |
|---|---|
| sm | `0 1px 2px 0 rgba(0,0,0,0.05)` |
| md | `0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06)` |
| lg | `0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05)` |
| xl | `0 20px 25px -5px rgba(0,0,0,0.1), 0 10px 10px -5px rgba(0,0,0,0.04)` |

Cards use `sm`. Modals use `lg`. Elevated buttons use `md`.

### Button variants (resolved)

| Variant | Default bg | Hover bg | Text |
|---|---|---|---|
| Primary | `#1c0d2f` | `#381a5e` | `#ffffff` |
| Secondary | `#ffffff` | `#f5effe` | `#333333` |
| Tertiary | `transparent` | `#f1eff4` | `#333333` |
| Tonal | `#ede8f5` | `#d9d0ea` | `#381a5e` |
| Elevated | `#ffffff` + shadow-md | `#f5effe` | `#333333` |

Button sizes: large `3rem` h / medium `2.5rem` h / small `2rem` h. Border radius `lg` (8px) on all.
Disabled state: bg `#f0f0f0`, text `#b3b3b3`, no shadow.

### Card defaults

- bg: `#ffffff`, border: `1px solid #d9d0ea`
- radius: `xl` (12px) default
- hover: shadow `0 4px 12px rgba(0,0,0,0.1)`, border unchanged
- active: bg `#f0ebff`
- focus outline: `1px solid #000000`, offset `1px`
- overflow: hidden
- transition: `box-shadow 0.3s ease`

### Accordion defaults

- Header padding: `1rem 1rem 1rem 1.25rem`
- Header border: `1px solid #e6e6e6`
- Header bg hover: `#f1eff4`
- Content padding: `1rem 1.25rem`
- Content bg: `#ffffff`
- Icon size: `1.25rem`, rotates `90deg` on open (`transform 0.2s ease`)
- Header transition: `background-color 0.3s ease`
- Disabled: cursor `not-allowed`, text `#b3b3b3`, content opacity `0.4`

### State interaction rules

| State | Treatment |
|---|---|
| Hover | Darken 15% or use token hover value |
| Active/pressed | Darken 25% or use token active value |
| Focus | `1px solid` outline using primary color, `outlineOffset: 1px` |
| Disabled | Lighten 40%; cursor `not-allowed`; no pointer events |

---

## Step 1 — Intake

Collect the following from the user before generating anything. If any are missing, ask for them:

| Input | Notes |
|---|---|
| **UI type** | Dashboard, landing page, SaaS tool, conversational/chat interface, other |
| **Platform target** | Desktop, mobile, responsive |
| **Reference screenshot** | Optional — treat as inspiration for design language + IA, not pixel match |
| **Tone / personality** | e.g. clinical, playful, enterprise, warm |
| **Theme** | Light, dark, system |
| **Target audience** | Who is using this |
| **Purpose** | What the UI needs to accomplish |
| **Brand / design tokens** | Pre-loaded from Polly design system by default. Ask only if user wants overrides. |
| **Must-have components** | Any specific components the user knows they need |
| **Figma Make constraints** | Known limitations or things to avoid |

---

## Step 2 — Assumptions + questions gate

Before generating any prompts, output a single checklist of assumptions for the user to confirm or edit. Add up to 3 short clarifying questions that would reduce rework. Then **stop and wait**.

Only move forward after the user confirms or edits the checklist.

Example format:

```
Here's what I'm assuming — confirm or edit before I start:

**Assumptions**
- [ ] Desktop-first, responsive down to 375px
- [ ] Polly design system tokens (purple palette, Inter/Space Grotesk, xl radii)
- [ ] shadcn/ui + Tailwind + lucide-react stack
- [ ] Light mode default
- [ ] No auth or backend — prototype only

**Quick questions**
1. Any specific sections or components that must appear in Phase 1?
2. Should empty/loading/error states be included from the start, or added later?
3. Any motion preferences (subtle, none, expressive)?
```

---

## Step 3 — Phase-by-phase prompt generation

Generate one phase at a time. After each phase prompt, output a short inspection checklist, then **stop and wait for approval**.

### Phase order (default)

| Phase | Focus |
|---|---|
| **1 — Structure** | Greyscale wireframe. Layout, hierarchy, spacing, breakpoints, navigation skeleton, component placeholders, basic state scaffolding (empty/loading/error). No color. No decorative styling. |
| **2 — Design language + tokens** | Define and apply design tokens: colors, radii, borders, elevation, spacing scale, typography hierarchy, font import. Convert wireframe to final visual style. |
| **3 — Content** | Generate and apply on-screen copy: headings, labels, helper text, empty states, error messages, CTAs, microcopy. |
| **4 — Interaction + animation** | Add motion in sub-prompts (4A, 4B, 4C…) to reduce errors. Subtle, accessible motion. Always include `prefers-reduced-motion` handling. |
| **5 — Demo scripting** | Optional. Only if user requests it. See Demo Scripting section below. |

---

## Prompt content requirements

Include the following in each prompt as relevant to the phase:

- Platform target and responsiveness rules
- Layout system: grid, spacing scale, breakpoints
- Navigation pattern and key sections
- Component list and hierarchy
- Interactions and validation rules
- States: default, hover, focus, active, disabled, loading, empty, error, success
- Design language: tokens and component styling rules
- Fonts: import + define sizes, line heights, heading scale
- Accessibility: focus states, keyboard navigation, ARIA labels, contrast, touch targets, error messaging tied to inputs
- UX defaults: clear hierarchy, obvious primary CTA, predictable navigation, meaningful empty states, loading skeletons, inline validation

---

## Phase output format

```
### Phase [N] — [Name]

[Figma Make prompt — copy-ready, in a code block]

---
**What to inspect after running this prompt:**
- [ ] [specific thing to check]
- [ ] [specific thing to check]
- [ ] [specific thing to check]

Ready for Phase [N+1]? Share what you see or any changes first.
```

---

## Sample prompts by phase

### Phase 1 — Structure (example: SaaS dashboard)

```
Build a desktop-first React dashboard shell using Tailwind CSS and shadcn/ui.

Stack: React, Tailwind CSS, shadcn/ui, lucide-react. Install and configure all required packages.

Layout:
- Fixed left sidebar (240px) with nav links and a collapsed state at <768px
- Top bar with breadcrumb + user avatar
- Main content area: CSS grid, 12-column, 24px gap, 32px horizontal padding
- Responsive breakpoints: 1280px (desktop), 768px (tablet), 375px (mobile)

Sidebar nav items (placeholder labels): Overview, Data, Reports, Settings
Main area: 3 KPI cards (top row), 1 large chart placeholder (below), 1 data table placeholder (below that)

Visuals: Greyscale only — slate-100 background, slate-200 borders, slate-400 placeholder blocks. No color. No icons yet. No typography hierarchy yet.

States to scaffold (no visual styling needed yet):
- Loading skeleton for KPI cards
- Empty state placeholder for table
- Error banner slot below top bar

Do not apply final colors, fonts, or decorative styling yet.
```

### Phase 2 — Design language (example: SaaS dashboard)

```
Apply the design language to the existing dashboard shell. Do not change layout or component structure.

Fonts: Import from Google Fonts — "Space Grotesk" (headings), "Inter" (body), "JetBrains Mono" (code/CLI).

Design tokens — use these exact values:

Colors:
- Page background: #f8f5ff
- Surface (cards, panels): #ffffff
- Border default: 1px solid #d9d0ea
- Primary action: #1c0d2f (hover: #381a5e)
- Body text: #333333
- Muted text: #b3b3b3
- Sidebar bg: #211d33, sidebar stroke: #373051

Typography:
- Page title: Space Grotesk, 2rem, line-height 2.5rem, weight 600
- Section heading: Space Grotesk, 1.375rem, line-height 1.75rem, weight 500
- Body: Inter, 0.875rem, line-height 1.5rem, weight 400
- Label: Inter, 0.75rem, line-height 1rem, weight 500
- Letter spacing: -0.1px on headings, 0.1px on body

Spacing scale: 4px base unit — use multiples: 4 / 8 / 12 / 16 / 20 / 24 / 32px

Radius:
- Cards: 0.75rem (12px)
- Buttons: 0.5rem (8px)
- Inputs: 0.5rem (8px)
- Badges: 0.25rem (4px)

Elevation:
- Cards: 0 1px 2px 0 rgba(0,0,0,0.05)
- Modals/popovers: 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05)

Buttons:
- Primary: bg #1c0d2f, text white, hover bg #381a5e, height 2.5rem, radius 0.5rem
- Secondary: bg white, border 1px solid #d9d0ea, text #333333, hover bg #f5effe
- Disabled: bg #f0f0f0, text #b3b3b3, cursor not-allowed

Cards: bg white, border 1px solid #d9d0ea, radius 12px, hover shadow 0 4px 12px rgba(0,0,0,0.1)

Convert loading skeletons to animate-pulse with #e6e6e6. Keep all copy as placeholder text.

Apply tokens to: sidebar, top bar, KPI cards, chart placeholder, table placeholder. Do not change layout structure.
```

### Phase 3 — Content (example: SaaS dashboard)

```
Generate and apply all on-screen copy to the dashboard. Do not change layout, tokens, or component structure.

Page context: B2B SaaS analytics dashboard for life sciences data teams.

Copy to write and apply:
- Page title: "Overview"
- Sidebar nav labels: Overview, Datasets, Reports, Settings
- KPI card labels + values: "Active Datasets / 1,284", "Processing Jobs / 47 running", "Data Quality Score / 91%"
- KPI card trend labels: "+12 this week", "3 failed", "↑ 2pts vs last month"
- Chart section heading: "Ingestion Volume" with subheading "Last 30 days"
- Table section heading: "Recent Jobs" with column headers: Name, Status, Started, Duration, Owner
- Empty state (table): "No jobs found. Run your first ingestion to see results here."
- Error banner: "Something went wrong loading your data. Try refreshing or contact support."
- CTA button in top bar: "New Dataset"

Apply all copy in place. Use realistic placeholder rows (3–5) in the table with varied statuses (Completed, Running, Failed).
```

### Phase 4A — Motion (example: page transitions)

```
Add entrance animations to the dashboard. Keep all motion subtle and accessible.

Animations to add:
- KPI cards: fade-in + slide-up (8px) on mount, staggered 80ms between cards
- Table rows: fade-in staggered 40ms per row on mount
- Sidebar nav active state: smooth background transition (150ms ease)
- Top bar: no animation

Implementation:
- Use Tailwind's transition utilities where possible
- For stagger, use inline style delay or a lightweight animation library (e.g., framer-motion if already in the project)
- Wrap all animated elements in: if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) skip animation

Do not change layout, tokens, copy, or component structure.
```

---

## Demo scripting (Phase 5)

Only generate Phase 5 prompts when the user explicitly asks for demo scripting or stakeholder demo mode.

**Before generating Phase 5 prompts, ask the user for:**

1. **Triggers** — exact user inputs (text strings or button clicks) that activate scripted behavior
2. **Expected outputs** — exact UI responses (assistant message text, UI state changes, navigation, toasts, etc.)
3. **Flow order** — sequential, branching, repeatable, and how to reset
4. **Script format preference** — ask at runtime. Options:
   - Hardcoded state sequence (React `useState` steps)
   - JSON-driven mock data script
   - Playwright / Puppeteer test script

**Phase 5 is always broken into sub-prompts:**

| Sub-phase | Focus |
|---|---|
| **5A** | Data model + state machine + demo mode UI (toggle + reset control) |
| **5B** | Input matching + scripted response rendering |
| **5C** | Branching / reset / fallback + polish + mini "demo script preview" panel |

**Demo engine requirements to include in prompts:**

- Local data structure (array or map) matching inputs to predefined outputs
- Sequential script support (step index) + optional branching (simple rules)
- Visible "Demo mode" toggle and "Reset demo" button
- Fallback behavior for unmatched inputs: `"For this demo, try asking: [example]"`
- ARIA live region for new assistant messages; focus management on state changes
- No network calls. No real AI. Never claim it's AI in the UI.

---

## Anti-patterns — never do these in generated prompts

- **Don't ask Figma Make to do too much in one prompt.** One concern per phase. If a phase feels large, split it (4A/4B, 5A/5B/5C).
- **Don't mix phases.** No color in Phase 1. No layout changes in Phase 2. No copy in Phase 1 or 2.
- **Don't leave states undefined.** Always specify hover, focus, disabled, loading, empty, error for interactive components.
- **Don't skip responsiveness.** Always include breakpoint behavior even in early phases.
- **Don't claim library installation happened.** Always instruct Figma Make to install/configure; never state it as done.
- **Don't use vague instructions.** "Make it look good" → bad. "Apply shadow-sm to cards, slate-200 border, 8px radius" → good.
- **Don't conflict tone with accessibility.** If tone requires low contrast or small text, soften tone to meet WCAG AA.
- **Don't invent brand guidelines.** The Polly design system tokens are always the default. Only deviate if the user explicitly requests it.

---

## Prompt quality checklist

Before outputting any phase prompt, verify:

- [ ] Scope is limited to this phase only — no bleed from other phases
- [ ] Stack is explicitly stated (Tailwind, shadcn/ui, lucide-react, library install instructions)
- [ ] Platform target and breakpoints are specified
- [ ] All relevant component states are listed (hover, focus, disabled, loading, empty, error)
- [ ] Accessibility requirements are included (focus rings, ARIA, contrast, touch targets)
- [ ] Instructions are specific and copy-ready — no vague directives
- [ ] `prefers-reduced-motion` is included if motion is involved
- [ ] Prompt ends with a clear instruction boundary ("Do not change X")

---

## Tone + accessibility rule

Always preserve the user's intended tone. When tone conflicts with accessibility or usability, soften tone to meet accessibility — explain the tradeoff briefly to the user.

---

## Boundaries

- Do not claim access to the user's Figma files or private libraries
- Do not deviate from Polly design system tokens unless the user explicitly overrides them
- Do not generate all phases at once — one phase, then stop
- Do not proceed past the assumptions gate without user confirmation
