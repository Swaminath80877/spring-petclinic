# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then they are redirected to the owners list page displaying matching owners.

**Why this priority**: This is a core functionality for navigating and managing existing owner data, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, submitting, and verifying the displayed list. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" field and click "Search", **Then** the "Owner List" page is displayed showing all owners with the last name "Davis".
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "NonExistent") and click "Search", **Then** the "Owner List" page is displayed with a message indicating no owners found.

---

### User Story 2 - Create a new owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and they are redirected to the owner's details page.

**Why this priority**: This is fundamental for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting, and verifying redirection to the newly created owner's details page. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the "Owner Details" page for the newly created owner.

---

### User Story 3 - Handle duplicate pet name creation (Priority: P2)

Given an owner has an existing pet with a specific name, When a new pet is created for the same owner with the same name, Then an error is displayed indicating the name is a duplicate.

**Why this priority**: Prevents data inconsistencies and ensures accurate pet identification within an owner's record.

**Independent Test**: Can be fully tested by creating an owner, adding a pet with a specific name, then attempting to add another pet for the same owner with the identical name and verifying the error message. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user attempts to add another pet for "John Doe" with the name "Buddy", **Then** an error message "The pet name must be unique for a given owner" is displayed, and the pet is not created.

---

### User Story 4 - Update an existing pet's details (Priority: P2)

Given a user is viewing an owner's details, When they select a pet to edit and submit updated information, Then the pet's details are updated and the owner's details page reflects the changes.

**Why this priority**: Allows for correction of errors or updating information for existing pets.

**Independent Test**: Can be fully tested by navigating to an owner's details, selecting a pet, modifying a field (e.g., birth date), submitting, and verifying the updated information on the owner's details page. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" has a pet "Max" with birth date "2020-05-10", **When** the user navigates to "Max"'s details, changes the birth date to "2020-06-15", and clicks "Update Pet", **Then** the owner's details page shows "Max" with the birth date "2020-06-15".

---

### User Story 5 - Create a new pet for an existing owner (Priority: P3)

Given a user is viewing an owner's details, When they choose to add a new pet and submit valid pet information, Then the new pet is associated with the owner and displayed on the owner's details page.

**Why this priority**: Allows owners to register new pets with the clinic.

**Independent Test**: Can be fully tested by navigating to an owner's details, initiating the "Add Pet" process, filling in valid pet information, submitting, and verifying the new pet appears on the owner's details page. Delivers the ability to add new pets to an owner's record.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details for owner "Alice Wonderland", **When** they click "Add New Pet", fill in the pet's name "Cheshire", select a "Cat" type, and provide a birth date, and click "Add Pet", **Then** "Cheshire" appears in the list of pets for "Alice Wonderland".

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → System rejects with validation error.
- What happens when an owner is created or updated with a blank last name? → System rejects with validation error.
- What happens when an owner is created or updated with a blank address? → System rejects with validation error.
- What happens when an owner is created or updated with a blank city? → System rejects with validation error.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → System rejects with validation error.
- What happens when attempting to edit or access an owner with an ID that does not exist in the database? → System throws `IllegalArgumentException`.
- What happens when a pet is created or updated with a blank name? → System rejects with validation error.
- What happens when a pet is created or updated without selecting a pet type? → System rejects with validation error.
- What happens when a pet is created or updated with a null birth date? → System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner? → System rejects with validation error.
- What happens when a visit is submitted with a date that is not in the future? → System rejects with validation error.
- What happens when attempting to book a visit for an owner ID that does not exist? → System throws `IllegalArgumentException`.
- What happens when attempting to book a visit for a pet ID that does not exist for the specified owner? → System throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's details.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet details.
- **FR-005**: System SHOULD populate a dropdown list with available pet types for selection.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details.
- **FR-008**: System MUST allow searching for owners by last name.
- **FR-009**: System MUST display a list of owners matching a search query.
- **FR-010**: System MUST enforce that owner first names are not blank.
- **FR-011**: System MUST enforce that owner last names are not blank.
- **FR-012**: System MUST enforce that owner addresses are not blank.
- **FR-013**: System MUST enforce that owner cities are not blank.
- **FR-014**: System MUST enforce that owner telephone numbers are exactly 10 digits.
- **FR-015**: System MUST enforce that pet names are not blank.
- **FR-016**: System MUST enforce that pet names are unique for a given owner.
- **FR-017**: System MUST enforce that pet types are selected during pet creation/update.
- **FR-018**: System MUST enforce that pet birth dates are valid.
- **FR-019**: System MUST enforce that visit dates are valid.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their contact information and a list of their pets. Key attributes include first name, last name, address, city, and telephone number.
- **Pet**: Represents an individual pet belonging to an owner. Key attributes include name, birth date, and type. It is associated with an Owner and can have multiple Visits.
- **PetType**: Represents the species or breed of a pet (e.g., Cat, Dog, Hamster). It has a name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and description. It is associated with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name and view their details within 5 seconds.
- **SC-002**: New owners can be successfully created and their details viewed within 1 minute of form submission.
- **SC-003**: New pets can be added to an existing owner's record and displayed within 30 seconds.
- **SC-004**: 99% of owner and pet data entries pass validation checks upon submission.
- **SC-005**: The system correctly prevents duplicate pet names for the same owner, providing immediate user feedback.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled outside this module.
- The `spring-petclinic` project's existing database schema and infrastructure will be utilized.
- Default pet types (e.g., Cat, Dog, Hamster) will be pre-populated or managed through a separate configuration.
- The `Person` entity from `org.springframework.samples.petclinic.model` will be used as a base for `Owner` for common fields like first and last name.
- Date formatting for `LocalDate` will follow the `yyyy-MM-dd` pattern as indicated in the repository context.
- Error messages for validation failures will be user-friendly and displayed clearly on the relevant forms.