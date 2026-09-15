# Feature Specification: Add Pet Visits

**Feature Branch**: `004-visits-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "visits for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Successfully book a new visit for a pet (Priority: P1)

Given an owner and a pet exist, When a user submits a new visit form with a future date and description, Then the visit is booked successfully and the user is redirected to the owner's details page.

**Why this priority**: This is the core functionality of adding a visit, directly addressing the primary user need.

**Independent Test**: Can be fully tested by navigating to an owner's pet, filling out the visit form with valid data, and verifying the visit appears on the owner's details page.

**Acceptance Scenarios**:

1. **Given** an existing owner and a pet associated with that owner, **When** the user navigates to the "Add Visit" form for the pet, enters a future date (e.g., tomorrow's date) and a description (e.g., "Annual check-up"), and submits the form, **Then** the visit is successfully recorded, and the user is redirected to the owner's details page, displaying the newly added visit.

---

### User Story 2 - Receive an error when booking a visit with a past date (Priority: P2)

Given an owner and a pet exist, When a user submits a new visit form with a date that is not in the future, Then the form displays a type mismatch error for the date field and remains on the visit creation form.

**Why this priority**: Ensures data integrity by preventing invalid past visit entries, which is a critical business rule.

**Independent Test**: Can be tested by attempting to submit a visit with a past date and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an existing owner and a pet, **When** the user navigates to the "Add Visit" form for the pet, enters a past date (e.g., yesterday's date) and a description, and submits the form, **Then** a "type mismatch" error related to the date field is displayed on the form, and the user remains on the visit creation form.

---

### User Story 3 - View the visit creation form (Priority: P3)

Given an owner and a pet exist, When a user navigates to the new visit form for that pet, Then the visit creation form is displayed.

**Why this priority**: This is a prerequisite for booking a visit and ensures users can access the necessary interface.

**Independent Test**: Can be tested by navigating to an owner's pet and verifying the visit form is accessible.

**Acceptance Scenarios**:

1. **Given** an existing owner and a pet, **When** the user navigates to the "Add Visit" form for that pet, **Then** the visit creation form is displayed, showing fields for date and description.

---

### Edge Cases

- What happens when the visit description is empty?
- How does the system handle a missing visit date during submission?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow adding a new visit for a pet.
- **FR-002**: System MUST retrieve all visits for a given pet.
- **FR-003**: System SHOULD ensure that adding a visit increments the visit count for the pet.
- **FR-004**: System SHOULD ensure that each added visit has a non-null ID.
- **FR-005**: System SHOULD allow retrieving an owner by ID and then accessing their pets and associated visits.
- **FR-006**: System MUST validate that a visit date is in the future.
- **FR-007**: System MUST validate that a visit has a description.

### Key Entities *(include if feature involves data)*

- **Visit**: Represents a single visit to the clinic. Attributes include:
    - `id`: Unique identifier for the visit.
    - `date`: The date of the visit.
    - `description`: A text description of the visit's purpose.
    - `owner`: The owner of the pet receiving the visit.
    - `pet`: The pet receiving the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully book a new visit in under 1 minute.
- **SC-002**: 99% of valid visit submissions are processed without errors.
- **SC-003**: Users receive immediate feedback (error messages) for invalid visit dates or missing descriptions.
- **SC-004**: The system correctly displays all past visits associated with a pet on the owner's details page.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing owner and pet data structures.
- The date format for input will be handled by the front-end or framework defaults.
- Error messages will be user-friendly and informative.
- The "visit count for the pet" mentioned in FR-003 refers to a display or internal counter, not a strict database constraint.
- The `BaseEntity` and `NamedEntity` abstractions provide necessary ID generation and naming capabilities.
- The `JpaRepository` will handle persistence operations for `Visit` entities.
- The `PetValidator` and `OwnerRepository` are available and functional for related operations.
- The `VisitController` will manage the user interface and form submissions for visits.