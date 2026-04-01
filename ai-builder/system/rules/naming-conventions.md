# Naming Conventions

## Artifact and Planning IDs

- Milestones: `M-01`, `M-02`, ...
- Stories: `ST-001`, `ST-002`, ...
- Tickets: `T-001`, `T-002`, ...
- AI Tasks: `TASK-001`, `TASK-002`, ...

Rules:

- IDs are immutable once assigned.
- IDs must be unique within a project.
- Dependencies must reference IDs, not free-text names.

## File Naming

- Markdown artifacts: uppercase stage names with stable file name:
  - `1-IDEA.md`
  - `2-DISCOVERY.md`
  - `4-SYSTEM-DESIGN.md`
  - `7-PLANNING.md`
- Source files: lowercase kebab-case for non-component files.
- UI components: PascalCase (`UserCard.tsx`).
- Utility modules: camelCase exports with kebab-case file names.

## Code Symbols

- Types and interfaces: PascalCase (`UserSession`, `CreateOrderInput`).
- Constants: UPPER_SNAKE_CASE for true constants.
- Variables and functions: camelCase.
- Enums: PascalCase enum name, UPPER_SNAKE_CASE members.

## Branch and PR Naming

- Branches: `<type>/<ticket-id>-<short-slug>`
  - Example: `feature/T-014-user-auth-flow`
- PR title: `[<ticket-id>] <short description>`
  - Example: `[T-014] Add login form validation`

## Label Naming (GitHub Project)

- `milestone:M-01`
- `type:feature|setup|bug|chore|test`
- `priority:P0|P1|P2`
- `area:frontend|backend|infra|data|qa`
