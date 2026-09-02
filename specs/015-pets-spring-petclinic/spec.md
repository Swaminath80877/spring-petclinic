# Feature Specification: Pet Management

**Feature Branch**: `015-pets-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a new pet for an owner (Priority: P1)

Given an owner exists, When a new pet is created with valid details (name, type, birthDate), Then the pet is successfully added to the owner and the owner's details are updated.

**Why this priority**: This is the core functionality for managing pets within the clinic.

**Independent Test**: Can be fully tested by creating a new owner, then adding a pet to that owner, and verifying the pet is listed.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** a new pet is created with a unique name, a valid pet type, and a valid birth date, **Then** the pet is successfully associated with the owner and appears in the owner's pet list.
2. **Given** an owner exists in the system, **When** a new pet is created with a unique name, a valid pet type, and a birth date in the past, **Then** the pet is successfully associated with the owner.

---

### User Story 2 - Prevent creation of a pet with a duplicate name for the same owner (Priority: P2)

Given an owner exists and already has a pet with a specific name, When an attempt is made to create a new pet for the same owner with the same name, Then a "duplicate" error is reported for the pet's name, and the form is redisplayed.

**Why this priority**: Ensures data integrity and prevents confusion for users.

**Independent Test**: Can be tested by creating a pet for an owner, then attempting to create another pet for the same owner with the identical name.

**Acceptance Scenarios**:

1. **Given** an owner exists and has a pet named "Buddy", **When** an attempt is made to create a new pet for the same owner with the name "Buddy", **Then** a validation error indicating a duplicate name is displayed, and the pet creation form remains visible with previous inputs.

---

### User Story 3 - Update an existing pet's details (Priority: P3)

Given an owner exists and has a pet, When the pet's details (name, type, birthDate) are updated, Then the pet's details are successfully updated and the owner's details reflect the changes.

**Why this priority**: Allows for correction of errors and maintenance of accurate pet information.

**Independent Test**: Can be tested by creating a pet, then updating its name, type, or birth date, and verifying the changes.

**Acceptance Scenarios**:

1. **Given** an owner exists and has a pet, **When** the pet's name is updated to a unique name, **Then** the pet's name is successfully changed.
2. **Given** an owner exists and has a pet, **When** the pet's type is updated to a different valid type, **Then** the pet's type is successfully changed.
3. **Given** an owner exists and has a pet, **When** the pet's birth date is updated to a valid date, **Then** the pet's birth date is successfully updated.

---

### User Story 4 - Add a visit for a pet (Priority: P1)

Given a pet exists for an owner, When a new visit is created with valid details (description, date), Then the visit is successfully recorded for the pet.

**Why this priority**: Core functionality for tracking pet health events.

**Independent Test**: Can be tested by creating a pet, then adding a visit for that pet, and verifying the visit is listed.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a new visit is created with a description and a future date, **Then** the visit is successfully associated with the pet.

---

### User Story 5 - Prevent adding a visit with a past date (Priority: P2)

Given a pet exists for an owner, When an attempt is made to create a visit with a date in the past, Then a validation error is displayed for the visit date.

**Why this priority**: Ensures chronological accuracy of visit records.

**Independent Test**: Can be tested by creating a pet, then attempting to add a visit with a date prior to the current date.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** an attempt is made to create a visit with a date that is in the past, **Then** a validation error indicating an invalid date is displayed.

---

### Edge Cases

- **Duplicate Pet Name**: Attempting to add a pet with a name that already exists for the same owner → system rejects with a "duplicate" error.
- **Missing Pet Type**: Attempting to create a pet without specifying its type → system rejects with a "required" error for the pet type.
- **Empty Pet Name**: Attempting to create or update a pet with an empty name → system rejects with a "required" error for the name.
- **Future Birth Date**: Attempting to create or update a pet with a birth date in the future → system rejects with a "typeMismatch.birthDate" error.
- **Null Birth Date**: Attempting to create or update a pet with a null birth date → system rejects with a "required" error for the birth date.
- **Visit Date in the Past**: Attempting to book a visit with a date that is not after the current date → system rejects with a "typeMismatch.visitDate" error.
- **Visit with Missing Fields**: Attempting to process a new visit form with missing required fields → system rejects with validation errors on the visit object.
- **Non-existent Owner for Visit**: Attempting to create a visit for a non-existent owner ID → system throws an `IllegalArgumentException` indicating the owner was not found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate the name, type, and birth date of a pet during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's information.
- **FR-004**: System SHOULD display a form for creating or updating a pet, pre-populated with the owner's details.
- **FR-005**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-006**: System MUST allow the creation of a new visit for an existing pet.
- **FR-007**: System MUST validate the description and date of a visit during creation.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an animal owned by a person. Key attributes include name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Hamster). Key attribute is its name.
- **Visit**: Represents a medical visit for a pet. Key attributes include description and date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new pet for an owner in under 1 minute.
- **SC-002**: The system prevents the creation of duplicate pet names for the same owner with 100% accuracy.
- **SC-003**: 95% of pet detail updates are completed successfully without errors.
- **SC-004**: Users can add a new visit for a pet in under 45 seconds.
- **SC-005**: The system rejects all attempts to book visits with past dates.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing owner data.
- The list of available pet types is managed elsewhere and will be provided to the pet creation/update forms.
- The system will handle date formatting based on user locale.