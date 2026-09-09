# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-10

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing existing owners and is frequently used.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system, **When** I search for owners with the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** there are no owners with a specific last name prefix, **When** I search for owners with that prefix, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a new owner (Priority: P2)

As a clinic staff member, I want to add a new owner to the system so that I can register new clients.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is added to the list.

**Acceptance Scenarios**:

1. **Given** I am on the new owner form, **When** I enter valid owner details (first name, last name, address, city, telephone) and submit the form, **Then** the owner is created successfully and I am redirected to the owner's list page.

---

### User Story 3 - Handle owner creation errors (Priority: P3)

As a clinic staff member, I want to receive clear feedback when I submit invalid owner information so that I can correct the errors.

**Why this priority**: Ensures data integrity and guides users to provide correct information.

**Independent Test**: Can be fully tested by submitting the new owner form with invalid data and verifying error messages.

**Acceptance Scenarios**:

1. **Given** I am on the new owner form, **When** I submit the form with a blank address, **Then** a validation error message for the "address" field is displayed, and I remain on the new owner form.
2. **Given** I am on the new owner form, **When** I submit the form with a telephone number that is not 10 digits, **Then** a validation error message for the "telephone" field is displayed, and I remain on the new owner form.

---

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the updating of an existing owner's details.
- **FR-003**: System MUST validate that the owner's first name is not blank.
- **FR-004**: System MUST validate that the owner's last name is not blank.
- **FR-005**: System MUST validate that the owner's address is not blank.
- **FR-006**: System MUST validate that the owner's city is not blank.
- **FR-007**: System MUST validate that the owner's telephone number consists of exactly 10 digits.
- **FR-008**: System MUST allow searching for owners by their last name prefix.
- **FR-009**: System MUST disallow the 'id' field when creating or updating an owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the pet clinic. Includes attributes for first name, last name, address, city, telephone, and a list of associated pets.
- **Pet**: Represents an animal belonging to an owner. Includes attributes for birth date, type, and a list of visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a medical visit for a pet. Includes attributes for date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: 95% of new owner creations with valid data are successful on the first attempt.
- **SC-003**: Validation errors for owner creation/update are displayed clearly and immediately upon submission of invalid data.
- **SC-004**: The system supports managing up to 10,000 owners without performance degradation.

## Assumptions

- Users performing these actions are authenticated clinic staff members.
- The system has a mechanism for generating unique owner IDs.
- The `Pet` entity and its associated types (PetType, Visit) are managed separately but are linked to the Owner.
- The telephone number format validation (`\d{10}`) is sufficient for the project's needs.
- The search functionality for owners by last name prefix is case-insensitive.