# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-10

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find an owner by last name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners by last name "Franklin", Then the search results display the owner with the last name "Franklin".

**Why this priority**: This is a core functionality for managing pet clinic data, allowing staff to quickly locate existing owner records.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying the correct owner is displayed.

**Acceptance Scenarios**:

1. **Given** the system has an owner with the last name "Franklin", **When** a user searches for owners using "Franklin" as the last name, **Then** the owner "Franklin" is displayed in the search results.
2. **Given** the system has multiple owners with the last name "Franklin", **When** a user searches for owners using "Franklin" as the last name, **Then** all owners with the last name "Franklin" are displayed in the search results.
3. **Given** no owner with the last name "Smith" exists, **When** a user searches for owners using "Smith" as the last name, **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a new owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form with first name "George" and last name "Davis", Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is essential for onboarding new clients and their pets into the clinic's system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to the owner's detail page.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with first name "George", last name "Davis", address "123 Main St", city "Anytown", and telephone "1234567890", **Then** the owner "George Davis" is created and the user is redirected to their details page.
2. **Given** a user is on the new owner form, **When** they submit a valid owner form with first name "Jane", last name "Doe", address "456 Oak Ave", city "Otherville", and telephone "0987654321", **Then** the owner "Jane Doe" is created and the user is redirected to their details page.

---

### User Story 3 - Handle invalid owner creation (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form (e.g., missing last name), Then an error message is displayed and the form is re-rendered.

**Why this priority**: Ensures data integrity by preventing incomplete or invalid owner records from being saved.

**Independent Test**: Can be fully tested by navigating to the new owner form, leaving a required field blank (e.g., last name), submitting the form, and verifying that an error message is shown and the form remains on the page.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit the form with a blank last name, **Then** an error message indicating "Last name must not be blank" is displayed, and the form is re-rendered with the previously entered data.
2. **Given** a user is on the new owner form, **When** they submit the form with an invalid telephone format (e.g., "123"), **Then** an error message indicating "Telephone must be 10 digits" is displayed, and the form is re-rendered with the previously entered data.
3. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** an error message indicating "Address must not be blank" is displayed, and the form is re-rendered with the previously entered data.

---

### User Story 4 - Add a new pet for an existing owner (Priority: P1)

Given an existing owner, When a user navigates to the owner's details page and initiates adding a new pet, Then a form is presented to enter pet details.

**Why this priority**: Core functionality for managing a pet owner's associated pets.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, and initiating the "Add Pet" action.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Smith", **When** a user navigates to John Smith's details page and clicks "Add Pet", **Then** a form to add a new pet is displayed.
2. **Given** the "Add Pet" form is displayed, **When** the user selects a pet type from the dropdown and enters a pet name, **Then** the pet type and name are correctly populated in the form fields.

---

### User Story 5 - Update an existing pet's details (Priority: P2)

Given an existing pet belonging to an owner, When a user navigates to the pet's details and initiates an update, Then a form is presented to modify pet details.

**Why this priority**: Allows for correction or modification of pet information as it changes.

**Independent Test**: Can be fully tested by selecting an existing pet, navigating to its details, and initiating the "Edit Pet" action.

**Acceptance Scenarios**:

1. **Given** an existing pet "Buddy" belonging to owner "Jane Doe", **When** a user navigates to Buddy's details and clicks "Edit Pet", **Then** a form to edit Buddy's details is displayed, pre-populated with current information.
2. **Given** the "Edit Pet" form is displayed, **When** the user changes the pet's birth date and selects a different pet type, **Then** the updated birth date and pet type are reflected in the form.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation or update with a blank name → validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST validate that owner first name, last name, address, and city are not blank.
- **FR-004**: System MUST validate that owner telephone is a 10-digit number.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-006**: System MUST allow the update of an existing pet's details, including pet name, birth date, and pet type.
- **FR-007**: System SHOULD validate pet name is not blank.
- **FR-008**: System SHOULD validate pet birth date is a valid date.
- **FR-009**: System SHOULD validate that a pet name is unique for a given owner.
- **FR-010**: System SHOULD display a form for creating or updating pet details.
- **FR-011**: System SHOULD populate a dropdown list with available pet types when creating or updating a pet.
- **FR-012**: System MUST display appropriate error messages for invalid input during owner and pet creation/update.
- **FR-013**: System MUST handle attempts to access non-existent owner IDs by throwing an `IllegalArgumentException`.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include address, city, and telephone. Has a relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name and birth date. Has a relationship with `PetType` and `Visit`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner in under 1 minute.
- **SC-002**: Owner search results are displayed within 2 seconds for up to 1000 owners.
- **SC-003**: 95% of users successfully create or update pet information without encountering validation errors on the first attempt.
- **SC-004**: The system prevents the creation of duplicate pet names for the same owner.
- **SC-005**: All mandatory fields for owner and pet creation/update are clearly indicated and validated.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet attributes respectively.
- The `PetType` entity will be pre-populated with common pet types (e.g., Cat, Dog, Bird, Rabbit).
- Error messages will be user-friendly and displayed in a consistent manner.
- The system will use standard Spring Boot validation mechanisms.
- The `Visit` entity will be managed separately but is linked to `Pet`.
- The primary database is assumed to be relational.