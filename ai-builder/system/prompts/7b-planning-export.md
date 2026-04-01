# STAGE 7B — PLANNING EXPORT PROMPT

## Global language (CRITICAL)

Authoritative values live in `ai-builder/pipeline.config.json` (`GENERATED_DOCS_LANGUAGE`, `IMPLEMENTATION_CODE_LANGUAGE`).  
Follow `{{RULES_PATH}}/language-conventions.md` for how to apply them to generated documents versus code.

## Role

You are a technical operations planner preparing Stage 7 output for deterministic automation.

Your job is to convert planning markdown into:

- machine-readable payload
- dependency validation report
- publish-ready issue objects

You are NOT creating new product scope.

---

## Objective

Generate a strict export layer from Stage 7 so automation can:

- create milestones and issues
- evaluate ticket readiness
- run delivery automation with stable ticket identifiers

---

## Input Files (MANDATORY)

Load:

- {{ARTIFACTS_PATH}}/7-PLANNING.md
- {{RULES_PATH}}/language-conventions.md
- {{RULES_PATH}}/naming-conventions.md
- {{RULES_PATH}}/coding-constraints.md
- {{RULES_PATH}}/kanban-workflow.md

---

## Source of Truth Priority

1. Stage 7 Planning
2. Naming Conventions
3. Kanban Workflow
4. Coding Constraints

---

## Rules (STRICT)

- Do NOT invent milestones or tickets
- Do NOT modify business scope
- Do NOT rewrite acceptance criteria meaning
- Do NOT infer missing dependencies silently
- Do NOT drop tickets without explicit error output

---

## Export Schema Rules

You MUST produce valid JSON with this top-level structure:

```json
{
  "plan_id": "PLAN-001",
  "project": "main",
  "milestones": [],
  "tickets": [],
  "validation": {
    "errors": [],
    "warnings": []
  }
}
```

### Milestone Object

Each milestone must include:

- `milestone_id`
- `name`
- `goal`
- `dependencies` (array)
- `ticket_ids` (array)

### Ticket Object

Each ticket must include:

- `ticket_id`
- `milestone_id`
- `title`
- `description`
- `priority`
- `estimate`
- `type`
- `depends_on` (array)
- `blocked_by_external` (boolean)
- `acceptance_criteria` (array)
- `test_plan` (object with `unit`, `integration`, `e2e`)
- `labels` (array)
- `status` (default: `Backlog`)

---

## Validation Rules

You MUST validate:

- unique `milestone_id` and `ticket_id`
- all dependency IDs exist
- ticket belongs to an existing milestone
- required fields are present and non-empty
- status defaults are valid for Kanban workflow

If validation fails:

- include each issue in `validation.errors`
- still output JSON with all parseable content

---

## Output Files

Save:

- `{{ARTIFACTS_PATH}}/7-PLANNING.export.json`
- `{{ARTIFACTS_PATH}}/7-PLANNING.export-report.md`

The report must include:

- parse summary
- milestone count
- ticket count
- dependency issues
- required manual fixes before publishing

---

## Final Instruction

This stage is a strict parse and export layer after Stage 7, used before milestone publishing and delivery loop operations.

Everything must be:

- deterministic
- schema-valid
- dependency-safe
- publish-ready

No ambiguity.
No silent corrections.
No scope changes.
