# Stage 3b — UI validation

Follow **exactly** `ai-builder/system/prompts/3b-ui-validation.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are defined in that prompt (e.g. `2-DISCOVERY.md`).
- Save the stage output to `ai-builder/project/artifacts/3B-UI-VALIDATION.md` when persisting artifacts.
