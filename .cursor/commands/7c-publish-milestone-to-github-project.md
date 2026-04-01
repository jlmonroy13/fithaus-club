# Stage 7C — Publish milestone to GitHub Project

Follow **exactly** `ai-builder/system/prompts/7c-publish-milestone-to-github-project.md` (role, rules, idempotency, output report).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are listed in that prompt.
- Run this stage only after `7b-planning-export`.
- Provide `github_project_url` as preferred runtime input.
- If URL is not provided, pass `project_owner` and `project_number`.
- Publish one milestone per run from:
  - `ai-builder/project/artifacts/7-PLANNING.export.json`
  - `ai-builder/project/artifacts/7-PLANNING.export-report.md`
- Use dry-run first, then run publish mode.
