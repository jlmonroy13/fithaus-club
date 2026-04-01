# Global language conventions

Authoritative settings live in `ai-builder/pipeline.config.json` at the repository root:

- **`GENERATED_DOCS_LANGUAGE`** — Natural language for pipeline outputs (markdown artifacts, filled templates, validation narratives, planning/story text, and other generated documentation).
- **`IMPLEMENTATION_CODE_LANGUAGE`** — Natural language for **implementation work**: source comments, docstrings, developer-facing error messages, commit messages, and PR descriptions when executing tickets. Identifier and API names stay conventional for the stack (often English); user-visible product copy follows Discovery unless stated otherwise.

## How to apply

1. Read the current values from `pipeline.config.json` before generating or reviewing content.
2. If a value is a locale name (e.g. `Spanish`, `English`), use that language consistently for the scope above.
3. Do **not** mix languages within a single artifact or PR unless the product specification explicitly requires it (e.g. bilingual UI).
4. Template **structure** (headings, section order) must still match the template files; translate section **titles** only when the template is authored for localization or when the pipeline explicitly allows localized headings.

## Examples

| Setting | Applies to |
|--------|------------|
| `GENERATED_DOCS_LANGUAGE` | `1-IDEA.md`, `2-DISCOVERY.md`, stage outputs under `{{ARTIFACTS_PATH}}`, exported planning JSON reports’ human-readable fields where generated |
| `IMPLEMENTATION_CODE_LANGUAGE` | Code comments, `@param` docs, implementation notes in repos, ticket execution outputs under Stage 8 |

When in doubt, prefer the configured language over the language of the prompt file (prompts may be written in English for tooling while artifacts follow `GENERATED_DOCS_LANGUAGE`).
