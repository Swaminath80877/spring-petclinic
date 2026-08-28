# Feature Specification: Pet Management for Spring PetClinic

**Feature Branch**: `008-pets-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a new pet for an owner (Priority: P1)

As a clinic staff member, I want to be able to create a new pet for an existing owner so that I can record their details in the system.

**Why this priority**: This is a core function for managing pet information and is essential for the system's primary purpose.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the pet creation form, entering valid pet details, and verifying the pet is listed under the owner. Delivers the ability to add new pets.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1, **When** a new pet is created with valid details (name: "Buddy", type: "hamster", birthDate: "1990-01-01"), **Then** the pet is saved and linked to the owner, and a success message "Pet details has been edited" is displayed.
2. **Given** an owner exists, **When** a new pet is created with a valid name and type but no birth date, **Then** the system rejects the creation with a "required" error for the birth date field.

---

### User Story 2 - Update an existing pet's details (Priority: P1)

As a clinic staff member, I want to be able to update an existing pet's details so that I can correct or modify their information.

**Why this priority**: Maintaining accurate pet information is crucial for effective clinic operations.

**Independent Test**: Can be fully tested by selecting an owner, choosing an existing pet, modifying its details, saving the changes, and verifying the updated information is displayed. Delivers the ability to correct pet information.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and a pet with ID 1 named "petty", **When** the pet's details are updated (e.g., name changed to "Buddy", birthDate to "1990-01-01"), **Then** the pet's details are updated in the system, and the user is redirected to the owner's details page with a success message "Pet details has been edited".
2. **Given** an owner exists with ID 1 and a pet named "Buddy", **When** an attempt is made to update this pet's name to "Buddy" (a duplicate name for the same owner), **Then** the system rejects the update with a "duplicate" error for the "name" field.

---

### User Story 3 - Prevent creation of a pet with a duplicate name for the same owner (Priority: P2)

As a clinic staff member, I want the system to prevent me from creating a pet with a name that already exists for the same owner, so that pet names remain unique within an owner's record.

**Why this priority**: Ensures data integrity and avoids confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by creating a pet with a specific name for an owner, then attempting to create another pet for the same owner with the identical name. Delivers a safeguard against duplicate pet names.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and already has a pet named "petty", **When** an attempt is made to create a new pet with the name "petty", **Then** the system rejects the creation, indicating a "duplicate" error for the "name" field, and the form remains on the "createOrUpdatePetForm" view.

---

### User Story 4 - Select pet type from a predefined list (Priority: P2)

As a clinic staff member, I want to be able to select the pet's type from a predefined list (e.g., cat, dog, hamster) when creating or updating a pet, so that I can ensure consistency and accuracy in pet categorization.

**Why this priority**: Standardizes pet types, improving data quality and enabling better reporting and filtering.

**Independent Test**: Can be fully tested by initiating pet creation/update and verifying a dropdown or selection mechanism displays available pet types, and that selecting one correctly populates the pet's type. Delivers standardized pet type selection.

**Acceptance Scenarios**:

1. **Given** the pet creation form is open, **When** the user views the "Pet Type" field, **Then** a list of available pet types (e.g., "cat", "dog", "hamster") is presented for selection.
2. **Given** the user selects "dog" from the pet type list, **When** the pet is saved, **Then** the pet's type is recorded as "dog".

---

### User Story 5 - Add a visit for a pet (Priority: P3)

As a clinic staff member, I want to be able to add a visit record for a specific pet, including a description and date, so that I can track their medical history.

**Why this priority**: Essential for maintaining a complete medical history for each pet.

**Independent Test**: Can be fully tested by selecting a pet, navigating to the visit creation form, entering a valid description and date, and verifying the visit is recorded for that pet. Delivers the ability to log pet visits.

**Acceptance Scenarios**:

1. **Given** a pet exists, **When** a new visit is added with description "Annual check-up" and date "2026-09-15", **Then** the visit is successfully recorded and associated with the pet.
2. **Given** a pet exists, **When** an attempt is made to add a visit with an invalid date (e.g., in the past), **Then** the system rejects the creation with a "typeMismatch.visitDate" error.

---

### Edge Cases

- **Duplicate Pet Name**: Attempting to create or update a pet with a name that already exists for the same owner → system rejects with a "duplicate" error.
- **Missing Pet Name**: Attempting to create or update a pet without providing a name → system rejects with a "required" error.
- **Missing Pet Type**: Attempting to create a new pet without specifying its type → system rejects with a "required" error.
- **Missing Pet Birth Date**: Attempting to create or update a pet without providing a birth date → system rejects with a "required" error.
- **Future Birth Date**: Attempting to create or update a pet with a birth date in the future → system rejects with a "typeMismatch.birthDate" error.
- **Invalid Visit Date**: Attempting to book a visit with a date that is not in the future (i.e., today or in the past) → system rejects with a "typeMismatch.visitDate" error.
- **Non-existent Owner**: Attempting to create or update a pet or visit for an owner ID that does not exist → system throws an `IllegalArgumentException` indicating the owner was not found.
- **Data Integrity Violation (Duplicate Pet Name)**: Attempting to save a pet with a name that is a case-insensitive duplicate of an existing pet's name for the same owner → system throws a `DataIntegrityViolationException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate pet name, type, and birth date during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's details.
- **FR-004**: System SHOULD display a form for creating or updating pet information.
- **FR-005**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-006**: System MUST allow adding a visit record for a pet, including a description and date.
- **FR-007**: System MUST validate the visit date to ensure it is in the future.
- **FR-008**: System MUST prevent the creation of a pet with a name that is a duplicate of an existing pet's name for the same owner.
- **FR-009**: System MUST reject pet creation/update if the owner ID does not exist.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. It is associated with an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat, hamster). It has a name and can be associated with multiple pets.
- **Visit**: Represents a record of a pet's visit to the clinic. Key attributes include description and date. It is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new pet for an owner in under 1 minute.
- **SC-002**: Updating an existing pet's details takes less than 45 seconds.
- **SC-003**: 99% of pet creation/update attempts with valid data succeed.
- **SC-004**: The system prevents duplicate pet names for the same owner with a clear error message.
- **SC-005**: All pet visits are recorded accurately with correct descriptions and dates.
- **SC-006**: The system handles invalid input for pet name, type, and birth date gracefully, providing informative error messages.

## Assumptions

- Users interacting with the pet management system are clinic staff with appropriate permissions.
- A mechanism for selecting existing owners exists and is functional.
- The list of available pet types is managed elsewhere and will be provided to this feature.
- Dates are handled in the `YYYY-MM-DD` format.
- The system will leverage existing Spring Boot conventions for error handling and validation messages.
- The `Owner` entity is already defined and accessible.