# Kanban Workflow for Delivery

## Purpose

Define a deterministic delivery workflow that maps Stage 7 planning and Stage 7B export to GitHub Project operations.

## Board Columns

- Backlog
- Ready
- In Progress
- In Review
- Done
- Blocked

## Required Tracking Fields

- Priority (P0, P1, P2)
- Size (XS, S, M, L) on the GitHub Project board
- Ticket ID in issue title and issue body metadata
- Milestone ID in milestone title/label and issue body metadata
- Depends On in issue body metadata (comma-separated Ticket IDs)
- Blocked By in issue body metadata
- Story ID (optional, issue body metadata)

## Required Labels

- `type:feature|setup|chore|bug|test`
- `area:frontend|backend|infra|data|qa`
- `priority:P0|P1|P2`
- `milestone:M-xx`

## Definitions

### Definition of Ready (DoR)

A ticket can move from Backlog to Ready only when:

- All dependencies listed in the issue metadata `Depends On` are in Done.
- Acceptance criteria are explicit and testable.
- Scope is bounded to a single responsibility.
- No active external blocker exists.

### Definition of Done (DoD)

A ticket can move to Done only when:

- Behavior is implemented according to ticket scope.
- Lint, test, type-check, and build pass.
- Acceptance criteria are validated.
- Pull request is merged to `main`.
- Context documents are updated when applicable.

## State Transitions

- Backlog -> Ready: DoR satisfied.
- Ready -> In Progress: implementation starts (`task run <ticket_id>`).
- In Progress -> In Review: PR created (`task run <ticket_id>`).
- In Review -> Done: PR merged.
- Any -> Blocked: unresolved dependency or external blocker.
- In Review -> In Progress: review changes requested.

## Milestone Publishing Rule

- Publish one milestone at a time from Stage 7 output.
- Stage 7B export is required before publishing milestone data to GitHub Project.
- Do not publish next milestone until current milestone is closed, except explicit override.

## Operational Command Contract

### `plan sync`

- Input: `7-PLANNING.md` + current GitHub Project state.
- Output: consistency report (missing, duplicate, stale fields, dependency mismatch).

### `plan export`

- Input: `7-PLANNING.md` + rules.
- Behavior: parse and validate Stage 7 into machine-readable output.
- Output:
  - `7-PLANNING.export.json`
  - `7-PLANNING.export-report.md`

### `plan publish <milestone_id>`

- Input: `7-PLANNING.export.json` + GitHub runtime config.
- Behavior: create/update milestone, create/update issues, link issues to project.
- Output: publish report with created/updated/skipped operations.

### `plan ready`

- Input: tickets in Backlog and Blocked.
- Behavior: evaluate DoR and dependency state using Stage 7 export plus GitHub Project status, including reevaluating Blocked tickets whose blockers may now be resolved.
- Output: move eligible tickets to Ready with reason log; move blocked or still-blocked tickets to Blocked with reason; leave non-ready tickets in Backlog.

### `task run <ticket_id>`

- Input: one ticket ID currently in Ready.
- Behavior: execute single-ticket lifecycle from Ready to In Review, including:
  - technical brief generation
  - implementation
  - branch/commit/push/PR
- Precondition: `plan export` completed without blocking validation errors.
- Required updates:
  - project status transitions
  - issue technical summary comment
  - `context/progress.md` update
  - `context/decisions.md` update when design decisions were made

### `task verify <ticket_id>`

- Input: ticket in In Review or Done.
- Behavior: validate DoD and detect required updates for future tasks or context artifacts.

### `milestone close <milestone_id>`

- Input: milestone identifier.
- Behavior: verify all milestone tickets are Done and produce closure summary.
