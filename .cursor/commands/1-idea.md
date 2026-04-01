# Stage 1 — Idea normalization

Follow **exactly** `ai-builder/system/prompts/1-idea.md` (role, rules, output format).

- Resolve `{{ARTIFACTS_PATH}}` as `ai-builder/project/artifacts` (see `pipeline.config.json`).
- Resolve `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from the same file; follow `ai-builder/system/rules/language-conventions.md`.
- Save the stage output to `ai-builder/project/artifacts/1-IDEA.md` when persisting artifacts.

The user provides the raw product idea in natural language in this chat.
