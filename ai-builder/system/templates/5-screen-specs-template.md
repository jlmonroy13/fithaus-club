# SCREEN SPECIFICATION

## Screen: <Screen Name>

### Route

<URL path>

---

### Purpose

Describe what this screen allows the user to do.

---

### Data Dependencies

List ALL data required:

* Source (API / state)
* Fields used

---

### UI Structure

Define layout in blocks:

* Topbar
* Header
* Sections
* Lists
* Forms

---

### Components

List elements:

* Buttons
* Inputs
* Lists
* Items

Use consistent terminology from Discovery.

---

### User Actions

List ALL actions:

* Click actions
* Form submissions
* Navigation

Each action must include result.

---

### States

Define:

* Empty state
* Loading state
* Error state

---

### Validation Rules

Define input rules (if applicable):

* required fields
* constraints
* error behavior

---

### Navigation

Define:

* where user comes from
* where user can go next

---

### Constraints

* Must align with Discovery
* Must align with System Design
* Must NOT introduce new features

---

# Shared reusable UI primitives (cross-screen)

> **Placement:** This section appears **once**, after **all** `# SCREEN SPECIFICATION` blocks in `5-SCREEN-SPECS.md`. Do not repeat it per screen.

## Purpose

Implementation-oriented inventory of UI building blocks shared across routes so `components/ui` (or the System Design–defined primitive layer) can be aligned before feature work.

## Inventory

For each row, derive only from Discovery + the screen specs above; deduplicate across screens.

| Primitive / variant (neutral name) | Screens / routes | Notes (behavior, not visuals) | Suggested kit mapping (optional) |
| ---------------------------------- | ---------------- | ------------------------------ | ------------------------------ |
| \<e.g. Primary link / button — navigation\> | \<routes\> | \<e.g. navigates per Discovery\> | \<e.g. Button asChild + Link\> |
| \<e.g. Month filter control\> | \<routes\> | \<YYYY-MM, required for API\> | \<if stack implies one\> |

## Explicitly out of scope (for this product)

List any common primitives **not** needed (e.g. card, modal, data grid) **because** Discovery / screens do not require them—**one line** is enough.

## Constraints

* Must align with Discovery
* Must align with System Design
* Must NOT introduce new features or new screens
