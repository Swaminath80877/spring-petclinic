# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-16

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic application usability.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list matches the expected owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** the owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** an empty list or a "no results found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the owner creation form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: This is a fundamental operation for adding new customers to the clinic.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and confirming the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is saved and the user is redirected to the "Owners List" page, displaying the newly added owner.

---

### User Story 3 - Handle Duplicate Pet Name for an Owner (Priority: P2)

Given an owner exists with existing pets, When a user attempts to add a new pet with a name that already exists for that owner, Then an error is displayed indicating the pet name is a duplicate.

**Why this priority**: Prevents data integrity issues and provides clear feedback to the user.

**Independent Test**: Can be tested by adding a pet to an owner, then attempting to add another pet with the same name to that same owner.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user attempts to add another pet for "John Doe" named "Buddy", **Then** a validation error message "Pet name must be unique for this owner" is displayed, and the new pet is not saved.

---

### User Story 4 - Update an Existing Owner (Priority: P2)

Given an owner exists, When a user edits the owner's details and saves, Then the owner's information is updated.

**Why this priority**: Allows for correction of errors or changes in owner information.

**Independent Test**: Can be tested by editing an existing owner's details and verifying the changes are reflected.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists with address "123 Main St", **When** the user navigates to Jane Smith's profile, edits the address to "456 Oak Ave", and saves, **Then** Jane Smith's owner record is updated with the new address.

---

### User Story 5 - Add a New Pet to an Existing Owner (Priority: P3)

Given an owner exists, When a user adds a new pet for that owner, Then the pet is associated with the owner.

**Why this priority**: Essential for managing the full lifecycle of a pet's care at the clinic.

**Independent Test**: Can be tested by selecting an owner and adding a new pet to their record.

**Acceptance Scenarios**:

1. **Given** an owner "Alice Wonderland" exists, **When** the user navigates to Alice Wonderland's profile, adds a new pet with a valid name, birth date, and type, and saves, **Then** the new pet is listed under Alice Wonderland's pets.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address?
  System rejects the operation with a validation error indicating the address cannot be blank.
- What happens when an owner is created or updated with a blank city?
  System rejects the operation with a validation error indicating the city cannot be blank.
- What happens when an owner is created or updated with a telephone number that is not exactly 10 digits?
  System rejects the operation with a validation error indicating the telephone number must be 10 digits.
- What happens when a pet is created or updated with a blank name?
  System rejects the operation with a validation error indicating the pet name cannot be blank.
- What happens when a pet is created or updated without selecting a pet type?
  System rejects the operation with a validation error indicating a pet type must be selected.
- What happens when a pet is created or updated without providing a birth date?
  System rejects the operation with a validation error indicating the birth date is required.
- What happens when attempting to add a pet with a name that already exists for the same owner?
  System rejects the operation with a validation error indicating the pet name must be unique for that owner.
- What happens when a visit date is not in the future?
  System rejects the operation with a validation error indicating the visit date must be in the future.
- What happens when attempting to access or modify data for an owner ID that does not exist?
  System throws an `IllegalArgumentException` and displays an appropriate error message to the user.
- What happens when attempting to access or modify data for a pet ID that does not exist for a given owner?
  System throws an `IllegalArgumentException` and displays an appropriate error message to the user.
- What happens when accessing the `/oups` endpoint?
  System throws a `RuntimeException` and displays a generic error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name prefix.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-007**: System MUST validate pet information (name, birth date, type) before saving.
- **FR-008**: System MUST display a list of pet types when creating or updating a pet.
- **FR-009**: System MUST handle cases where an owner is not found when attempting to add a pet.
- **FR-010**: System MUST handle cases where a pet is not found for an owner when attempting to update or add visits.
- **FR-011**: System MUST prevent duplicate pet names for the same owner.
- **FR-012**: System MUST allow the creation of new visits for a pet.
- **FR-013**: System MUST validate visit information (description, date) before saving.
- **FR-014**: System MUST display an error page when the `/oups` endpoint is accessed.

### Key Entities *(include if feature involves data)*

- **Person**: Represents an individual with a first name, last name, address, city, and telephone number.
- **Owner**: Represents a person who owns pets. Inherits from Person and has a list of associated Pets.
- **Pet**: Represents an animal owned by an Owner. Has a name, birth date, type, and a list of associated Visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Has a name.
- **Visit**: Represents a medical visit for a Pet. Has a date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an owner in under 45 seconds.
- **SC-004**: 95% of form submissions (owner, pet) are successful on the first attempt due to clear validation feedback.
- **SC-005**: The system supports up to 500 concurrent users browsing the owner list without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date and time formats will be used.
- The system will use a relational database for persistence.
- The primary language for the application is English.
- The `/oups` endpoint is intended for testing error handling.
- Existing `Person` and `NamedEntity` base classes will be utilized.
- The `PetType` entity will have pre-populated values (e.g., Cat, Dog).
- The `Visit` entity will have a description field.