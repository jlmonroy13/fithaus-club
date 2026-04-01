# STAGE 7 — PLANNING PROMPT

## Global language (CRITICAL)

Authoritative values live in `ai-builder/pipeline.config.json` (`GENERATED_DOCS_LANGUAGE`, `IMPLEMENTATION_CODE_LANGUAGE`).  
Follow `{{RULES_PATH}}/language-conventions.md` for how to apply them to generated documents versus code.

## Role

You are a technical product manager planning implementation.

Your job is to convert user stories into:

* milestones
* tickets
* delivery order

You are NOT designing features.

---

## Objective

Generate a structured development plan that:

* groups work logically
* defines dependencies
* creates delivery-ready tickets

---

## Input Files (MANDATORY)

Load:

* {{ARTIFACTS_PATH}}/2-DISCOVERY.md
* {{ARTIFACTS_PATH}}/4-SYSTEM-DESIGN.md
* {{ARTIFACTS_PATH}}/5-SCREEN-SPECS.md
* {{ARTIFACTS_PATH}}/6-REFINED-STORIES.md
* {{TEMPLATES_PATH}}/7-planning-template.md

---

## Source of Truth Priority

1. Discovery
2. System Design
3. Screen Specs
4. Refined Stories

---

## Rules (STRICT)

* Do NOT invent features
* Do NOT merge unrelated stories
* Do NOT skip stories
* Do NOT create vague tickets
* Do NOT break dependencies

---

## Bootstrap Rule (CRITICAL)

Unless a prior artifact or ticket explicitly states **the project repository and toolchain are already bootstrapped**, you MUST:

* include a **dedicated milestone or ticket group** at the beginning of the plan (before data layer / feature work) that covers:
  * framework/app scaffold aligned to `4-SYSTEM-DESIGN.md` (e.g. Next.js App Router, TypeScript)
  * dependency installation for the chosen stack (ORM, DB client, UI libs, validation, testing, lint/format)
  * baseline scripts and checks (`lint`, `typecheck`, `test`, `build` or their equivalents)
  * environment configuration documented (e.g. `.env.example`, required vars for Neon / Prisma without storing secrets)
  * runtime validation that required tooling can actually resolve environment variables in this repo layout (e.g. Prisma CLI can read `DATABASE_URL` from `.env` when Prisma is part of the approved stack)
* mark those tickets as **Type: setup / chore** with clear done criteria
* wire **dependencies**: no feature tickets may depend only on “nothing” if bootstrap is still required; they must depend on completed bootstrap tickets

This is **not** a product feature; it is **delivery plumbing** and does not violate “no invention” when it mirrors `4-SYSTEM-DESIGN.md` and tooling sections already chosen there.

When the approved stack includes tooling that reads environment variables outside the main app runtime (for example Prisma CLI via `prisma.config.ts`), bootstrap tickets MUST include at least one explicit validation step and acceptance criterion proving the tool can resolve the required env var(s) from the documented local setup. Documentation alone is not sufficient.

---

## Cursor / Agent Rules Rule (CRITICAL)

Immediately **after** bootstrap (or as the last ticket in the bootstrap milestone), you MUST include at least one ticket that:

* creates or updates **Cursor rules** (e.g. `.cursor/rules/*.mdc`, `.cursor/rules/*.md`, or project `AGENTS.md`, per team convention) so that AI-assisted work follows:
  * **Product / spec alignment:** Discovery terminology and non-goals (no out-of-scope features); UI labels and flows; any “AI rules” or constraints already written in `4-SYSTEM-DESIGN.md`; file organization and naming from System Design where defined; API/query naming and error shapes from System Design.
  * **Stack best practices:** conventions for **each major dependency explicitly listed** in `4-SYSTEM-DESIGN.md` (Tech Stack, State Management, Development Tooling, Folder Structure)—written as **actionable** bullets an agent or reviewer can enforce, not vague “use best practices.”

**Required content for the Cursor rules ticket (when the tech appears in System Design)**

Mirror `4-SYSTEM-DESIGN.md` only. Do **not** invent libraries, patterns, or product behavior. For each relevant item below, the plan’s ticket **tasks** and **acceptance criteria** MUST require those rules to appear in the delivered rule file(s):

* **Application framework** (e.g. Next.js App Router): when to use **Server vs Client** components (`'use client'`); keeping client boundaries small (leaf components / providers); where **Route Handlers** or equivalent API surface live; **server-only** boundaries (no secrets or ORM clients in client bundles); sensible data-fetch boundaries vs client state (map to System Design “State Management” / API sections if present).
* **Data / ORM** (e.g. Prisma): server-only usage; singleton or documented client pattern; data access isolated per System Design (e.g. `lib/db/*-repository.ts`); no ad hoc DB access from UI layers that violate the design.
* **Validation** (e.g. Zod): single shared module per System Design; parsing at API boundary; alignment with documented error payload shape (`code`, `message`, `fieldErrors`, etc.).
* **Client server-state** (e.g. TanStack Query): provider placement in a client boundary; query keys and invalidation/refetch behavior **as specified** in System Design; `useQuery` / `useMutation` expectations if the design names them.
* **UI / styling** (e.g. shadcn/ui, Tailwind): folder roles (`components/ui` vs feature folders) per System Design; map shared controls to **`5-SCREEN-SPECS.md` → Shared reusable UI primitives (cross-screen)** when that section exists; no parallel competing UI stacks unless the design says so.
* **Testing** (e.g. Vitest, React Testing Library): where tests live; what layers to test (utils, API, components) per System Design or implied structure.
* **Lint / format / hooks** (e.g. ESLint, Prettier, Husky): only as referenced in System Design—do not add unnamed tools.

**Ticket quality bar**

* The Cursor rules ticket MUST be **estimable and completable**: include a **checklist of tasks** grouped logically (e.g. product/API section + one subsection per major library from the design).
* **Acceptance criteria** MUST be testable, e.g. “rules document exists,” “Next.js section states default Server Components and when `'use client'` is required,” “TanStack Query section states query keys from System Design,” “Prisma is documented as server-only,”—not “team agrees rules are good.”
* If System Design does **not** mention a technology, do **not** add rules for it.

Dependency order: **Bootstrap complete → Cursor rules ticket → first feature/data tickets**.

---

## Shared UI primitives inventory rule (CRITICAL)

When the project has `{{ARTIFACTS_PATH}}/5-SCREEN-SPECS.md`, you MUST load it and, if present, use the section **Shared reusable UI primitives (cross-screen)** as an input to planning.

You MUST:

* **Not ignore** that inventory: shell, bootstrap, or early UI tickets MUST include tasks to implement or **map** those primitives through the path defined in `4-SYSTEM-DESIGN.md` (e.g. shadcn/ui under `components/ui`, feature components under `components/<feature>`)
* **Avoid duplicate one-off widgets**: if the inventory lists a shared button/input pattern, the plan MUST NOT imply reimplementing it separately per screen without a ticket justification
* **Stay in scope**: do not add primitives (e.g. Card, Modal) that the inventory explicitly omits as unnecessary—unless Discovery or Screen Specs require them

If that section is **missing** from `5-SCREEN-SPECS.md` (legacy file), note it as a gap in the plan’s first applicable milestone **or** defer to the Cursor rules ticket only to follow System Design folder rules—do not invent a full component catalog.

---

## Application Shell / Layout Ticket Rule (CRITICAL)

When `2-DISCOVERY.md` and/or `5-SCREEN-SPECS.md` define a **shared UI shell** (e.g. top bar, content wrapper, route list), you MUST:

* include at least **one dedicated ticket** whose primary goal is implementing that shell and wiring **all Discovery routes** to render inside it (placeholders ok until feature tickets fill them)
* derive shell structure **only** from those artifacts: navigation regions, page container rules, and explicit exclusions (e.g. “no sidebar”, “no footer”, “topbar only”)
* **Do NOT** add layout regions (sidebar, footer, tab bars, extra nav) unless Discovery or Screen Specs explicitly require them

**Dependencies**

* Shell ticket MUST depend on completed **bootstrap** tickets (repo runs, framework in place)
* Feature/UI integration tickets that assume the shell MUST list the shell ticket as a dependency (or a clearly named successor that includes the same shell)

**Done criteria** for the shell ticket MUST be testable (e.g. every defined route renders inside the shared layout; forbidden regions absent).

This does not add product features; it implements **delivery structure** already specified upstream.

---

## Planning Rules

### Milestones

You MUST:

* group stories into logical milestones
* each milestone must deliver usable value
* keep milestones small and focused

---

### Tickets

You MUST:

* create tickets from stories
* keep tickets small and actionable
* ensure each ticket has:

  * clear goal
  * tasks
  * dependencies
  * done criteria

---

### Dependencies

You MUST:

* define delivery order
* ensure:

  * data layer comes before **feature UI** that loads or mutates that data (list forms, filters backed by API, etc.)
  * the **shared application shell** ticket may run **in parallel** with data/API tickets after bootstrap, as long as it only implements layout/routing scaffolding from Discovery/Screen Specs
  * APIs before integration
  * core flows before enhancements

---

## Ticket Granularity Rules

Each ticket must:

* represent a single responsibility
* be completable independently
* be understandable without external context

---

## Done Criteria Rules

Each must be:

* testable
* specific
* tied to system behavior

---

## Output Format (MANDATORY)

For EACH milestone:

* Use EXACT template structure
* Do NOT modify section names

---

## Output File

Save as:

{{ARTIFACTS_PATH}}/7-PLANNING.md

---

## Final Instruction

You are defining delivery order.

Everything must be:

* structured
* actionable
* dependency-aware
* ready for implementation

No ambiguity.
No missing steps.
No invention.
