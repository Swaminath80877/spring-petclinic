# Feature Specification: Pet Types for Spring PetClinic

**Feature Branch**: `003-pet-types-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "pet types for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet type (Priority: P1)

As a clinic administrator, I want to add new types of pets that the clinic can handle, so that our system accurately reflects the services we offer.

**Why this priority**: This is a foundational requirement for managing pet information accurately. Without defined pet types, the system cannot properly categorize pets.

**Independent Test**: Can be fully tested by navigating to a pet type management interface, entering a new pet type name, and verifying its successful addition and display in the list of available types.

**Acceptance Scenarios**:

1. **Given** I am on the pet types management page, **When** I enter "Dog" into the new pet type field and click "Add", **Then** "Dog" appears in the list of available pet types.
2. **Given** I am on the pet types management page, **When** I enter "Cat" into the new pet type field and click "Add", **Then** "Cat" appears in the list of available pet types.

---

### User Story 2 - View existing pet types (Priority: P1)

As a clinic administrator or staff member, I want to view all the currently supported pet types, so that I can select the correct type when adding or managing a pet.

**Why this priority**: Essential for data entry and ensuring consistency. Users need to see what options are available.

**Independent Test**: Can be fully tested by navigating to the pet types management page and verifying that all previously added pet types are displayed.

**Acceptance Scenarios**:

1. **Given** "Dog" and "Cat" pet types have been previously added, **When** I navigate to the pet types management page, **Then** I see "Dog" and "Cat" listed as available pet types.

---

### User Story 3 - Attempt to add a duplicate pet type (Priority: P2)

As a clinic administrator, I want to be prevented from adding a pet type that already exists, so that the system maintains unique pet type entries.

**Why this priority**: Prevents data redundancy and ensures data integrity.

**Independent Test**: Can be fully tested by attempting to add a pet type name that is already present in the system and verifying that an error message is displayed and the duplicate is not added.

**Acceptance Scenarios**:

1. **Given** the pet type "Bird" already exists, **When** I attempt to add a new pet type named "Bird", **Then** an error message is displayed stating "Pet type name already exists", and "Bird" is not added again.

---

### User Story 4 - Assign a pet type to a pet (Priority: P1)

As a clinic staff member, I want to assign a pet type to a new or existing pet, so that the pet is correctly categorized within the system.

**Why this priority**: This is the primary use case for pet types – associating them with actual pets.

**Independent Test**: Can be fully tested by creating a new pet and selecting an existing pet type from a dropdown or list, then verifying the pet is saved with the correct type.

**Acceptance Scenarios**:

1. **Given** the pet type "Dog" exists, **When** I create a new pet and select "Dog" as its type, **Then** the pet is successfully created and associated with the "Dog" type.
2. **Given** a pet currently has no type assigned, **When** I edit the pet and assign it the type "Bird", **Then** the pet's type is updated to "Bird".

---

### User Story 5 - Update an existing pet type (Priority: P3)

As a clinic administrator, I want to update the name of an existing pet type, so that I can correct typos or reflect changes in terminology.

**Why this priority**: Allows for maintenance and correction of existing data.

**Independent Test**: Can be fully tested by selecting an existing pet type, changing its name, and verifying the update.

**Acceptance Scenarios**:

1. **Given** the pet type "Kitten" exists, **When** I edit the pet type and change its name to "Young Cat", **Then** the pet type is updated to "Young Cat" and any pets previously associated with "Kitten" are now associated with "Young Cat".

---

### User Story 6 - Delete an existing pet type (Priority: P3)

As a clinic administrator, I want to delete a pet type that is no longer supported, so that the system only reflects current offerings.

**Why this priority**: Allows for cleanup of outdated data.

**Independent Test**: Can be fully tested by deleting an existing pet type and verifying it is removed from the list of available types.

**Acceptance Scenarios**:

1. **Given** the pet type "Exotic Lizard" exists and is not assigned to any pets, **When** I delete the "Exotic Lizard" pet type, **Then** "Exotic Lizard" is no longer listed as an available pet type.

### Edge Cases

- **Blank Pet Name**: Submitting a pet with an empty or whitespace-only name → system rejects with "required" validation error.
- **Missing Pet Type**: Creating a new pet without assigning a type → system rejects with "required" validation error.
- **Missing Birth Date**: Creating a new pet without a birth date → system rejects with "required" validation error.
- **Future Birth Date**: Submitting a pet with a birth date in the future → system rejects with "typeMismatch.birthDate" validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with "duplicate" validation error.
- **Invalid Visit Date**: Submitting a visit with a date that is not after the current date → system rejects with "typeMismatch.visitDate" validation error.
- **Non-existent Owner ID**: Attempting to access or modify data for a non-existent owner ID → system throws an `IllegalArgumentException` indicating the owner was not found.
- **Non-existent Pet ID for Owner**: Attempting to access or modify a pet that does not exist for a given owner ID → system throws an `IllegalArgumentException` indicating the pet was not found.
- **Duplicate Pet Name Across Owners**: Adding a pet with a name that is already in use by a different owner → system allows the creation, demonstrating case-insensitive name comparison for different owners.
- **Exception Trigger**: Navigating to the "/oups" endpoint → system throws a `RuntimeException` and displays an error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pet types with a unique name.
- **FR-002**: System MUST allow the retrieval and display of all available pet types.
- **FR-003**: System SHOULD allow the updating of existing pet type names.
- **FR-004**: System SHOULD allow the deletion of existing pet types, provided they are not currently assigned to any pets.
- **FR-005**: System MUST validate pet type names to ensure they are not empty or blank.
- **FR-006**: System MUST allow a pet to be associated with a specific pet type.
- **FR-007**: System MUST prevent the creation of a pet type with a name that already exists.

### Key Entities *(include if feature involves data)*

- **PetType**: Represents a category of pet (e.g., Dog, Cat, Bird). It has a `name` attribute.
- **Pet**: Represents an individual animal. It has a `type` attribute which is a `PetType`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Administrators can add a new pet type in under 30 seconds.
- **SC-002**: All existing pet types are displayed on the management page within 1 second.
- **SC-003**: 100% of attempts to create a duplicate pet type are rejected with an appropriate error message.
- **SC-004**: 95% of users can successfully assign a pet type to a pet on their first attempt.
- **SC-005**: The system correctly displays the assigned pet type when viewing pet details.

## Assumptions

- Users interacting with pet type management will have appropriate administrative privileges.
- The system will use a standard, case-insensitive comparison for pet type names to prevent duplicates.
- Deleting a pet type that is currently assigned to pets will be prevented to maintain data integrity.
- The list of pet types will be presented in alphabetical order by default.