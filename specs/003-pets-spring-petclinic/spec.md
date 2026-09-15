# Feature Specification: Pet Management

**Feature Branch**: `[001-pet-management]`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a new pet for an owner (Priority: P1)

As a clinic staff member, I want to be able to add a new pet for an existing owner so that I can record their animal companions in the system.

**Why this priority**: This is a core function for managing pet information and is essential for the system's primary purpose.

**Independent Test**: Can be fully tested by navigating to an owner's profile, initiating the "Add Pet" action, filling in valid pet details, and verifying the pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1, **When** a new pet is created with valid details (name: "Buddy", type: "hamster", birthDate: "1990-01-01"), **Then** the pet is saved successfully and linked to the owner, and a success message "Pet details has been edited" is displayed.
2. **Given** an owner exists with ID 1, **When** a new pet is created with a blank name, **Then** the system rejects the creation with a "name must not be blank" error.
3. **Given** an owner exists with ID 1, **When** a new pet is created without assigning a type, **Then** the system rejects the creation with a "pet type is required" error.
4. **Given** an owner exists with ID 1, **When** a new pet is created without providing a birth date, **Then** the system rejects the creation with a "birth date is required" error.
5. **Given** an owner exists with ID 1, **When** a new pet is created with a birth date in the future, **Then** the system rejects the creation with a "birth date cannot be in the future" error.

---

### User Story 2 - Prevent creation of a pet with a duplicate name for the same owner (Priority: P2)

As a clinic staff member, I want the system to prevent me from adding a pet with a name that already exists for the same owner, to avoid confusion and maintain data integrity.

**Why this priority**: Prevents data duplication and ensures each pet within an owner's record is uniquely identifiable by name.

**Independent Test**: Can be fully tested by adding a pet with a specific name for an owner, then attempting to add another pet for the same owner with the identical name, and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and already has a pet named "petty", **When** an attempt is made to create a new pet for this owner with the name "petty", **Then** the system rejects the creation, displaying an "already exists" error for the pet's name, and the form remains on the create/update pet page.

---

### User Story 3 - Update an existing pet's details (Priority: P3)

As a clinic staff member, I want to be able to update the details of an existing pet, such as its name, type, or birth date, to ensure the pet's information is always current.

**Why this priority**: Allows for correction of errors and reflects changes in a pet's information over time.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, submitting the changes, and verifying the updated information on the owner's details page.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID 1 and has a pet with ID 1 named "petty", **When** the owner updates the pet's details (e.g., name to "Buddy", type to "dog", birthDate to "2015-02-12") and submits the form, **Then** the pet's details are updated, and the owner is redirected to the owner's details page with a message "Pet details has been edited".
2. **Given** an owner exists with ID 1 and has a pet with ID 1, **When** the owner attempts to update the pet's name to a blank value, **Then** the system rejects the update with a "name must not be blank" error.

---

### User Story 4 - Add a visit for a pet (Priority: P1)

As a clinic staff member, I want to be able to add a visit record for a specific pet, including the date and a description of the visit, to track the pet's medical history.

**Why this priority**: Essential for maintaining a complete medical history of pets.

**Independent Test**: Can be fully tested by selecting a pet, initiating the "Add Visit" action, providing a valid date and description, and verifying the visit appears in the pet's visit history.

**Acceptance Scenarios**:

1. **Given** a pet exists with ID 1, **When** a new visit is added with date "2026-09-15" and description "Routine check-up", **Then** the visit is saved successfully and linked to the pet.
2. **Given** a pet exists with ID 1, **When** a new visit is added with a date in the past (e.g., "2026-09-14"), **Then** the system rejects the addition with a "visit date must not be in the past" error.
3. **Given** a pet exists with ID 1, **When** a new visit is added with a blank description, **Then** the system rejects the addition with a "description must not be blank" error.

---

### Edge Cases

- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with a "duplicate" error message.
- **Missing Pet Name**: Creating or updating a pet without providing a name → system rejects with a "required" error.
- **Missing Pet Type**: Creating a pet without assigning a type (when it's a new pet) → system rejects with a "required" error.
- **Missing Birth Date**: Creating or updating a pet without providing a birth date → system rejects with a "required" error.
- **Future Birth Date**: Creating or updating a pet with a birth date in the future → system rejects with a "typeMismatch.birthDate" error.
- **Visit Date Not in Future**: Submitting a new visit with a date that is not after the current date → system rejects with a "typeMismatch.visitDate" error.
- **Non-existent Owner ID**: Attempting to access or create resources for a pet associated with an owner ID that does not exist → system throws an "IllegalArgumentException" indicating the owner was not found.
- **Concurrency Issue with Duplicate Pet Name**: Multiple concurrent requests to add a pet with the same name for the same owner → only one request succeeds, and others are blocked, resulting in a count of 1 successful addition and the final pet count reflecting only one new pet.
- **Exception Trigger**: Navigating to the "/oups" endpoint → throws a `RuntimeException` with a specific message, indicating a controlled exception scenario.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an owner.
- **FR-002**: System MUST validate the name, type, and birth date of a pet during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's information.
- **FR-004**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-005**: System SHOULD ensure that a pet's identifier is not null when adding a visit.
- **FR-006**: System MUST allow the creation of a new visit for a pet, including date and description.
- **FR-007**: System MUST validate the visit date and description during creation.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an animal companion. Key attributes include name, birth date, and type. It is associated with an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Hamster). Key attribute is its name.
- **Visit**: Represents a medical visit for a pet. Key attributes include the date of the visit and a description of the services provided. It is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new pet for an owner in under 1 minute.
- **SC-002**: System prevents duplicate pet names for the same owner with 100% accuracy.
- **SC-003**: 95% of pet detail updates are completed successfully within 30 seconds.
- **SC-004**: 99% of new visit entries are created successfully within 45 seconds.
- **SC-005**: The system correctly links all visits to their respective pets.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing owner management functionality.
- Pet types are predefined and managed separately.
- The current date is used as a reference for validating visit dates.
- The system will display user-friendly error messages for validation failures.
- The "spring-petclinic" project structure and conventions will be followed.
- The `PetType` entity will be populated with common pet types (e.g., Cat, Dog, Bird, Rabbit, Hamster).
- The `Visit` date validation will ensure the date is not in the past relative to the current date.