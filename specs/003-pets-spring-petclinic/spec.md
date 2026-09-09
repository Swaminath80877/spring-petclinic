# Feature Specification: Manage Pets

**Feature Branch**: `003-pets-spring-petclinic`

**Created**: 2026-09-09

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet for an owner (Priority: P1)

Given an owner exists with ID 1, When a new pet is created with valid details (name: "Buddy", type: "hamster", birthDate: "1990-01-01"), Then the pet is saved and linked to the owner, and the message "Pet details has been edited" is displayed.

**Why this priority**: This is the core functionality for managing pets, enabling users to add new animals to their profiles.

**Independent Test**: Can be fully tested by navigating to an owner's profile, initiating the "Add Pet" action, filling in valid pet details, and confirming the pet is listed and the success message is shown.

**Acceptance Scenarios**:

1. **Given** an owner with ID 1 exists, **When** a new pet is created with the name "Buddy", type "hamster", and birth date "1990-01-01", **Then** the pet is successfully saved and associated with owner ID 1, and a confirmation message "Pet details has been edited" is displayed.
2. **Given** an owner with ID 1 exists, **When** a new pet is created with the name "Whiskers", type "cat", and birth date "2020-05-15", **Then** the pet is successfully saved and associated with owner ID 1, and a confirmation message "Pet details has been edited" is displayed.

---

### User Story 2 - Prevent adding a pet with a duplicate name for the same owner (Priority: P2)

Given an owner exists with ID 1 and already has a pet named "Buddy", When an attempt is made to add a new pet with the name "Buddy", Then a validation error "already exists" is shown for the pet's name, and the form remains on the create/update pet page.

**Why this priority**: Prevents data integrity issues by ensuring unique pet names per owner, improving user experience by providing immediate feedback.

**Independent Test**: Can be tested by adding a pet named "Buddy" to owner ID 1, then attempting to add another pet with the exact same name "Buddy" to the same owner, verifying the error message and that the form does not submit.

**Acceptance Scenarios**:

1. **Given** an owner with ID 1 has a pet named "Buddy", **When** an attempt is made to add a new pet for owner ID 1 with the name "Buddy", **Then** a validation error indicating the name already exists is displayed for the pet's name field, and the pet is not saved.

---

### User Story 3 - Update an existing pet's details (Priority: P1)

Given an owner exists with ID 1 and has a pet with ID 1 named "petty", When the pet's details are updated (name: "Buddy", type: "hamster", birthDate: "1990-01-01"), Then the pet's details are updated successfully, and the user is redirected to the owner's details page with a success message.

**Why this priority**: Allows owners to correct or update information about their pets, maintaining accurate records.

**Independent Test**: Can be tested by selecting an existing pet for an owner, modifying its name, type, or birth date, saving the changes, and verifying the updated information on the owner's details page.

**Acceptance Scenarios**:

1. **Given** an owner with ID 1 has a pet with ID 1, **When** the pet's name is updated to "Buddy", its type to "hamster", and its birth date to "1990-01-01", **Then** the pet's details are updated successfully, and the user is redirected to the owner's details page with a success message.
2. **Given** an owner with ID 1 has a pet with ID 2, **When** the pet's type is updated to "dog" and its birth date to "2018-11-20", **Then** the pet's details are updated successfully, and the user is redirected to the owner's details page with a success message.

---

### User Story 4 - Add a visit for an existing pet (Priority: P1)

Given an owner with ID 1 has a pet with ID 1, When a new visit is added for this pet with a future date and description "Routine check-up", Then the visit is successfully recorded and linked to the pet.

**Why this priority**: Essential for tracking the medical history and care of pets.

**Independent Test**: Can be tested by navigating to a specific pet's profile, initiating the "Add Visit" action, providing a future date and a description, and confirming the visit is listed.

**Acceptance Scenarios**:

1. **Given** an owner with ID 1 has a pet with ID 1, **When** a visit is added with the date "2026-10-01" and description "Routine check-up", **Then** the visit is successfully recorded and associated with pet ID 1.
2. **Given** an owner with ID 1 has a pet with ID 2, **When** a visit is added with the date "2026-11-15" and description "Vaccination", **Then** the visit is successfully recorded and associated with pet ID 2.

### Edge Cases

- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with "duplicate" error.
- **Missing Pet Type**: Creating a new pet without specifying its type → system rejects with "required" error.
- **Missing Pet Name**: Creating or updating a pet with an empty name → system rejects with "required" error.
- **Missing Pet Birth Date**: Creating or updating a pet without a birth date → system rejects with "required" error.
- **Future Birth Date**: Creating or updating a pet with a birth date in the future → system rejects with "typeMismatch.birthDate" error.
- **Visit Date Not in Future**: Submitting a new visit with a date that is not in the future → system rejects with "typeMismatch.visitDate" error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate the name, type, and birth date of a pet during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's information.
- **FR-004**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-005**: System MUST allow adding a visit for an existing pet.
- **FR-006**: System MUST validate the visit date and description during visit creation.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an animal owned by a person. Attributes include name, birth date, and type. It is associated with an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a medical visit for a pet. Attributes include the date of the visit and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully add a new pet for an owner in under 1 minute.
- **SC-002**: 95% of pet updates are completed successfully without errors.
- **SC-003**: The system prevents the creation of duplicate pet names for the same owner.
- **SC-004**: All required fields for pet creation and update (name, type, birth date) are validated, with validation errors displayed clearly to the user.
- **SC-005**: Users can add a new visit for a pet with a future date, and the visit is recorded accurately.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing owner data.
- The list of available pet types is predefined and managed separately.
- The system will provide user-friendly error messages for validation failures.
- Visits are always associated with a pet that already exists.