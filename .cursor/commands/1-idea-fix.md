# COMMAND — STAGE 1 AUTO FIX

## Global language

Read `GENERATED_DOCS_LANGUAGE` and `IMPLEMENTATION_CODE_LANGUAGE` from `ai-builder/pipeline.config.json` and follow `ai-builder/system/rules/language-conventions.md`.

## Role

You are a senior product engineer and system corrector.

Your job is to FIX a failed Stage 1 Idea Brief using validation feedback.

You must correct the existing file — NOT regenerate it from scratch.

---

## Inputs

- Idea file:
  {{ARTIFACTS_PATH}}/1-IDEA.md

- Validation result (latest run):
  {{LAST_VALIDATION_OUTPUT}}

- Template reference:
  {{SYSTEM_PATH}}/templates/1-idea-template.md

- Original raw idea input:
  {{RAW_INPUT}}

---

## Objective

Fix ALL validation failures while:

- preserving valid sections
- preserving explicit user intent
- minimizing unnecessary changes

---

## Fixing Rules (CRITICAL)

### 1. Do NOT regenerate from scratch

- Modify ONLY what is broken
- Keep correct sections intact
- Preserve the existing structure unless the validation explicitly shows a structural failure

---

### 2. Preserve Explicit Content

- Do NOT remove or alter explicit user-provided information
- Do NOT simplify explicit business behavior
- Do NOT rewrite details into generic summaries

---

### 3. Apply Minimal Fixes

- Fix only what is required to pass validation
- Do NOT introduce new product scope
- Do NOT add arbitrary features
- Do NOT over-correct valid sections

---

### 4. Respect Template

- Ensure structure matches:
  `1-idea-template.md`
- Add missing sections if needed
- Do NOT remove required sections
- Do NOT add extra sections

---

### 5. Attribution Fix Rules

If attribution issues exist:

- Ensure EVERY section has Source Attribution
- Ensure every item is classified as one of:
  - Explicit
  - AI-Inferred
  - AI-Proposed
- Do NOT leave any content unclassified
- Correct misclassified items based on the validation feedback

Definitions:

- Explicit = directly provided by the user
- AI-Inferred = required logical extension of explicit input
- AI-Proposed = added only to complete missing structure

---

### 6. Target User Fix Rules

- Ensure EXACTLY ONE Primary user exists
- Ensure at most ONE Secondary user exists
- Preserve any extra roles from the source idea in:
  `Additional Roles Mentioned`
- Do NOT lose roles
- Do NOT invent roles
- Do NOT merge unrelated roles

---

### 7. Information Preservation Fix Rules

- Re-add any explicit details that were omitted
- Restore specific behaviors, constraints, flows, edge cases, or risks if they were lost
- Preserve wording close to the original input when possible

---

### 8. Scope Control Fix Rules

- Remove any content that incorrectly expands the scope
- Remove any AI-Proposed content that introduces unnecessary features
- Keep only minimal structure needed for reviewability

---

### 9. Completeness Fix Rules

- Ensure all sections are filled
- If a section truly lacks information, mark it as:
  - `Not specified`
  - or `None at this stage`
- Do NOT leave sections empty

---

### 10. Consistency Fix Rules

Ensure consistency between:

- Core Problem ↔ Product Goal
- Target User ↔ MVP Scope Summary
- Constraints ↔ Scope
- Source Attribution ↔ content origin

---

## Output

Rewrite the FULL corrected file:

{{ARTIFACTS_PATH}}/1-IDEA.md

---

## Final Instruction

Fix precisely.
Do not over-edit.
Preserve first.
Correct only what is necessary to pass validation.
