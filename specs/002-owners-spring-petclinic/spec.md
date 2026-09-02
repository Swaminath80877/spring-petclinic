# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic application usability.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list matches the expected owners, delivering the value of finding specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** no owners are displayed.

---

### User Story 2 - Create a new owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: Adding new owners is a fundamental operation for growing the pet clinic's database.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner appears in the owner list, delivering the value of adding a new client.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Save", **Then** the new owner is saved and the user is redirected to the "Owners List" page, displaying the newly added owner.

---

### User Story 3 - Handle duplicate pet name for an owner (Priority: P3)

Given an owner exists with existing pets, When a user attempts to add a new pet with a name that already exists for that owner, Then an error is displayed indicating the pet name is a duplicate.

**Why this priority**: Prevents data inconsistencies and provides clear feedback to the user, improving the data integrity and user experience.

**Independent Test**: Can be fully tested by adding a pet to an owner, then attempting to add another pet with the same name to that same owner, delivering the value of preventing duplicate pet names for a single owner.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user attempts to add another pet named "Buddy" to "John Doe", **Then** a validation error message "Pet name must be unique for this owner" is displayed, and the pet is not saved.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → System rejects with validation error.
- What happens when an owner is created/updated with a blank city? → System rejects with validation error.
- What happens when an owner is created/updated with a telephone number not matching the 10-digit pattern? → System rejects with validation error.
- What happens when attempting to find or edit an owner with an ID that does not exist? → System throws `IllegalArgumentException`.
- What happens when a pet is created/updated with a blank name? → System rejects with validation error.
- What happens when a pet is created with a missing pet type? → System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner? → System rejects with validation error.
- What happens when a pet is created/updated with an invalid birth date format? → System rejects with validation error.
- What happens when a pet is created/updated with a blank birth date? → System rejects with validation error.
- What happens when a visit is submitted with a date that is not in the future? → System rejects with validation error.
- What happens when attempting to add a visit for a non-existent owner? → System throws `IllegalArgumentException`.
- What happens when attempting to add a visit for a non-existent pet of an existing owner? → System throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow the retrieval of all pet types for populating forms.
- **FR-005**: System SHOULD handle potential data integrity violations when saving pet information.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the updating of an existing owner's details.
- **FR-008**: System MUST validate owner information during creation or update.
- **FR-009**: System MUST allow the creation of a new visit for an existing pet.
- **FR-010**: System MUST allow the updating of an existing visit's details.
- **FR-011**: System MUST validate visit information during creation or update.
- **FR-012**: System MUST disallow the 'id' field and any nested 'id' fields when creating or updating an owner.
- **FR-013**: System MUST disallow the 'id' field and any nested 'id' fields when creating or updating a visit.
- **FR-014**: System MUST ensure a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact information (address, city, telephone) and a list of associated pets.
- **Pet**: Represents an animal owned by an owner, including its birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a record of a pet's visit, including the date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner in under 1 minute.
- **SC-002**: Users can find owners by last name prefix with results displayed in under 2 seconds.
- **SC-003**: 99% of pet creations for an owner are successful without duplicate names.
- **SC-004**: All owner and pet data validation errors are clearly presented to the user upon submission.
- **SC-005**: The system successfully handles 100 concurrent requests for owner and pet data retrieval.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Existing database infrastructure is available and functional.
- The core data structures (BaseEntity, NamedEntity) are correctly implemented and available.
- Standard Spring Boot conventions for dependency injection and configuration will be followed.
- Error messages for validation failures will be user-friendly and informative.
- The system will use a standard relational database for persistence.
- The application will be deployed in an environment where standard Java and Spring Boot applications can run.