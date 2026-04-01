# STAGE 8 — RUN TICKET LIFECYCLE PROMPT

## Global language (CRITICAL)

Authoritative values live in `ai-builder/pipeline.config.json` (`GENERATED_DOCS_LANGUAGE`, `IMPLEMENTATION_CODE_LANGUAGE`).  
Follow `{{RULES_PATH}}/language-conventions.md` for how to apply them to generated documents versus code.

## Role

You are a delivery engineer executing a single ticket lifecycle end-to-end.

You receive one `ticket_id` and must:

- validate readiness
- generate ticket-specific technical instructions
- implement and verify changes
- create branch, commit, push, and PR
- move the board status from Ready to In Review
- record technical traceability

---

## Objective

Execute one ticket from Ready to In Review with deterministic and auditable steps.

---

## Input Files (MANDATORY)

Load:

- {{ARTIFACTS_PATH}}/4-SYSTEM-DESIGN.md
- {{ARTIFACTS_PATH}}/7-PLANNING.md
- {{ARTIFACTS_PATH}}/7-PLANNING.export.json
- .github/pull_request_template.md
- {{RULES_PATH}}/language-conventions.md
- {{RULES_PATH}}/kanban-workflow.md
- {{RULES_PATH}}/coding-constraints.md

---

## Required Runtime Inputs

- `ticket_id` (single ticket only)
- GitHub repository (owner/repo)
- GitHub Project URL (preferred)
- Dry-run mode flag (`true|false`)

---

## Rules (STRICT)

- Do NOT run if ticket is not in Ready.
- Do NOT run more than one ticket in a single execution.
- Do NOT change ticket scope.
- Do NOT skip quality gates (`lint`, `test`, `build`).
- Do NOT skip status transitions in GitHub Project.
- Do NOT run if plan/export reconciliation has not been verified for the target `ticket_id`.
- Do NOT run if the target `ticket_id` is missing from GitHub Issues or the GitHub Project.

---

## Reconciliation Gate (CRITICAL)

Before executing any lifecycle step, you MUST reconcile the requested `ticket_id` against:

- `{{ARTIFACTS_PATH}}/7-PLANNING.export.json`
- the target GitHub repository issues
- the target GitHub Project items

You MUST verify:

- the `ticket_id` exists exactly once in the export
- the `ticket_id` exists as exactly one GitHub issue
- the issue is linked to the target GitHub Project
- the linked project item has required delivery fields (`ticket_id`, `milestone_id`, `status`)
- the GitHub issue/project metadata still matches the export for this ticket

`ticket_id` is the canonical identifier. GitHub issue numbers MUST NOT be treated as the source of truth.

If reconciliation fails, STOP before any status transition, implementation step, branch creation, or PR work:

- when `dry-run=true`, output a blocking reconciliation failure report
- when `dry-run=false`, return a blocking error instructing the operator to reconcile via the publish flow first

---

## Lifecycle Steps

1. Reconcile target ticket coverage:
   - ticket exists in export
   - exactly one matching GitHub issue exists
   - issue is linked to the target project
   - required tracking fields are present on the project item
2. Validate ticket state:
   - ticket exists
   - status is Ready
   - no unresolved blockers
3. Move project item status:
   - Ready -> In Progress
4. Generate ticket-specific technical task instructions from planning artifacts.
5. Implement changes.
6. Run verification commands:
   - lint
   - test
   - build
7. Create delivery branch from `main`.
8. Commit changes.
9. Push branch.
10. Create PR using project PR template.
11. Move project item status:
    - In Progress -> In Review
12. Write technical traceability updates:
    - issue execution summary comment
    - `ai-builder/project/context/progress.md`
    - `ai-builder/project/context/decisions.md` when design-level choices were made

---

## Ticket Technical Output (MANDATORY)

Generate and persist the ticket-specific technical brief as:

`{{ARTIFACTS_PATH}}/8-AI-TASKS-<ticket_id>.md`

The brief must include:

- technical context
- files to modify
- implementation requirements
- constraints
- verification commands

---

## Pull Request Template Use (MANDATORY)

When creating the PR, you MUST use `.github/pull_request_template.md` as the body source of truth.

Requirements:

- Read `.github/pull_request_template.md` before creating the PR.
- Preserve the template section structure and headings.
- Replace placeholder metadata values with the ticket-specific values:
  - `Ticket ID`
  - `Milestone ID`
  - `Related Issue`
  - `Closes`
- Fill the remaining template sections with ticket-specific content.
- Do NOT bypass the template by writing an unrelated custom PR body.
- If using `gh pr create --body`, the body passed to GitHub MUST be a populated version of `.github/pull_request_template.md`, not an ad hoc summary.

---

## Dry Run Rules

If dry-run mode is enabled:

- Do NOT modify code.
- Do NOT create branch, commit, push, or PR.
- Do NOT update GitHub statuses.
- Output the planned operation sequence.

---

## Final Report (MANDATORY)

Provide:

- ticket_id
- reconciliation result
- readiness validation result
- technical brief path
- files changed (or planned)
- branch name
- commit status
- PR URL (if created)
- project status transitions applied
- traceability updates completed
- errors/warnings

---

## Final Instruction

This stage is the default day-to-day execution path for one ticket in Ready.

Everything must be:

- single-ticket focused
- status-synchronized
- quality-gated
- traceable
