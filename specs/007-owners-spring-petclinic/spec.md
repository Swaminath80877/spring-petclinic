# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `007-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then they are redirected to a list of owners matching that last name.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct list of owners is displayed.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" field and click "Search", **Then** the system displays a list of owners whose last name is "Davis".
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist in the system and click "Search", **Then** the system displays a message indicating no owners were found and returns to the "Find Owners" form.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and they are redirected to the owner's details page.

**Why this priority**: This is fundamental to adding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to the newly created owner's details page.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is saved, and the user is redirected to the details page for that owner.

---

### User Story 3 - Handle Owner Creation Errors (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form, Then they are shown the form again with error messages.

**Why this priority**: Ensures data integrity and provides user feedback for corrections.

**Independent Test**: Can be fully tested by navigating to the new owner form, intentionally leaving required fields blank or entering invalid data (e.g., non-numeric phone), submitting the form, and verifying that error messages are displayed and the form remains visible.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they leave the "First Name" field blank and click "Add Owner", **Then** an error message is displayed next to the "First Name" field, and the form remains visible.
2. **Given** the user is on the "New Owner" form, **When** they enter "123" for the "Telephone" field and click "Add Owner", **Then** an error message is displayed indicating an invalid telephone format, and the form remains visible.

---

### User Story 4 - Update Existing Owner Information (Priority: P2)

Given a user is viewing an owner's details page, When they edit the owner's information and submit the form, Then the owner's details are updated and the updated details are displayed.

**Why this priority**: Allows for correction and maintenance of existing owner records.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their details page, clicking an "Edit" button, modifying a field (e.g., address), saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details page for an existing owner, **When** they click the "Edit Owner" button, modify the "Address" field, and click "Update Owner", **Then** the owner's address is updated, and the details page displays the new address.

---

### User Story 5 - Add a New Pet to an Owner (Priority: P3)

Given a user is viewing an owner's details page, When they choose to add a new pet and submit the pet's details, Then the new pet is associated with the owner and displayed on their details page.

**Why this priority**: Essential for managing the full scope of an owner's pets.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the process to add a pet, filling in the pet's details (name, birth date, type), saving it, and verifying the new pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details page for an owner, **When** they click "Add New Pet", fill in the pet's name, birth date, and select a "Pet Type", and click "Add Pet", **Then** the new pet is successfully added to the owner's record and appears in the list of pets on the owner's details page.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist → `IllegalArgumentException` thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → validation error on `lastName` field, returns to find owners form.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.
- **Non-existent Owner for Visit**: Attempting to add a visit for a non-existent owner → `IllegalArgumentException` thrown.
- **Non-existent Pet for Visit**: Attempting to add a visit for a non-existent pet of an owner → `IllegalArgumentException` thrown.
- **Exception Trigger**: Accessing the `/oups` endpoint → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow the updating of existing pet information.
- **FR-003**: System SHOULD validate pet data upon creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet details.
- **FR-005**: System SHOULD populate a list of available pet types for selection.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST allow the creation of new owners.
- **FR-008**: System MUST validate owner data upon creation or update.
- **FR-009**: System MUST display a form for creating or updating owner details.
- **FR-010**: System MUST allow updating of existing owner information.
- **FR-011**: System MUST display a list of owners matching a search query.
- **FR-012**: System MUST display detailed information for a specific owner.
- **FR-013**: System MUST display a list of pets associated with an owner.
- **FR-014**: System MUST allow adding visits for a pet.
- **FR-015**: System MUST validate visit data upon submission.
- **FR-016**: System MUST display a form for adding visits.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (name, address, contact information) and a list of their pets.
- **Pet**: Represents an individual pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Dog, Cat, Hamster).
- **Visit**: Represents a single visit to the clinic for a pet, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Owner information can be updated and reflected on the details page within 5 seconds.
- **SC-004**: New pets can be added to an owner's record and displayed within 10 seconds.
- **SC-005**: 95% of form submissions (owner creation/update, pet creation/update, visit submission) with invalid data result in clear error messages and the form remaining visible for correction.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date formats will be used for input.
- The system will operate within a single timezone for date handling.
- Existing authentication mechanisms (if any) are outside the scope of this feature.
- The primary users are clinic staff responsible for managing owner and pet information.