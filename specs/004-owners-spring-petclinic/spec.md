# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then the system displays a list of owners whose last names start with the entered value.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for day-to-day operations of the pet clinic.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Smith" into the "Last Name" field and click "Search", **Then** a list of owners whose last names start with "Smith" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist and click "Search", **Then** a message indicating "Owner not found" is displayed, and the user remains on the "Find Owners" page.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then a new owner is created and the user is redirected to the owner's details page.

**Why this priority**: The ability to add new clients is fundamental to the pet clinic's operations.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the redirection to the newly created owner's detail page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** a new owner record is created, and the user is redirected to the details page for that new owner.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank first name, **Then** a validation error message is displayed for the first name field, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and chooses to add a new pet, Then a form is presented to add pet details, and upon submission with valid data, the pet is associated with the owner.

**Why this priority**: Managing pets is a core aspect of the pet clinic's services.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, initiating the "Add Pet" action, filling in valid pet details (name, birth date, type), and verifying the pet is listed under the owner. Delivers the ability to register pets for existing clients.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** the user navigates to John Doe's details page and clicks "Add New Pet", **Then** a form to add a new pet is displayed, pre-populated with owner information and available pet types.
2. **Given** the user is on the "New Pet" form for owner "John Doe", **When** they enter a valid pet name, birth date, and select a pet type, and click "Add Pet", **Then** the new pet is successfully added to John Doe's record and displayed on his details page.

---

### User Story 4 - Handle Duplicate Pet Name for an Owner (Priority: P2)

Given an owner exists and already has a pet named "Buddy", When a user attempts to add another pet with the name "Buddy" for the same owner, Then the system rejects the pet creation and displays a "duplicate" error message for the pet's name.

**Why this priority**: Prevents data inconsistencies and ensures clear identification of pets.

**Independent Test**: Can be fully tested by creating an owner, adding a pet with a specific name, then attempting to add another pet with the exact same name for that owner and verifying the error message. Delivers data integrity for pet names within an owner's record.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" has a pet named "Max", **When** the user attempts to add another pet for "Jane Smith" with the name "Max", **Then** a validation error message "duplicate" is displayed for the pet's name field, and the pet is not created.

---

### User Story 5 - Update an Existing Owner's Information (Priority: P3)

Given an owner exists, When a user navigates to the owner's details page and chooses to edit the owner, Then a form is presented with the owner's current information, and upon submission with valid changes, the owner's record is updated.

**Why this priority**: Allows for correction of errors or updating of client information.

**Independent Test**: Can be fully tested by selecting an existing owner, initiating the edit action, modifying a field (e.g., telephone number), saving the changes, and verifying the updated information on the owner's details page. Delivers the ability to maintain accurate owner records.

**Acceptance Scenarios**:

1. **Given** an existing owner "Robert Johnson" exists, **When** the user navigates to Robert Johnson's details page and clicks "Edit Owner", **Then** an editable form displaying Robert Johnson's current information is shown.
2. **Given** the user is on the "Edit Owner" form for Robert Johnson, **When** they change the telephone number and click "Update Owner", **Then** the owner's record is updated with the new telephone number, and the user is redirected to the updated owner's details page.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with no pet type specified → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.
- **Non-existent Owner ID for Pet Visit**: Attempting to create a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a non-existent pet belonging to an owner → `IllegalArgumentException` thrown.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → `result.rejectValue("lastName", "notFound", "not found")` and returns to the find owners form.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST display a form to create or update a pet, pre-populated with owner and pet types.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD allow finding owners by last name.
- **FR-005**: System SHOULD allow updating a pet's name.
- **FR-006**: System MUST allow creation of new owners.
- **FR-007**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-008**: System MUST allow updating an existing owner's information.
- **FR-009**: System MUST display a list of owners matching a given last name.
- **FR-010**: System MUST display an error message when an owner or pet is not found.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the pet clinic. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal belonging to an owner. Key attributes include name, birth date, and type. A pet can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to their details page is completed in under 5 seconds.
- **SC-003**: Adding a new pet to an owner's record is completed in under 5 seconds.
- **SC-004**: 95% of users successfully create or update owner/pet information without encountering validation errors on the first attempt.
- **SC-005**: The system correctly identifies and prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The "owners" module is the primary focus, and other modules (like vets, visits) will be handled in separate specifications.
- Data persistence will be handled by a relational database.
- The `PetType` entity will have pre-defined values available for selection.
- The telephone number format validation (`\\d{10}`) is sufficient for all regions.