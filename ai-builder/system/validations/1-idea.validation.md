# STAGE 1 — IDEA VALIDATION CHECKLIST

## Global language (CRITICAL)

Expect narrative content in the language set by `GENERATED_DOCS_LANGUAGE` in `ai-builder/pipeline.config.json`. See `ai-builder/system/rules/language-conventions.md`.

## Structure Validation (CRITICAL)

- [ ] The output strictly follows the template: `1-idea-template.md`
- [ ] The artifact H1 is `# STAGE 1 — IDEA` (not the template file’s `IDEA TEMPLATE` title)
- [ ] No sections are missing
- [ ] No extra sections were added
- [ ] Section order is exactly preserved

---

## Content Completeness

- [ ] All sections are filled
- [ ] No section is empty
- [ ] Sections without input are explicitly marked as:
  - `Not specified`
  - or `None at this stage`

---

## Information Preservation (CRITICAL)

- [ ] ALL explicit user-provided information is present
- [ ] No explicit detail was removed, simplified, or generalized
- [ ] Specific behaviors (rules, flows, permissions, constraints) are preserved exactly
- [ ] Edge cases and unusual conditions are preserved

---

## Scope Control (CRITICAL)

- [ ] No features were added beyond:
  - explicit input
  - or strictly implied functionality
- [ ] No product scope expansion occurred
- [ ] No advanced or unnecessary features were introduced

---

## Implied vs Proposed Logic

- [ ] AI-Inferred content is used ONLY when required for explicit functionality
- [ ] AI-Proposed content is minimal and necessary
- [ ] AI-Proposed content does NOT introduce new product scope

---

## Target User Validation (CRITICAL)

- [ ] EXACTLY ONE Primary user is defined
- [ ] At most ONE Secondary user is defined
- [ ] Primary user represents the main value receiver
- [ ] Secondary user supports or enables the primary user

---

## Additional Roles Handling

- [ ] All additional roles mentioned in the input are preserved
- [ ] Additional roles appear ONLY in:
  - `Additional Roles Mentioned`
- [ ] No roles were lost or omitted
- [ ] No new roles were invented

---

## Attribution Integrity (CRITICAL)

- [ ] ALL sections are included in the Source Attribution section
- [ ] Every section has a classification
- [ ] Every item is classified as:
  - Explicit
  - AI-Inferred
  - AI-Proposed
- [ ] No content is left unclassified
- [ ] Classifications follow the defined rules correctly

---

## Wording Fidelity

- [ ] Original wording is preserved where possible
- [ ] No unnecessary abstraction or generalization occurred
- [ ] Specific details were not rewritten into vague language

---

## MVP Scope Validation (CRITICAL)

- [ ] All explicitly mentioned features are included
- [ ] All required functionality is present
- [ ] No optional or future features were introduced
- [ ] No relevant capability was omitted

---

## Out of Scope Validation

- [ ] Explicit exclusions are preserved
- [ ] No artificial exclusions were introduced

---

## Constraints & Risks

- [ ] All explicit constraints are preserved
- [ ] All explicit risks are preserved
- [ ] No constraints or risks were generalized or removed

---

## Information Pending Definition

- [ ] Includes ONLY:
  - explicitly undecided items
  - or decisions that cannot be safely inferred or proposed
- [ ] Does NOT include already resolved items

---

## Consistency Check (CRITICAL)

- [ ] No contradictions exist between sections
- [ ] Target users align with MVP scope
- [ ] Product goal aligns with the core problem
- [ ] Scope aligns with constraints and assumptions

---

## Final Validation Rule

- [ ] The output is:
  - structured
  - complete
  - faithful to the input
  - minimal but sufficient
  - ready for Stage 2 without ambiguity

---

## Failure Handling (CRITICAL)

If ANY of the following fail:

- Structure Validation
- Information Preservation
- Scope Control
- Target User Validation
- Attribution Integrity
- MVP Scope Validation
- Consistency Check

→ VALIDATION MUST FAIL

---

## Final Decision

- If ALL checks pass:
  → STAGE 1 VALIDATION PASSED — SAFE TO PROCEED

- If ANY critical check fails:
  → STAGE 1 VALIDATION FAILED — DO NOT PROCEED
