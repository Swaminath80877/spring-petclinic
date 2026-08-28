# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `017-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owner information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed list.

**Acceptance Scenarios**:

1. **Given** the system has multiple owners with the last name "Smith", **When** a user searches for "Smith", **Then** a list of all owners with the last name "Smith" is displayed.
2. **Given** the system has no owners with the last name "Jones", **When** a user searches for "Jones", **Then** a "not found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to be able to add new owners to the system so that we can register new clients.

**Why this priority**: Essential for onboarding new customers and expanding the clinic's client base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting, and verifying the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields populated, **Then** the owner is created and the user is redirected to the owner's list page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** a validation error is displayed for the address field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P3)

As a clinic staff member, I want to view the complete details of an existing owner so that I can understand their information and their pets.

**Why this priority**: Allows for quick access to all relevant owner and pet information for better service.

**Independent Test**: Can be fully tested by selecting an owner from the list and verifying all their details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with a registered pet exists, **When** the user navigates to the owner's details page, **Then** all owner attributes (name, address, city, telephone) and their associated pet(s) (name, birth date, type) are displayed.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P3)

As a clinic staff member, I want to add a new pet for an existing owner so that we can keep track of all their animals.

**Why this priority**: Important for maintaining a complete record of each owner's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling in valid pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** a user adds a new pet with valid details (name, birth date, type), **Then** the pet is successfully created and associated with the owner.
2. **Given** an existing owner, **When** a user attempts to add a pet with a duplicate name for that owner, **Then** a validation error is displayed, and the pet is not created.

---

### User Story 5 - Update an Existing Pet's Information (Priority: P4)

As a clinic staff member, I want to update an existing pet's information so that the records are always accurate.

**Why this priority**: Ensures data accuracy for pet records.

**Independent Test**: Can be fully tested by selecting a pet, navigating to the edit pet form, changing a detail (e.g., name), saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a user updates the pet's name and saves, **Then** the pet's name is updated in the system.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Blank Pet Birth Date**: Pet creation/update with a blank birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Submitting a visit with a date that is not in the future → validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found during Find**: Searching for owners with a last name that yields no results → `result.rejectValue("lastName", "notFound", "not found")` is called, and the "owners/findOwners" view is returned.
- **Exception Trigger**: Navigating to the `/oups` endpoint → a `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST display a form for creating or updating a pet, pre-populated with owner details.
- **FR-003**: System MUST validate pet information before saving.
- **FR-004**: System MUST allow owners to be found by their last name.
- **FR-005**: System MUST allow updating a pet's name.
- **FR-006**: System MUST allow updating an owner's address.
- **FR-007**: System MUST allow updating an owner's city.
- **FR-008**: System MUST allow updating an owner's telephone number.
- **FR-009**: System MUST display all owner attributes on the owner details page.
- **FR-010**: System MUST display all pets associated with an owner on the owner details page.
- **FR-011**: System MUST validate owner information upon creation or update.
- **FR-012**: System MUST display a form for creating a new owner.
- **FR-013**: System MUST display a form for finding owners by last name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (address, city, telephone) and a collection of their pets.
- **Pet**: Represents an animal owned by a pet owner, including its name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Owner details can be viewed within 2 seconds.
- **SC-004**: New pets can be added to an owner's record in under 1 minute.
- **SC-005**: 95% of data entry operations (owner creation/update, pet creation/update) are completed without validation errors on the first attempt.

## Assumptions

- Users performing these actions are clinic staff with appropriate permissions.
- The underlying database and persistence layer are functional.
- Standard web browser capabilities are assumed for user interaction.
- The system will use a sequential numbering scheme for new owners if not otherwise specified.
- The system will use the current date as a default for new pet birth dates if not specified, though this is unlikely to be a user-facing option.
- The system will use standard date formats for display and input.
- Error messages will be user-friendly and informative.
- The `owners` module is the primary focus, and other modules (like `vets`) are considered external dependencies for this specification.
- The `spring-petclinic` project structure and conventions will be followed.
- The `SPEC_FILE` will be created in a `specs/` directory with a prefix based on sequential numbering.
- The `SPECIFY_FEATURE_DIRECTORY` will be `specs/001-owners-management`.
- The `SPEC_FILE` will be `specs/001-owners-management/spec.md`.