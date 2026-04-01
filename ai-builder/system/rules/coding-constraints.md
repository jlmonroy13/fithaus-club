# Coding Constraints

## Global Constraints

- Do not implement behavior that is not present in approved artifacts.
- Do not change architecture decisions without explicit approval.
- Prefer small, reversible changes per ticket.
- Keep implementation aligned with dependency order.

## Quality Gates (Required)

- Lint must pass.
- Type checks must pass.
- Build must pass.
- Relevant tests must pass.

If any gate fails, the ticket is not done.

## Scope Discipline

- Each ticket must solve one responsibility.
- Avoid cross-cutting refactors unless explicitly planned.
- Do not modify unrelated files.
- Record intentional deviations in ticket notes.

## API and Data

- Validate input at boundaries.
- Handle expected error states explicitly.
- Avoid silent failures.
- Keep contracts backward-compatible unless a breaking change is approved.

## Frontend

- Reuse existing components before creating new ones.
- Keep UI states explicit: loading, empty, error, success.
- Keep user-facing copy consistent with product language.

## Testing

- Add tests for new behavior.
- Update tests when behavior changes.
- Prefer deterministic tests.
- Include at least one behavior-level validation per ticket.

## AI Delivery Constraints

- Follow files and requirements defined in the AI task.
- Do not skip dependencies marked as blocking.
- Do not infer missing requirements; flag ambiguity instead.
