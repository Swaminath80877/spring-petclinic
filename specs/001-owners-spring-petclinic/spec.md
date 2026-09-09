# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-10

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing pet owners, essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners. Delivers immediate value for finding existing records.

**Acceptance Scenarios**:

1. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Jo", **Then** a list containing "Jones" is displayed.
3. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Xy", **Then** an empty list is displayed and a "no owners found" message is shown.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: Adding new owners is a fundamental requirement for expanding the pet clinic's client base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting, and verifying redirection to the owner list with the new owner present.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" form, **When** they enter valid data for first name, last name, address, city, and telephone, **Then** the owner is successfully created and the user is redirected to the owner list page.

---

### User Story 3 - Handle Owner Creation Errors (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then an error message is displayed and the user remains on the creation form.

**Why this priority**: Ensures data integrity and provides a good user experience by guiding users to correct input.

**Independent Test**: Can be fully tested by attempting to submit the new owner form with invalid data (e.g., blank fields, incorrect phone format) and verifying that error messages are displayed and the form remains active.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" form, **When** they submit the form with a blank address, **Then** an error message indicating "Address must not be blank" is displayed, and the user remains on the "Add Owner" form.
2. **Given** the user is on the "Add Owner" form, **When** they submit the form with a telephone number that is not 10 digits, **Then** an error message indicating "Telephone must be 10 digits" is displayed, and the user remains on the "Add Owner" form.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? System rejects with validation error.
- What happens when an owner is created or updated with a blank city? System rejects with validation error.
- What happens when an owner is created or updated with an invalid telephone format (not 10 digits)? System rejects with validation error.
- What happens when a pet is created or updated with a blank name? System rejects with validation error.
- What happens when a pet is created or updated without selecting a pet type? System rejects with validation error.
- What happens when a pet is created or updated without providing a birth date? System rejects with validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? System rejects with validation error.
- What happens when a visit date is not in the future? System rejects with validation error.
- What happens when attempting to access or modify data for a non-existent owner ID? System throws `IllegalArgumentException`.
- What happens when attempting to access or modify data for a non-existent pet ID for a given owner? System throws `IllegalArgumentException`.
- What happens when searching for owners with a last name that does not exist in the database? System returns an empty result and displays a "not found" error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with their contact details (address, city, telephone) and associated pets.
- **FR-002**: System MUST allow the update of an existing owner's details, including their contact information and pets.
- **FR-003**: System MUST allow searching for owners by their last name prefix.
- **FR-004**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, city, and telephone.
- **FR-005**: System MUST validate the owner's telephone number to ensure it consists of exactly 10 digits.
- **FR-006**: System MUST allow viewing a list of all owners.
- **FR-007**: System MUST allow viewing the details of a specific owner, including their pets and visits.
- **FR-008**: System MUST allow the creation of a new pet for an existing owner.
- **FR-009**: System MUST allow the update of an existing pet's details.
- **FR-010**: System SHOULD validate pet information during creation or update, including name, birth date, and type.
- **FR-011**: System SHOULD display a form for creating or updating pet details.
- **FR-012**: System SHOULD allow viewing a list of pet types when creating or updating a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal information (name, address, city, telephone) and a collection of their pets.
- **Pet**: Represents an animal owned by a specific owner, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner list completes in under 5 seconds.
- **SC-003**: 95% of owner creation attempts with invalid data are rejected with clear error messages, and the user remains on the form.
- **SC-004**: The system supports displaying up to 100 owners on the owner list page without performance degradation.
- **SC-005**: All mandatory fields for owner and pet creation/update are validated, resulting in a 0% rate of incomplete records being saved.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for common attributes.
- Data persistence will be handled by Spring Data JPA repositories.
- The primary user interface will be a web-based application.
- The system will use standard date formats for input and display.
- The telephone number format validation (10 digits) is sufficient for initial implementation.
- The uniqueness of pet names for a given owner will be enforced at the application level.