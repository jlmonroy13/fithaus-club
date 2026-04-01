# Stage 4a — Tech interview

Follow **exactly** `ai-builder/system/prompts/4a-tech-interview.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are defined in that prompt.
- Save the stage output to `ai-builder/project/artifacts/4A-TECH-PREFERENCES.md` when persisting artifacts.
