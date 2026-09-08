# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then the system displays a list of owners whose last names start with the entered value.

**Why this priority**: This is a core functionality for navigating and managing existing owners, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" search field and click "Search", **Then** a list of owners whose last names start with "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist in the system and click "Search", **Then** a "No Owners Found" message is displayed.
3. **Given** the user is on the "Find Owners" page, **When** they leave the "Last Name" search field blank and click "Search", **Then** all owners are displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is a fundamental capability for adding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to the owner's detail page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (First Name, Last Name, Address, City, Telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the owner's details page.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank "Address" field, **Then** a validation error message is displayed for the "Address" field, and the owner is not created.
3. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a telephone number that is not 10 digits, **Then** a validation error message is displayed for the "Telephone" field, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and initiates the process to add a new pet, Then they can provide pet details and save the new pet associated with that owner.

**Why this priority**: Managing pets is a core aspect of the clinic's operations, and adding new pets is a frequent task.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, initiating pet creation, filling in valid pet details, and saving. Delivers the ability to register new pets for existing clients.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user views the owner's details page and clicks "Add New Pet", **Then** a form to add a new pet is displayed, allowing selection of pet type, name, and birth date.
2. **Given** the user is on the "Add New Pet" form for an owner, **When** they enter a valid pet name, select a pet type, and enter a valid birth date, and click "Add Pet", **Then** the new pet is created and associated with the owner, and the owner's details page is updated to show the new pet.
3. **Given** the user is on the "Add New Pet" form for an owner, **When** they attempt to create a pet with a name that already exists for that owner, **Then** a validation error message "duplicate" is displayed for the pet name, and the pet is not created.

---

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

Given a pet exists for an owner, When a user navigates to the pet's details and initiates an update, Then they can modify the pet's information and save the changes.

**Why this priority**: Allows for correction of errors or updating information as a pet's circumstances change.

**Independent Test**: Can be fully tested by selecting an owner, then a pet, initiating an edit, changing a field (e.g., birth date), saving, and verifying the change. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** an owner has an existing pet, **When** the user views the owner's details page and clicks to edit the pet, **Then** a form pre-populated with the pet's current details is displayed.
2. **Given** the user is on the "Edit Pet" form, **When** they modify the pet's birth date and click "Update Pet", **Then** the pet's birth date is updated, and the owner's details page reflects the change.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? **System displays a validation error for the address field.**
- What happens when an owner is created or updated with a blank city? **System displays a validation error for the city field.**
- What happens when an owner is created or updated with an invalid telephone format (not 10 digits)? **System displays a validation error for the telephone field.**
- What happens when an attempt is made to edit or view an owner with a non-existent ID? **An `IllegalArgumentException` is thrown, indicating the owner was not found.**
- What happens when searching for owners with a blank last name? **All owners are returned.**
- What happens when creating or updating a pet with a blank name? **System displays a validation error "required" for the pet name.**
- What happens when creating or updating a pet without selecting a pet type? **System displays a validation error "required" for the pet type.**
- What happens when attempting to save a pet with a name that already exists for the same owner? **System displays a validation error "duplicate" for the pet name.**
- What happens when creating or updating a pet with an invalid birth date format? **System displays a validation error "typeMismatch" for the birth date.**
- What happens when creating or updating a pet with a null birth date? **System displays a validation error for the birth date.**
- What happens when booking a visit with a date that is on or before the current date? **System displays a validation error "typeMismatch.visitDate".**
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? **An `IllegalArgumentException` is thrown, indicating the pet was not found for the owner.**

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the updating of an existing owner's details.
- **FR-003**: System MUST allow the creation of a new pet for a given owner.
- **FR-004**: System MUST allow the updating of an existing pet's details.
- **FR-005**: System SHOULD validate owner information before saving.
- **FR-006**: System SHOULD validate pet information before saving.
- **FR-007**: System SHOULD display a form for creating or updating an owner.
- **FR-008**: System SHOULD display a form for creating or updating a pet.
- **FR-009**: System SHOULD populate a list of available pet types for selection during pet creation/update.
- **FR-010**: System MUST allow searching for owners by last name.
- **FR-011**: System MUST display a list of owners matching a search query.
- **FR-012**: System MUST display a "No Owners Found" message when a last name search yields no results.
- **FR-013**: System MUST allow viewing an owner's details, including their associated pets.
- **FR-014**: System MUST allow adding visits for a pet.

### Key Entities *(include if feature involves data)*

- **Person**: Represents an individual with a first name, last name, address, city, and telephone number.
- **Owner**: Extends Person, representing a pet owner. Can have multiple pets.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Has a name.
- **Pet**: Represents a pet with a name, birth date, and type. Associated with an owner and can have multiple visits.
- **Visit**: Represents a visit to the clinic for a pet, including a visit date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an existing owner in under 2 minutes.
- **SC-004**: 95% of users can successfully create or update owner and pet information without encountering validation errors on the first attempt.
- **SC-005**: The system correctly displays all associated pets when viewing an owner's details.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` entity for owner details.
- The system will use standard web form validation for all input fields.
- The system will use a sequential numbering scheme for new owners and pets if not explicitly provided.
- The system will display user-friendly error messages for validation failures.
- The system will use the `LocalDate` type for pet birth dates and visit dates.
- The system will use a predefined list of `PetType`s.