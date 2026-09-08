# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

**Description**: As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing and accessing owner data, essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** the system has multiple owners with different last names, **When** a user enters "Davis" into the "Last Name" search field and clicks "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** the system has no owners with the last name "Smith", **When** a user enters "Smith" into the "Last Name" search field and clicks "Search", **Then** a message indicating "notFound" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

**Description**: As a clinic staff member, I want to create a new owner record so that I can register new clients and their pets.

**Why this priority**: This is fundamental to onboarding new customers into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they enter valid details for first name, last name, address, city, telephone, and submit the form, **Then** the new owner is created and the user is redirected to the owner's list page, displaying the newly added owner.
2. **Given** the user is on the "New Owner" form, **When** they enter a telephone number that does not conform to the 10-digit pattern, **Then** a validation error is displayed for the telephone field, and the owner is not created.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

**Description**: As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their pets' information and visits.

**Why this priority**: This is a common operation for existing clients who acquire new pets.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet list, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an existing owner exists in the system, **When** the user navigates to the owner's details page, selects "Add New Pet", and submits a form with a valid pet name, birth date, and pet type, **Then** the new pet is associated with the owner and displayed in their pet list.
2. **Given** an owner already has a pet named "Buddy", **When** the user attempts to add another pet for the same owner with the name "Buddy", **Then** a validation error is displayed indicating a duplicate pet name, and the new pet is not added.

---

### User Story 4 - Update an Existing Pet's Information (Priority: P2)

**Description**: As a clinic staff member, I want to update an existing pet's information so that I can keep their records accurate.

**Why this priority**: Ensures that pet details like name, birth date, or type can be corrected if entered incorrectly or changed.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an existing pet is associated with an owner, **When** the user navigates to the pet's details page, modifies the pet's birth date, and submits the changes, **Then** the pet's birth date is updated in the system.
2. **Given** an existing pet is associated with an owner, **When** the user navigates to the pet's details page and attempts to change the pet's name to a blank value, **Then** a validation error is displayed for the pet name, and the changes are not saved.

---

### User Story 5 - Record a Visit for a Pet (Priority: P3)

**Description**: As a clinic staff member, I want to record a visit for a pet so that I can maintain a history of their medical care.

**Why this priority**: Essential for tracking a pet's medical history and providing continuity of care.

**Independent Test**: Can be fully tested by selecting a pet, navigating to the visit recording form, and submitting a new visit with valid details.

**Acceptance Scenarios**:

1. **Given** an existing pet exists for an owner, **When** the user navigates to the pet's details page, selects "Add New Visit", and submits a form with a valid date and description, **Then** the new visit is recorded and associated with the pet.
2. **Given** an existing pet exists for an owner, **When** the user attempts to create a visit with a date in the past, **Then** a validation error is displayed for the visit date, and the visit is not recorded.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error indicating "required".
- **Missing Pet Type**: Pet creation with a missing pet type → validation error indicating "required".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating "duplicate".
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format (e.g., "2015/02/12") → validation error indicating "typeMismatch".
- **Blank Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error indicating "typeMismatch.visitDate".
- **Non-existent Owner ID for Visit**: Attempting to create a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Find Owners with No Results**: Searching for owners with a last name that does not match any records → validation error indicating "notFound".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including name, birth date, and pet type.
- **FR-004**: System MUST allow updating an existing pet's information (name, birth date, type).
- **FR-005**: System MUST allow recording a new visit for a pet, including date and description.
- **FR-006**: System SHOULD validate owner data upon creation or update according to defined business rules (BR-001 to BR-005).
- **FR-007**: System SHOULD validate pet data upon creation or update according to defined business rules (BR-006, BR-008).
- **FR-008**: System SHOULD validate visit data upon creation according to defined business rules (BR-007).
- **FR-009**: System SHOULD display a list of pet types when creating or updating a pet.
- **FR-010**: System SHOULD handle potential data integrity violations during pet operations.
- **FR-011**: System MUST display a "notFound" message when a search for owners yields no results.
- **FR-012**: System MUST throw an `IllegalArgumentException` when attempting operations with non-existent owner IDs.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, pet type, and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog). Key attribute is its name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name, with search results displayed in under 2 seconds.
- **SC-002**: New owner creation is completed successfully in under 1 minute, including validation.
- **SC-003**: Adding a new pet to an owner is completed successfully in under 1 minute, including validation.
- **SC-004**: Recording a visit for a pet is completed successfully in under 1 minute, including validation.
- **SC-005**: 99% of all data entry operations (owner, pet, visit) pass validation on the first attempt due to clear error messages.
- **SC-006**: The system handles 100 concurrent users performing owner and pet management tasks without performance degradation.

## Assumptions

- Users performing these operations are clinic staff with appropriate permissions.
- The underlying database is available and responsive.
- Standard web browser functionality is assumed for user interaction.
- The `spring-petclinic.model` module provides necessary base entities like `BaseEntity` and `NamedEntity`.
- The `spring-petclinic.owner` module provides the core domain classes (`Owner`, `Pet`, `PetType`, `Visit`).
- Data validation constraints defined in the `Owner.java` and `Pet.java` files are to be enforced.
- The `\d{10}` pattern for telephone numbers is the definitive requirement.
- The `yyyy-MM-dd` format is the definitive requirement for `LocalDate` fields.
- The "notFound" message for owner searches is a user-facing indicator.
- `IllegalArgumentException` is the expected exception for invalid IDs.
- The "required" and "duplicate" validation messages for pets are the expected user feedback.
- The "typeMismatch" validation for dates and the "required" validation for pet types are the expected user feedback.
- The "typeMismatch.visitDate" validation message is the expected user feedback for invalid visit dates.
- The "notFound" message for owner searches is a user-facing indicator.
- `IllegalArgumentException` is the expected exception for invalid IDs.
- The "required" and "duplicate" validation messages for pets are the expected user feedback.
- The "typeMismatch" validation for dates and the "required" validation for pet types are the expected user feedback.
- The "typeMismatch.visitDate" validation message is the expected user feedback for invalid visit dates.