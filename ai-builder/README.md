# AI Product Builder

This repository contains a reusable AI-driven product pipeline.

## Structure

- `system/` → reusable prompts, templates, and rules
- `project/` → project-specific artifacts, UI assets, and context
- `pipeline.config.json` → source of truth for path variables and global language

## Path variables

Prompts and templates use variables such as:

- `{{ARTIFACTS_PATH}}`
- `{{SCREENSHOTS_PATH}}`
- `{{PROMPTS_PATH}}`
- `{{TEMPLATES_PATH}}`
- `{{RULES_PATH}}`
- `{{SYSTEM_PATH}}` (alias for the `system/` root: `ai-builder/system`)

This allows the pipeline to relocate the workspace root without rewriting internal references.

## Language variables

Also defined in `pipeline.config.json` (see `system/rules/language-conventions.md`):

- **`GENERATED_DOCS_LANGUAGE`** — Language for generated markdown artifacts and pipeline documentation (e.g. `Spanish`, `English`).
- **`IMPLEMENTATION_CODE_LANGUAGE`** — Language for code comments, docstrings, and implementation-time messages when running tickets (identifiers may remain English per stack norms).

Change these once for the whole pipeline; prompts and Cursor commands reference them.

## Resume
### 🧠 AI Product Pipeline — End-to-End Overview

#### 🎯 Purpose

This system defines a **deterministic pipeline** that transforms an idea into a publish-ready and implementation-ready delivery plan.

It replaces ambiguity with structure and enables:

* predictable outcomes
* scalable delivery
* continuous improvement

---

#### 🔗 High-Level Flow

```
Idea → Discovery → UI → System → Screens → Stories → Planning → Planning Export → Publish Milestone to GitHub Project → Plan Ready → Run Ticket Lifecycle
```

---

### 🟢 STAGE 1 — IDEA

#### Objective

Normalize and structure the raw idea into a clear starting point.

#### Input

* Free-form idea from the user

#### Output

`1-IDEA.md`

#### What it defines

* What the product is
* Who it is for
* What problem it solves

#### Success Criteria

* Clear and minimal
* No ambiguity in user or problem
* No extra features introduced

---

### 🔵 STAGE 2 — DISCOVERY

#### Objective

Convert the idea into a **complete product specification**

#### Input

`1-IDEA.md`

#### Output

`2-DISCOVERY.md`

#### What it defines

* User roles
* Core problem
* User flows
* Navigation
* UI structure
* Business rules
* Data model (high level)
* Out of scope

#### Success Criteria

* Fully deterministic
* No open decisions
* No feature invention
* Ready for system design

---

### 🟡 STAGE 3A — UI GENERATION

#### Objective

Explore UI using AI tools

#### Input

`2-DISCOVERY.md`

#### Output

`/ui/screenshots/`

#### What it produces

* Visual representations of the product

#### Notes

* This is exploratory
* Not a source of truth

---

### 🟡 STAGE 3B — UI VALIDATION

#### Objective

Extract useful structure from UI without trusting it blindly

#### Input

* `/ui/screenshots/`
* `2-DISCOVERY.md`

#### Output

`3B-UI-VALIDATION.md`

#### What it does

* Identifies UI patterns
* Validates layout consistency
* Ignores visual noise

---

### 🔴 STAGE 4A — TECH PREFERENCES

#### Objective

Capture developer constraints and preferences

#### Input

* `2-DISCOVERY.md`
* template file

#### Output

`4A-TECH-PREFERENCES.md`

#### What it defines

* Tech stack preferences
* Budget constraints
* Development priorities
* Team context

---

### 🔴 STAGE 4B — SYSTEM DESIGN

#### Objective

Design the system architecture

#### Input

* `2-DISCOVERY.md`
* `4A-TECH-PREFERENCES.md`
* optional UI validation

#### Output

`4-SYSTEM-DESIGN.md`

#### What it defines

* Data model
* APIs
* State management
* Tech stack
* Folder structure
* Key decisions

#### Success Criteria

* Fully aligned with discovery
* No overengineering
* Implementation-ready

---

### 🔴 STAGE 5 — SCREEN SPECS

#### Objective

Define behavior for every screen

#### Input

* `2-DISCOVERY.md`
* `4-SYSTEM-DESIGN.md`
* optional UI validation

#### Output

`5-SCREEN-SPECS.md`

#### What it defines

* Screens
* Data per screen
* Actions
* States
* Navigation

---

### 🔴 STAGE 6 — REFINED STORIES

#### Objective

Convert screens into executable user stories

#### Input

* Discovery
* System Design
* Screen Specs

#### Output

`6-REFINED-STORIES.md`

#### What it defines

* User stories
* Acceptance criteria
* Edge cases
* Dependencies

#### Success Criteria

* Small and testable
* No ambiguity
* Implementation-ready

---

### 🟠 STAGE 7 — PLANNING

#### Objective

Organize delivery

#### Input

`6-REFINED-STORIES.md`

#### Output

`7-PLANNING.md`

#### What it defines

* Milestones
* Delivery order
* Dependencies
* Logical grouping

#### Usage

* GitHub Projects
* Roadmap
* Task prioritization

---

### 🟠 STAGE 7B — PLANNING EXPORT

#### Objective

Convert planning markdown into a machine-readable export for deterministic automation.

#### Input

* `7-PLANNING.md`
* Kanban workflow and naming rules

#### Output

* `7-PLANNING.export.json`
* `7-PLANNING.export-report.md`

#### What it defines

* Parse-ready milestones and tickets
* Dependency validation results
* Publish-ready payload for GitHub Project automation

#### Usage

* Pre-flight validation before publishing and execution
* Structured input for milestone and issue publishing

---

### 🟠 STAGE 7C — PUBLISH MILESTONE TO GITHUB PROJECT

#### Objective

Publish one milestone at a time from planning export artifacts into GitHub Milestones, Issues, and Project items.

#### Input

* `7-PLANNING.export.json`
* `7-PLANNING.export-report.md`
* GitHub runtime configuration

#### Output

* GitHub milestone and issues created/updated
* Project items linked in Backlog
* Publish report summary

#### What it defines

* Planning-to-board synchronization
* Idempotent ticket publishing by `ticket_id`
* Baseline project field initialization

#### Usage

* Run after Stage 7B
* Use dry-run before write mode
* Publish only one milestone per run

---

### 🟠 STAGE 7D — PLAN READY

#### Objective

Evaluate Backlog tickets with dependency and DoR checks, then move eligible work to Ready.

#### Input

* `7-PLANNING.export.json`
* GitHub Project status and fields
* Kanban workflow rules

#### Output

* Ticket readiness decision report
* Project status transitions (`Backlog -> Ready` or `Backlog -> Blocked`)

#### Usage

* Run after Stage 7C publishing
* Use dry-run before write mode
* Execute before selecting the next ticket for implementation

---

### 🔥 STAGE 8 — RUN TICKET LIFECYCLE

#### Objective

Execute one Ready ticket end-to-end until PR is created and moved to In Review.

#### Input

* `4-SYSTEM-DESIGN.md`
* `7-PLANNING.md`
* `7-PLANNING.export.json`
* selected `ticket_id` in Ready

#### Output

`8-AI-TASKS-<ticket_id>.md`

#### What it defines

* Ticket-specific technical implementation brief
* Exact files to create or modify
* Verification commands and traceability updates

#### Usage

* Cursor implementation flow
* Single-ticket execution by `ticket_id`
* PR-ready development cycle with automatic status transitions

---

---

### 🧠 SYSTEM LAYERS

#### Product Layer

```
Stage 1 → Stage 2
```

#### UI Layer

```
Stage 3A → Stage 3B
```

#### System Layer

```
Stage 4A → Stage 4B
```

#### Delivery Layer

```
Stage 5 → 6 → 7 → 7B → 7C → 7D → 8
```

---

### 🔥 FINAL OUTCOME

At the end of the pipeline, you achieve:

#### ✅ A fully defined product

* No ambiguity
* Clear flows
* Clear constraints

#### ✅ A structured delivery plan

* Ordered tasks
* Dependencies resolved

#### ✅ Publish-ready planning artifacts

* Deterministic
* Context-aware
* Validatable

#### ✅ A controlled execution loop

* Dependency-aware progression
* Clear status transitions

---

### 🎯 IN ONE SENTENCE

> This system converts ideas into publish-ready and implementation-ready delivery plans using a structured and deterministic pipeline.

---

## Kanban Delivery Model (GitHub Project)

This repository includes an operational model to run Stage 7, Stage 7B, Stage 7C, Stage 7D, and Stage 8 outputs through a Kanban board.

### Source Mapping

- Stage 7 (`7-PLANNING.md`) -> GitHub milestones and tickets
- Stage 7B (`7-PLANNING.export.json`) -> publish-ready automation payload
- Stage 7C (publish run) -> creates/updates milestones and issues in GitHub Project
- Stage 7D (`plan ready`) -> readiness gate for Backlog to Ready transitions
- Stage 8 (`task run <ticket_id>`) -> single-ticket implementation lifecycle with PR and traceability updates

### Board Flow

`Backlog -> Ready -> In Progress -> In Review -> Done` (with optional `Blocked`)

### Governance Files

- `ai-builder/system/rules/kanban-workflow.md`
- `ai-builder/system/rules/naming-conventions.md`
- `ai-builder/system/rules/coding-constraints.md`
- `ai-builder/system/rules/spec-manifest.md`

### GitHub Templates

- `.github/ISSUE_TEMPLATE/ticket.md`
- `.github/pull_request_template.md`

Use these files as default process artifacts when running milestone-by-milestone delivery.

## Default Daily Execution

Use this sequence for day-to-day implementation:

1. `7d-plan-ready` to identify tickets that can move to Ready
2. `8-ai-execution` with a single `ticket_id` in Ready

The Stage 8 command enforces status transitions and documents technical work in project context files.

## How to Run the Full Process

Use this runbook to execute the pipeline from planning to ticket delivery in GitHub Project.

### Prerequisites

- Stage artifacts up to planning are available:
  - `2-DISCOVERY.md`
  - `4-SYSTEM-DESIGN.md`
  - `5-SCREEN-SPECS.md`
  - `6-REFINED-STORIES.md`
  - `7-PLANNING.md`
- GitHub CLI is authenticated (`gh auth login`).
- You have a GitHub Project URL.
- Board columns exist: `Backlog`, `Ready`, `In Progress`, `In Review`, `Done`, optional `Blocked`.

### Milestone Publish Flow (One Milestone at a Time)

1. Run `7b-planning-export`
   - Produces:
     - `7-PLANNING.export.json`
     - `7-PLANNING.export-report.md`
2. Run `7c-publish-milestone-to-github-project` in dry-run mode.
3. Review dry-run report for blockers.
4. Run `7c-publish-milestone-to-github-project` in write mode.
   - Publishes one milestone and its tickets into GitHub Project.
5. Run `7d-plan-ready` in dry-run mode.
6. Review proposed `Backlog -> Ready` and `Backlog -> Blocked` transitions.
7. Run `7d-plan-ready` in write mode.

### Ticket Execution Flow (Single Ticket)

1. Pick one ticket in `Ready`.
2. Run `8-ai-execution` with that `ticket_id` in dry-run mode.
3. Review planned code, status transitions, and traceability updates.
4. Run `8-ai-execution` in write mode.
   - Moves ticket to `In Progress`
   - Generates `8-AI-TASKS-<ticket_id>.md`
   - Implements code and runs quality gates
   - Creates branch, commit, push, and PR
   - Moves ticket to `In Review`
   - Updates technical traceability
5. Review the PR manually.
6. If changes are needed, push additional commits to the same PR.
7. Merge PR when approved.
8. Repeat from `7d-plan-ready` for the next ticket.

### Operating Rules

- Always use dry-run first for `7C`, `7D`, and `8`.
- Publish one milestone per run.
- Execute one ticket per Stage 8 run.
- Never move blocked tickets to `Ready`.
- Keep issue and context traceability updated on every delivered ticket.
