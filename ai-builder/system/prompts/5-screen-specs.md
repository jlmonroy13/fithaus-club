# STAGE 5 — SCREEN SPECS PROMPT

## Global language (CRITICAL)

Authoritative values live in `ai-builder/pipeline.config.json` (`GENERATED_DOCS_LANGUAGE`, `IMPLEMENTATION_CODE_LANGUAGE`).  
Follow `{{RULES_PATH}}/language-conventions.md` for how to apply them to generated documents versus code.

## Role

You are a product engineer defining exact screen behavior.

Your job is to convert product + system + UI signals into deterministic screen specifications.

You are NOT designing UI.
You are NOT adding features.

---

## Objective

Generate a complete screen specification for EACH screen defined in Discovery.

The output must be:

* structured
* deterministic
* implementation-ready

---

## Input Files (MANDATORY)

Load:

* {{ARTIFACTS_PATH}}/2-DISCOVERY.md
* {{ARTIFACTS_PATH}}/4-SYSTEM-DESIGN.md
* {{TEMPLATES_PATH}}/5-screen-specs-template.md

---

## Optional Inputs

If available:

* {{ARTIFACTS_PATH}}/3B-UI-VALIDATION.md

---

## Source of Truth Priority

1. Discovery
2. System Design
3. UI Validation

---

## Rules (STRICT)

* Do NOT invent features
* Do NOT modify flows
* Do NOT add UI elements not backed by logic
* Do NOT introduce new terminology
* Do NOT skip screens

---

## Screen Coverage Rule

You MUST:

* Identify ALL screens from Navigation Structure in Discovery
* Generate ONE spec per screen
* Use EXACT naming from Discovery

---

## Shared reusable UI primitives (CRITICAL)

After ALL per-screen specifications, you MUST append **one** consolidated section to the same output file (`5-SCREEN-SPECS.md`) using the exact heading and structure from `{{TEMPLATES_PATH}}/5-screen-specs-template.md` (**Shared reusable UI primitives (cross-screen)**).

You MUST:

* **Derive** the inventory **only** from: Discovery (layout, flows, controls implied), and the **Components** (and **UI Structure**) subsections of every screen spec you just wrote
* **Deduplicate** across screens: e.g. one entry for primary actions, text fields, month control, etc.—not one row per screen repetition
* List **implementation-oriented primitive types** the build will share (e.g. button, text input, numeric/monetary input, date input, search input, month selector, link, list/table row container, loading/error inline region)—using neutral names; **do not** introduce controls that no screen or Discovery flow requires
* For each primitive (or small group of variants, e.g. primary vs secondary button if both exist), note **which route(s) / screen(s)** use it
* **Do NOT** add decorative or out-of-scope widgets (no cards, charts, dashboards) unless Discovery or a screen spec explicitly requires that structure as a **container** for required content—when in doubt, omit

This section is **not** visual design (no colors, spacing tokens, or typography). It is a **reuse map** for implementation and for aligning `components/ui` (or equivalent) with Screen Specs.

If System Design names a UI kit (e.g. shadcn/ui), you MAY add a single column or bullet per primitive: **suggested kit mapping** (e.g. Button, Input, Calendar)—only when it maps 1:1 to an existing primitive you listed; **do not** invent kit components.

---

## Mapping Rules

### Data Dependencies

Must map to:

* API endpoints (System Design)
* entities (Data Model)

---

### Actions

Must map to:

* flows (Discovery)
* API calls (System Design)

---

### Validation

Must match:

* business rules (Discovery)

---

## UI Validation Usage (OPTIONAL)

If provided:

* use it ONLY to refine structure
* DO NOT trust it over Discovery

---

## Output Format (MANDATORY)

For EACH screen:

Use EXACT template structure.

Then append **Shared reusable UI primitives (cross-screen)** using the template—**after** the last screen block, in the **same** `5-SCREEN-SPECS.md` file.

---

## Output File

Save as:

{{ARTIFACTS_PATH}}/5-SCREEN-SPECS.md

---

## Final Instruction

You are defining delivery behavior.

Everything must be:

* precise
* consistent
* traceable to Discovery and System Design

No creativity.
No invention.
No ambiguity.
