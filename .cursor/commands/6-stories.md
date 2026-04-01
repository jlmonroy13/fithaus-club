# Stage 6 — Refined stories

Follow **exactly** `ai-builder/system/prompts/6-stories.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are listed in that prompt.
- Save the stage output to `ai-builder/project/artifacts/6-REFINED-STORIES.md` when persisting artifacts.
