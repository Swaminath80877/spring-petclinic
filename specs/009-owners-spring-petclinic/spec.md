# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `009-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for users to locate existing pet owners, enabling further actions like viewing details or adding pets.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a partial last name, submitting, and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Dav" into the "Last Name" field and click "Search", **Then** a list of owners whose last names start with "Dav" (e.g., David, Davis) is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist and click "Search", **Then** a message indicating no owners were found is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is essential for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting, and verifying redirection to the newly created owner's detail page.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields with valid data (first name, last name, address, city, telephone) and click "Add Owner", **Then** the owner is successfully created and the user is redirected to the owner's details page.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank "First Name" field and click "Add Owner", **Then** a validation error message for the "First Name" is displayed, and the form remains on the page.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and chooses to add a new pet, Then a form is presented to enter pet details, and upon submission of valid data, the pet is associated with the owner.

**Why this priority**: Allows existing clients to register new pets within the system, which is a common operation.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their details, initiating the "Add Pet" action, filling in valid pet details, and verifying the new pet appears on the owner's details page.

**Acceptance Scenarios**:

1. **Given** an existing owner is displayed on their details page, **When** the user clicks "Add New Pet", **Then** a form to add a new pet appears, including fields for name, birth date, and pet type selection.
2. **Given** the "Add Pet" form is displayed for an owner, **When** the user enters a valid pet name, birth date, selects a pet type, and clicks "Add Pet", **Then** the new pet is successfully added to the owner's record and displayed on the owner's details page.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

Given an owner exists and has pets, When a user attempts to create a new pet with a name that already exists for that owner, Then an error message indicating a duplicate name is displayed, and the form is re-rendered.

**Why this priority**: Ensures data integrity by preventing duplicate pet names for the same owner.

**Independent Test**: Can be fully tested by creating a pet for an owner, then attempting to create another pet for the same owner with the exact same name, and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** the user attempts to add another pet for the same owner and enters "Buddy" as the pet name, **Then** an error message "The pet name must be unique for a given owner" is displayed, and the pet creation form is re-rendered.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → system rejects with validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → system rejects with validation error.
- **Blank Address**: Owner creation or update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation or update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → system rejects with validation error.
- **Non-existent Owner**: Attempting to find or edit a non-existent owner by ID → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation or update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation or update without specifying a pet type → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit creation or update with a date that is not in the future → system rejects with validation error.
- **Non-existent Pet**: Visit submission for a non-existent pet ID for a given owner → system throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System SHOULD validate owner information during creation or update.
- **FR-007**: System SHOULD validate pet information during creation or update.
- **FR-008**: System SHOULD display a form for creating or updating owner details.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD populate a dropdown list with available pet types for selection when adding or editing a pet.
- **FR-011**: System MUST prevent the creation of a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (name, address, city, telephone) and a list of their pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the different types of pets (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a visit to the clinic for a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: New pets can be added to an existing owner's record in under 1 minute.
- **SC-004**: 99% of owner and pet data entries pass validation checks.
- **SC-005**: The system prevents duplicate pet names for the same owner, with an immediate user-facing error.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) will be handled by other modules.
- Data persistence is handled by the persistence layer and is assumed to be functional.
- The list of available pet types is managed and provided by the system.