# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-08-27

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - View and Find Owners (Priority: P1)

As a clinic administrator, I want to be able to view a list of all owners and search for owners by their last name, so that I can quickly access owner information.

**Why this priority**: This is a core functionality for managing the clinic's customer base and is fundamental to many other operations.

**Independent Test**: Can be fully tested by navigating to the owner list page, searching with various last name prefixes, and verifying the displayed results.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system with different last names, **When** I navigate to the owner list page, **Then** I see a list of all owners.
2. **Given** there are owners with last names starting with "S", **When** I search for owners with the last name prefix "S", **Then** I see a list of owners whose last names start with "S".
3. **Given** there are no owners with a last name starting with "X", **When** I search for owners with the last name prefix "X", **Then** I see a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic administrator, I want to be able to add new owners to the system, so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new customers and expanding the clinic's client base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is added to the list and their details are correctly displayed.

**Acceptance Scenarios**:

1. **Given** I am on the new owner form, **When** I enter valid owner details (first name, last name, address, city, telephone) and submit the form, **Then** the new owner is created and I am redirected to the owner list page, showing the newly added owner.

---

### User Story 3 - Edit an Existing Owner (Priority: P2)

As a clinic administrator, I want to be able to edit the details of an existing owner, so that I can keep their information up-to-date.

**Why this priority**: Important for maintaining accurate client records.

**Independent Test**: Can be fully tested by selecting an owner from the list, editing their details, saving the changes, and verifying the updated information.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click the "Edit" button, **Then** I am presented with a form pre-populated with the owner's current information.
2. **Given** I am on the edit owner form, **When** I modify the owner's telephone number and save the changes, **Then** the owner's telephone number is updated in the system and displayed correctly.

---

### User Story 4 - Add a New Pet to an Owner (Priority: P3)

As a clinic administrator, I want to be able to add a new pet for an existing owner, so that I can associate pets with their owners in the system.

**Why this priority**: Core functionality for managing pet ownership within the clinic.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with valid details, and verifying it appears associated with the owner.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click the "Add New Pet" button, **Then** I am presented with a form to enter pet details (name, birth date, type).
2. **Given** I am on the add new pet form for a specific owner, **When** I enter a valid pet name, select a pet type, and provide a birth date, **Then** the new pet is created and associated with the owner.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the "\\d{10}" pattern → validation error.
- **Non-existent Owner**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST display a form to create or update a pet, pre-populated with owner and pet type information.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD allow the creation of a new pet with a null ID, indicating a new pet.
- **FR-005**: System SHOULD retrieve pet types to populate a dropdown in the pet creation/update form.
- **FR-006**: System MUST allow owners to be searched by last name prefix.
- **FR-007**: System MUST allow new owners to be created with their contact details.
- **FR-008**: System MUST allow existing owner details to be updated.
- **FR-009**: System MUST enforce that owner first name, last name, address, and city are not blank.
- **FR-010**: System MUST enforce that owner telephone number is exactly 10 digits.
- **FR-011**: System MUST enforce that pet names are not blank.
- **FR-012**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-013**: System MUST enforce that a pet has a type.
- **FR-014**: System MUST enforce that a pet has a birth date.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal and contact information, and a list of their pets.
- **Pet**: Represents an animal belonging to an owner, including its name, birth date, type, and visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Owners can be found by last name prefix in under 1 second.
- **SC-002**: New owners can be created and displayed in the owner list within 5 seconds of submission.
- **SC-003**: Editing an owner's details and saving the changes takes under 3 seconds to reflect in the system.
- **SC-004**: Adding a new pet to an owner is completed and visible within 5 seconds of submission.
- **SC-005**: 100% of validation rules for owner and pet creation/updates are enforced.

## Assumptions

- Users interacting with the owner management features are clinic administrators with appropriate permissions.
- The system will reuse existing `BaseEntity` and `NamedEntity` structures for domain objects.
- Standard Spring Data JPA repositories will be used for data persistence.
- The application will be deployed in an environment where database connectivity is stable.
- Error messages displayed to users will be user-friendly and informative.
- The format for telephone numbers is strictly 10 digits.
- The date format for birth dates and visit dates will be "yyyy-MM-dd".
- The system will handle concurrent edits to owner data gracefully, with the last save winning.
- The primary focus is on the core owner and pet management functionalities as described.