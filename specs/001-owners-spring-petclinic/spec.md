# Feature Specification: Owner Management

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then the system displays a list of owners whose last names start with the entered value, or redirects to the owner's detail page if only one match is found.

**Why this priority**: This is a core functionality for users to locate existing pet owners, essential for managing their information and pets.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed results or redirection.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the last name field and click "Search", **Then** the system displays a list of owners whose last names start with "Davis".
2. **Given** the user is on the "Find Owners" page, **When** they enter "Franklin" into the last name field and click "Search", **Then** the system redirects to the "Owner Details" page for "Franklin".
3. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not match any owner and click "Search", **Then** an error message "not found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Adding new owners is fundamental to the pet clinic's operations, allowing for new clients to be registered.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting, and verifying the success message and owner creation.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they enter valid first name, last name, address, city, and telephone number, and click "Add Owner", **Then** the owner is created and the user sees a "New Owner Created" success message.
2. **Given** the user is on the "New Owner" form, **When** they enter invalid data (e.g., blank address, invalid phone number) and click "Add Owner", **Then** the system returns to the "New Owner" form with validation errors displayed.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

Given a user is on the owner edit form, When they submit a valid updated owner form, Then the owner's details are updated and the user is redirected to the owner's details page.

**Why this priority**: Allows for the maintenance of existing owner information, ensuring accuracy.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit form, making valid changes, submitting, and verifying the updated details on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's details, **When** they click "Edit Owner", **Then** the "Edit Owner" form is populated with the owner's current information.
2. **Given** the user is on the "Edit Owner" form, **When** they update the address and telephone number with valid data and click "Update Owner", **Then** the owner's details are updated, and the user is redirected to the "Owner Details" page.
3. **Given** the user is on the "Edit Owner" form, **When** they attempt to update with an empty address or telephone number and click "Update Owner", **Then** the system returns to the "Edit Owner" form with validation errors displayed.

---

### User Story 4 - Create a New Pet for an Owner (Priority: P3)

Given a user is on the pet creation form for a specific owner, When they submit a valid pet form, Then the pet is created and associated with the owner.

**Why this priority**: Enables the registration of new pets for existing owners, a core function of the pet clinic.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the pet creation form, filling in valid pet details, and verifying the pet is listed under the owner.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's details, **When** they click "Add New Pet", **Then** the "New Pet" form is displayed, pre-populated with the owner's information and a list of pet types.
2. **Given** the user is on the "New Pet" form, **When** they enter a valid pet name, select a pet type, and provide a birth date, and click "Add Pet", **Then** the pet is created and associated with the owner.
3. **Given** the user is on the "New Pet" form, **When** they attempt to create a pet with a blank name, or a duplicate name for the same owner, **Then** the system rejects the creation and displays a "duplicate name" or "blank name" error for the pet.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P3)

Given a user is on the pet edit form, When they submit a valid updated pet form, Then the pet's details are updated.

**Why this priority**: Allows for the correction or modification of existing pet information.

**Independent Test**: Can be fully tested by selecting a pet, navigating to its edit form, making valid changes, submitting, and verifying the updated details.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's pets, **When** they click "Edit" for a specific pet, **Then** the "Edit Pet" form is displayed, populated with the pet's current information and available pet types.
2. **Given** the user is on the "Edit Pet" form, **When** they update the pet's name, type, or birth date with valid data and click "Update Pet", **Then** the pet's details are updated.
3. **Given** the user is on the "Edit Pet" form, **When** they attempt to update the pet with a blank name or a duplicate name for the same owner, **Then** the system rejects the update and displays an appropriate validation error.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → system rejects with validation error.
- **Non-existent Owner**: Attempting to find or edit a non-existent owner by ID → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → system rejects with validation error.
- **Duplicate Pet Name**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format → system rejects with validation error.
- **Blank Visit Date**: Visit creation/update with a blank date → system rejects with validation error.
- **Visit Date in the Past**: Visit creation/update with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner for Visit**: Attempting to create a visit for a non-existent owner → system throws `IllegalArgumentException`.
- **Non-existent Pet for Visit**: Attempting to create a visit for a non-existent pet of an owner → system throws `IllegalArgumentException`.
- **Missing Translation Keys**: Translation files are not synchronized with the base properties file → system fails with a report of missing keys.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST display a list of owners when multiple match a search, with pagination.
- **FR-005**: System MUST redirect to owner details if only one owner matches a search.
- **FR-006**: System MUST display an error message if no owners are found for a search.
- **FR-007**: System MUST allow the creation of a new pet for an existing owner.
- **FR-008**: System MUST allow the update of an existing pet's details.
- **FR-009**: System SHOULD validate owner information (address, city, telephone) before saving.
- **FR-010**: System SHOULD validate pet information (name, type, birth date) before saving.
- **FR-011**: System SHOULD display a form for creating or updating owner information.
- **FR-012**: System SHOULD display a form for creating or updating pet information.
- **FR-013**: System SHOULD populate a dropdown list with available pet types when creating or updating a pet.
- **FR-014**: System MUST prevent duplicate pet names for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact information (address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, and type.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Existing owner details can be updated successfully in under 1 minute.
- **SC-004**: New pets can be added to an owner's record in under 1 minute.
- **SC-005**: 99% of form submissions with valid data are processed successfully.
- **SC-006**: Validation errors are displayed clearly and promptly for invalid data.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `BaseEntity` and `NamedEntity` structures for core data.
- Standard web application conventions for form handling and validation will be followed.
- The project will utilize Spring Boot and Spring MVC for web development.
- Data persistence will be handled via Spring Data JPA and an appropriate database.
- Internationalization (i18n) will be managed through standard Spring mechanisms.
- Error messages will be user-friendly and informative.
- The system will handle concurrent updates to owner and pet data gracefully, preventing data corruption.