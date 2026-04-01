# Stage 7D — Plan ready (Backlog -> Ready)

Follow **exactly** `ai-builder/system/prompts/7d-plan-ready.md` (role, rules, readiness checks, output report).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are listed in that prompt.
- Run this stage after milestone publishing (`7c-publish-milestone-to-github-project`).
- Provide `github_project_url` as preferred runtime input.
- Use dry-run first, then run write mode.
