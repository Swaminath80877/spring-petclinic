# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `013-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit, Then a list of owners with that last name is displayed.

**Why this priority**: This is a core functionality for users to locate existing pet owners, essential for managing their information and pets.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct owner(s) are displayed. Delivers the primary value of owner lookup.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" field and click "Search", **Then** a list of owners with the last name "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "NonExistent") and click "Search", **Then** a message indicating "Owner not found" is displayed.
3. **Given** the user is on the "Find Owners" page, **When** they leave the "Last Name" field blank and click "Search", **Then** all owners are displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: This is fundamental for adding new clients to the clinic's system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting, and verifying the owner appears on the owner list page. Delivers the core value of new client onboarding.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (First Name, Last Name, Address, City, Telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the "Owners" list page, displaying the newly added owner.
2. **Given** the user is on the "New Owner" form, **When** they leave the "First Name" field blank and click "Add Owner", **Then** a validation error message "required" is displayed for the "First Name" field, and the owner is not created.
3. **Given** the user is on the "New Owner" form, **When** they enter an invalid telephone number (e.g., "123") and click "Add Owner", **Then** a validation error message indicating an invalid telephone format is displayed, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page, Then all owner attributes are displayed.

**Why this priority**: Allows clinic staff to access comprehensive information about a specific owner and their pets.

**Independent Test**: Can be fully tested by finding an existing owner, clicking on their name, and verifying all their details (name, address, contact info, and associated pets) are displayed correctly. Delivers the value of detailed owner information access.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with associated pets, **When** the user clicks on "John Doe" from the "Owners" list, **Then** the "Owner Details" page is displayed, showing "John Doe's" first name, last name, address, city, telephone, and a list of their pets with their names and types.
2. **Given** an owner with no pets exists, **When** the user navigates to their "Owner Details" page, **Then** the owner's personal information is displayed, and a message indicating "No pets found" is shown.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P2)

Given a user is viewing an owner's details, When they choose to add a new pet and submit valid pet information, Then the pet is associated with the owner.

**Why this priority**: Essential for managing the pets belonging to existing clients.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the "Add Pet" action, filling in valid pet details (name, birth date, type), submitting, and verifying the new pet appears in the owner's pet list. Delivers the value of pet record management.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details of owner "Jane Smith", **When** they click "Add New Pet", fill in the pet's name as "Buddy", birth date as "2023-05-15", and select "Dog" from the pet type dropdown, and click "Add Pet", **Then** "Buddy" (a Dog) is displayed in Jane Smith's pet list.
2. **Given** the user is viewing the details of owner "Jane Smith", **When** they click "Add New Pet", leave the pet's name blank, and click "Add Pet", **Then** a validation error "required" is displayed for the pet's name.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P3)

Given a user is viewing an owner's pet details, When they choose to edit a pet and submit valid updated information, Then the pet's details are updated.

**Why this priority**: Allows for correction or modification of pet information.

**Independent Test**: Can be fully tested by navigating to an owner's details, selecting a pet to edit, changing a detail (e.g., birth date), submitting, and verifying the change on the owner's pet list. Delivers the value of maintaining accurate pet records.

**Acceptance Scenarios**:

1. **Given** owner "John Doe" has a pet named "Max" (a Dog) with birth date "2020-01-01", **When** the user edits "Max", changes the birth date to "2020-02-02", and clicks "Update Pet", **Then** the pet's birth date is updated to "2020-02-02" in John Doe's pet list.
2. **Given** owner "John Doe" has a pet named "Max", **When** the user attempts to edit "Max" and change its name to a duplicate name already existing for another pet of John Doe, and clicks "Update Pet", **Then** a validation error "duplicate" is displayed for the pet name.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when an owner is created/updated with an invalid telephone format (not 10 digits)? → Validation error.
- What happens when a user attempts to edit or access an owner with a non-existent ID? → `IllegalArgumentException` indicating owner not found.
- What happens when searching for owners with a blank last name? → Returns all records.
- What happens when searching for an owner last name that does not exist? → Validation error "notFound" on `lastName` field.
- What happens when creating or updating a pet with a blank name? → Validation error "required".
- What happens when creating a pet without specifying a type? → Validation error "required".
- What happens when attempting to save a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when creating or updating a pet with a null birth date? → Validation error "required".
- What happens when creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when booking a visit with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to book a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when navigating to the "/oups" endpoint? → Throws a `RuntimeException` and returns an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's details.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD display a form for creating or updating a pet.
- **FR-005**: System SHOULD populate a dropdown list of available pet types when creating or updating a pet.
- **FR-006**: System MUST allow users to find owners by their last name.
- **FR-007**: System MUST allow the creation of a new owner.
- **FR-008**: System MUST display owner details, including their associated pets.
- **FR-009**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-010**: System MUST validate pet information (name, birth date, type) before saving.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and pet type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog, Hamster). Key attribute is its name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include visit date and description. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: Adding a new pet to an existing owner takes less than 45 seconds.
- **SC-004**: 95% of users can successfully navigate to and view owner details without errors.
- **SC-005**: Validation errors for owner and pet forms are displayed clearly and immediately upon submission of invalid data.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet data structures.
- The system will use standard date formats for birth dates and visit dates.
- The system will provide user-friendly error messages for validation failures.
- The system will handle non-existent owner IDs gracefully by returning an appropriate error.
- The system will support a predefined list of pet types.