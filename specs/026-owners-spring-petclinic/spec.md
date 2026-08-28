# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `026-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then they are redirected to the owners list page displaying matching owners.

**Why this priority**: This is a core functionality for users to locate existing pet owners, essential for managing their pets and visits.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known owner's last name, submitting, and verifying the correct owner appears in the results.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" field and click "Search", **Then** the "Owner List" page is displayed showing owners with the last name "Davis".
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "NonExistent") and click "Search", **Then** an appropriate message is displayed indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and they are redirected to the owner's details page.

**Why this priority**: This is fundamental for adding new clients to the clinic's system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting, and verifying the new owner's details page is displayed.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (First Name, Last Name, Address, City, Telephone) with valid data and click "Add Owner", **Then** the new owner is created and the "Owner Details" page for that owner is displayed.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank "First Name", **Then** a validation error is displayed for the "First Name" field, and the form remains on the "New Owner" page.
3. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a telephone number that is not 10 digits, **Then** a validation error is displayed for the "Telephone" field, and the form remains on the "New Owner" page.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and initiates adding a new pet, Then they are presented with a form to enter pet details.

**Why this priority**: Allows clinic staff to associate new pets with existing owners, a common operational task.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their details, and initiating the pet creation process.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** the user navigates to the "Owner Details" page for that owner, **Then** an option to "Add New Pet" is available.
2. **Given** the user clicks "Add New Pet" on an owner's details page, **When** the pet creation form is displayed, **Then** fields for "Name", "Birth Date", and "Pet Type" are present, along with a list of available pet types.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

Given an owner exists with a pet, When a new pet is created with a name that already exists for that owner, Then an error message is displayed indicating the duplicate name, and the form is re-displayed.

**Why this priority**: Prevents data integrity issues and provides clear feedback to the user.

**Independent Test**: Can be fully tested by creating an owner with a pet, then attempting to add another pet with the same name for that owner.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with a pet named "Buddy", **When** the user attempts to add another pet for "John Doe" with the name "Buddy", **Then** a validation error message "The pet name must be unique for each owner" is displayed, and the pet creation form is re-displayed with the entered data.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Find Owner with No Results**: Searching for owners with a last name that yields no results → validation error indicating "not found".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information.
- **FR-003**: System MUST allow searching for owners by last name.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST display an error message when an owner search yields no results.
- **FR-006**: System MUST allow the creation of new pets for an owner.
- **FR-007**: System MUST allow the updating of existing pet information.
- **FR-008**: System SHOULD validate owner data upon creation or update, enforcing constraints on address, city, and telephone.
- **FR-009**: System SHOULD validate pet data upon creation or update, enforcing constraints on name and type.
- **FR-010**: System SHOULD display a form for creating or updating pet details.
- **FR-011**: System SHOULD retrieve a list of available pet types for selection when adding or editing a pet.
- **FR-012**: System MUST prevent the creation of a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. Has a relationship with multiple Pets.
- **Pet**: Represents a pet. Key attributes include name and birth date. Has a relationship with an Owner and a PetType.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Key attribute is its name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name, with results displayed within 2 seconds.
- **SC-002**: New owners can be successfully created and their details viewed within 3 minutes of form submission.
- **SC-003**: New pets can be added to an owner's record, with the pet appearing on the owner's details page within 1 minute of form submission.
- **SC-004**: 95% of users attempting to create a duplicate pet name for an owner receive an immediate, clear error message.
- **SC-005**: The system successfully validates all owner and pet fields according to defined business rules, with validation errors displayed clearly to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The list of pet types is pre-defined and managed elsewhere.
- Data retention policies for owner and pet information are handled by a separate system or are based on industry standards for veterinary clinics.
- The system will be deployed in an environment where database access is reliable and performant.