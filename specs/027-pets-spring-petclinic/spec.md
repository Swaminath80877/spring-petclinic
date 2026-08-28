# Feature Specification: Pet Management

**Feature Branch**: `027-pets-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a new pet for an owner (Priority: P1)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage all their animals.

**Why this priority**: This is a core function for managing pet information and is essential for the clinic's operations.

**Independent Test**: Can be fully tested by navigating to an owner's profile, initiating the "Add Pet" action, filling in valid pet details, and verifying the pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1, **When** a new pet is created with valid details (name: "Buddy", type: "hamster", birthDate: "1990-01-01"), **Then** the pet is successfully added to the owner and the owner's details are updated.
2. **Given** an owner exists, **When** a new pet is created with a blank name, **Then** a validation error is displayed, and the pet is not created.
3. **Given** an owner exists, **When** a new pet is created without specifying a type, **Then** a validation error is displayed, and the pet is not created.
4. **Given** an owner exists, **When** a new pet is created without providing a birth date, **Then** a validation error is displayed, and the pet is not created.

---

### User Story 2 - Prevent creation of a pet with a duplicate name for the same owner (Priority: P2)

As a clinic staff member, I want to be prevented from adding a pet with a name that already exists for the same owner, to avoid confusion.

**Why this priority**: Maintaining unique pet names per owner is crucial for accurate record-keeping and avoiding data ambiguity.

**Independent Test**: Can be tested by attempting to add a second pet with the exact same name as an existing pet for a given owner, and verifying the system rejects the action with an appropriate error message.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and already has a pet named "petty", **When** an attempt is made to create a new pet for this owner with the name "petty", **Then** a validation error indicating a duplicate name is shown, and the pet is not created.

---

### User Story 3 - Update an existing pet's details (Priority: P3)

As a clinic staff member, I want to be able to update an existing pet's information (name, type, birth date) so that the records remain accurate.

**Why this priority**: Allows for correction of errors or updating information as circumstances change.

**Independent Test**: Can be tested by selecting an existing pet, modifying its details (e.g., name, type), saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and has a pet with ID 1 named "petty", **When** the pet's details are updated (e.g., name to "Buddy", type to "hamster", birthDate to "1990-01-01"), **Then** the pet's information is successfully updated and persisted.

---

### Edge Cases

- What happens when a pet's birth date is set in the future? → System rejects with a "typeMismatch.birthDate" error.
- What happens when a visit date is set in the past or present? → System rejects with a "typeMismatch.visitDate" error.
- What happens when a request is made for a pet or visit associated with a non-existent owner ID? → System throws an `IllegalArgumentException` indicating the owner was not found.
- What happens when the `/oups` endpoint is accessed? → System throws a `RuntimeException` and returns an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate pet name, type, and birth date during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's details.
- **FR-004**: System SHOULD display a form for creating or updating pet information.
- **FR-005**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-006**: System MUST prevent a pet from having a name that is already in use by another pet belonging to the same owner.
- **FR-007**: System MUST reject attempts to create or update a pet with a blank name.
- **FR-008**: System MUST reject attempts to create or update a pet without specifying its type.
- **FR-009**: System MUST reject attempts to create or update a pet without providing a birth date.
- **FR-010**: System MUST reject attempts to create or update a pet with a birth date set in the future.
- **FR-011**: System MUST reject attempts to book a visit with a date that is not in the future.
- **FR-012**: System MUST throw an `IllegalArgumentException` for requests involving non-existent owners.
- **FR-013**: Accessing the `/oups` endpoint MUST result in a `RuntimeException` and an internal server error.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an individual animal. Key attributes include name, birth date, and type. It is associated with an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster). It has a name and is associated with pets.
- **Visit**: Represents a single appointment or interaction with a pet. Key attributes include the date of the visit and a description. It is associated with a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully add a new pet to an owner's record in under 1 minute.
- **SC-002**: Validation errors for duplicate pet names, missing required fields, or future dates are displayed to the user within 2 seconds of submission.
- **SC-003**: 95% of pet updates are successfully persisted and reflected in the system within 3 seconds.
- **SC-004**: The system can handle at least 50 concurrent requests for pet creation or updates without performance degradation.

## Assumptions

- Users interacting with the pet management system are clinic staff with appropriate permissions.
- The existing owner data is accurate and accessible.
- A predefined list of pet types is available and sufficient for initial use.
- The system will reuse existing date formatting and validation logic for birth dates and visit dates.
- Error messages for validation failures will be user-friendly and informative.
- The "Crash Endpoint" is intended for testing error handling and should return a 500 Internal Server Error.