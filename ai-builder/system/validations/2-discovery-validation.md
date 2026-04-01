# STAGE 2 — DISCOVERY VALIDATION CHECKLIST (FINAL)

## Global language (CRITICAL)

Expect narrative content in the language set by `GENERATED_DOCS_LANGUAGE` in `ai-builder/pipeline.config.json`.
See `ai-builder/system/rules/language-conventions.md`.

---

## Structure (CRITICAL)

- [ ] Matches template exactly
- [ ] Artifact H1 is `# STAGE 2 — DISCOVERY`
- [ ] No sections missing
- [ ] No extra sections present
- [ ] Section order matches template

---

## Coverage (CRITICAL)

- [ ] All explicit information from Stage 1 is preserved
- [ ] No explicit rules, constraints, or flows were dropped

---

## Roles (CRITICAL)

- [ ] Primary user exists
- [ ] No more than 4 roles total
- [ ] Additional roles preserved
- [ ] No roles were invented

---

## Flows (CRITICAL)

- [ ] Between 1 and 5 active flows
- [ ] Unused flows marked "Not used"
- [ ] Flows represent capabilities (NOT UI steps)
- [ ] No UI actions in steps (e.g. "click", "navigate")

---

## Navigation (CRITICAL)

- [ ] Routes represent logical entry points
- [ ] No routes created for UI components (modals, states)
- [ ] Each route has a clear purpose
- [ ] Routes align with flows

---

## Data Model (CRITICAL)

- [ ] All entities include:
  - Description
  - Key fields
  - Lifecycle (yes/no)
  - Mutable (yes/no)
- [ ] Relationships are defined
- [ ] Entities align with flows and business rules

---

## Business Rules (CRITICAL)

- [ ] All rules include a valid type:
  - validation
  - state
  - calculation
  - permission
- [ ] Rules are clear and unambiguous
- [ ] Rules align with flows and data model

---

## UX Constraints (CRITICAL)

- [ ] UX constraints describe user needs, NOT UI solutions
- [ ] No UI instructions (e.g. "use modal", "use sidebar")
- [ ] Constraints are aligned with product behavior

---

## UI Leakage (CRITICAL)

- [ ] No UI-specific actions in flows (click, open, navigate)
- [ ] No UI-specific decisions in layout (modal, sidebar enforced)
- [ ] No component-level instructions
- [ ] Layout descriptions are high-level only

---

## Terminology (CRITICAL)

- [ ] Terms are system-level (not UI labels)
- [ ] Definitions are clear and consistent
- [ ] No UI-specific wording in terminology

---

## Consistency (CRITICAL)

- [ ] Flows ↔ Roles aligned
- [ ] Flows ↔ Navigation aligned
- [ ] Flows ↔ Data Model aligned
- [ ] Business Rules ↔ Data Model aligned

---

## Traceability

- [ ] Key Decisions documented
- [ ] Key Assumptions present
- [ ] Known Constraints present
- [ ] Open Questions present
- [ ] System Boundaries defined

---

## Scope (CRITICAL)

- [ ] No new features introduced
- [ ] No scope expansion beyond Stage 1

---

## Final Rule

If ANY critical check fails → FAIL
If ALL critical checks pass → PASS
