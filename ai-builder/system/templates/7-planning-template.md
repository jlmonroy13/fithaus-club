# DEVELOPMENT PLAN

## Plan Metadata

- Plan ID: PLAN-001
- Project: <Project Name>
- Stage Link: Stage 7 (Planning) -> Stage 7B (Planning Export)
- Source Artifacts:
  - `2-DISCOVERY.md`
  - `4-SYSTEM-DESIGN.md`
  - `5-SCREEN-SPECS.md`
  - `6-REFINED-STORIES.md`
- Status: Draft | Approved

---

## Milestone: <Milestone Name>

### Milestone Metadata

- Milestone ID: M-01
- Target Outcome: <Business and technical outcome>
- Recommended Window: <Date range or sprint range>
- Entry Criteria:
  - <Condition required to start>
- Exit Criteria:
  - <Condition required to close>

---

### Goal

Describe the milestone outcome as user-visible value and implementation value.

---

### Scope

List included stories:

- ST-001 <Story title>
- ST-002 <Story title>
- ST-003 <Story title>

Out of scope:

- <Explicitly excluded work>

---

### Deliverables

Define what must be working at the end:

- <Deliverable 1>
- <Deliverable 2>
- <Deliverable 3>

---

### Tickets

#### Ticket: <Short title>

- Ticket ID: T-001
- Related Story: ST-001 <Story title>
- Priority: P0 | P1 | P2
- Estimate: XS | S | M | L
- Owner Role: Backend | Frontend | Fullstack | QA | DevOps
- Type: feature | setup | chore | bug | test

**Description**

Explain what needs to be implemented and why this ticket matters for milestone completion.

---

**Tasks**

- [ ] Task 1
- [ ] Task 2
- [ ] Task 3
- [ ] If the ticket documents required environment variables for approved tooling, add a concrete validation step proving the tool can resolve them in the repo setup.

---

**Dependencies**

- Depends on: T-000 or none
- Blocks: T-002, T-003 or none
- Blocked by external dependency: yes/no

---

**Acceptance Criteria**

- [ ] Criterion 1 (behavior-level and testable)
- [ ] Criterion 2 (behavior-level and testable)
- [ ] Criterion 3 (behavior-level and testable)
- [ ] If environment variables are part of the ticket scope, the relevant toolchain validation command succeeds using the documented local setup.

---

**Test Plan**

- Unit:
  - <What is validated>
- Integration:
  - <What is validated>
- E2E (if applicable):
  - <What is validated>
  - Include toolchain smoke checks when env-dependent tooling is in scope (for example `prisma validate` or equivalent).

---

**Done Criteria**

- [ ] Code implemented and reviewed
- [ ] Tests added and passing
- [ ] Lint/type/build checks passing
- [ ] Documentation/context updated if needed

---

### Dependencies

Milestone-level dependency graph:

- M-01 depends on: <none or other milestone IDs>
- Critical path tickets:
  - T-001 -> T-004 -> T-006

Delivery order notes:

- Data model and contracts before API integration
- API integration before UI workflow integration
- Core flow before enhancements

---

### GitHub Project Mapping

- Milestone Field: <Milestone name>
- Status Field: Todo | In Progress | Done
- Iteration Field: <Iteration/Sprint>
- Labels:
  - `milestone:<id>`
  - `type:<type>`
  - `priority:<priority>`
  - `area:<area>`

---

### Constraints

- Must follow Discovery
- Must follow System Design
- Must align with Screen Specs
- Must not introduce out-of-scope behavior
