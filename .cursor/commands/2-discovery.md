# Stage 2 — Discovery

Follow **exactly** `ai-builder/system/prompts/2-discovery.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Required input includes `ai-builder/project/artifacts/1-IDEA.md`.
- Save the stage output to `ai-builder/project/artifacts/2-DISCOVERY.md` when persisting artifacts.
