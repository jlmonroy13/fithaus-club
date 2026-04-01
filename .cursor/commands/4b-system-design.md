# Stage 4b — System design

Follow **exactly** `ai-builder/system/prompts/4b-system-design.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required inputs are listed in that prompt (discovery, tech preferences, optional UI validation).
- Save the stage output to `ai-builder/project/artifacts/4-SYSTEM-DESIGN.md` when persisting artifacts.
