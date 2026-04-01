# Stage 8 — Run ticket lifecycle

Follow **exactly** `ai-builder/system/prompts/8-ai-execution.md` (single-ticket lifecycle, status transitions, quality gates, traceability updates).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are listed in that prompt.
- Run this stage after `7d-plan-ready`.
- Provide a single `ticket_id` currently in Ready.
- Use planning export artifacts as machine-readable reference:
  - `ai-builder/project/artifacts/7-PLANNING.export.json`
  - `ai-builder/project/artifacts/7-PLANNING.export-report.md`
- Persist ticket technical brief as:
  - `ai-builder/project/artifacts/8-AI-TASKS-<ticket_id>.md`
- Use dry-run first, then run write mode.
