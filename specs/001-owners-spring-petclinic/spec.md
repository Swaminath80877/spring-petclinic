# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-10

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for navigating and managing existing owner data, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct owner(s) are displayed.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last name" field and click "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "Xyzzy"), **Then** a message indicating "not found" is displayed, and the user remains on the "Find Owners" page.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: This is fundamental for adding new clients to the clinic's system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting, and verifying the owner is created and visible in the system.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is saved, and the user is redirected to the owner's detail page.
2. **Given** the user is on the "Add Owner" form, **When** they attempt to submit the form with a blank first name, **Then** a validation error message is displayed for the first name field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page, Then all owner attributes are displayed.

**Why this priority**: Allows users to view comprehensive information about a specific owner and their pets.

**Independent Test**: Can be fully tested by finding an existing owner and navigating to their details page to verify all associated information is present.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with associated pets, **When** the user navigates to John Doe's owner details page, **Then** the owner's first name, last name, address, city, telephone, and all associated pets with their details are displayed.

---

### User Story 4 - Update Owner Details (Priority: P2)

Given an owner's details are displayed, When the user modifies and submits the owner's information, Then the owner's details are updated.

**Why this priority**: Allows for correction and maintenance of owner information.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit page, making a change, saving, and verifying the change is reflected.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details of an existing owner, **When** they click the "Edit Owner" button, **Then** they are presented with a form pre-populated with the owner's current information.
2. **Given** the user is on the "Edit Owner" form, **When** they change the owner's telephone number and click "Update Owner", **Then** the owner's telephone number is updated in the system, and the user is redirected to the owner's details page.

---

### User Story 5 - Add a New Pet for an Owner (Priority: P2)

Given an owner's details are displayed, When the user initiates adding a new pet and submits valid pet information, Then the new pet is associated with the owner.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by viewing an owner's details, initiating the add pet process, filling in valid pet details, and verifying the new pet appears under the owner.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's details, **When** they click "Add New Pet", **Then** a form to add a new pet is displayed, including fields for pet name, birth date, and pet type.
2. **Given** the user is on the "Add Pet" form for a specific owner, **When** they enter a valid pet name, select a pet type, and provide a birth date, and click "Add Pet", **Then** the new pet is created and linked to the owner, and the owner's pet list is updated.

---

### User Story 6 - Update an Existing Pet's Details (Priority: P3)

Given a pet's details are displayed, When the user modifies and submits the pet's information, Then the pet's details are updated.

**Why this priority**: Allows for correction and maintenance of pet information.

**Independent Test**: Can be fully tested by viewing an owner's pets, selecting a pet to edit, making a change, saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's pets, **When** they click to edit a specific pet, **Then** a form pre-populated with the pet's current details is displayed.
2. **Given** the user is on the "Edit Pet" form, **When** they change the pet's birth date and click "Update Pet", **Then** the pet's birth date is updated, and the owner's pet list reflects the change.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → `result.rejectValue("lastName", "notFound", "not found")` and returns to the find owners form.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST display owner details, including their pets.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner.
- **FR-006**: System MUST allow the update of an existing pet's details.
- **FR-007**: System SHOULD validate owner information before saving (first name, last name, address, city, telephone).
- **FR-008**: System SHOULD validate pet information before saving (name, birth date, type).
- **FR-009**: System SHOULD display a form for creating or updating owner information.
- **FR-010**: System SHOULD display a form for creating or updating pet information.
- **FR-011**: System SHOULD populate pet types when displaying the pet creation/update form.
- **FR-012**: System MUST display a clear error message when validation fails for owner or pet data.
- **FR-013**: System MUST prevent an owner from having multiple pets with the same name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes fields for first name, last name, address, city, and telephone number. Has a relationship with multiple Pets.
- **Pet**: Represents a pet. Includes fields for name, birth date, and pet type. Has a relationship with an Owner and a PetType.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Has a relationship with multiple Pets.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 30 seconds from form submission to confirmation.
- **SC-003**: 95% of users can successfully add a new pet to an existing owner on their first attempt.
- **SC-004**: Validation errors for owner and pet forms are displayed clearly and immediately upon submission of invalid data.
- **SC-005**: The system correctly displays all associated pets when viewing an owner's details.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for data persistence.
- Standard web browser functionality is assumed for user interaction.
- The project will utilize Spring Boot for application development.
- Existing Spring Data JPA repositories will be leveraged for data access.
- The date format for pet birth dates will be "yyyy-MM-dd".
- The telephone number format for owners will be a 10-digit string.
- The system will provide user-friendly error messages for validation failures.
- The "Find Owners" functionality will match last names starting with the entered text.
- The system will handle concurrent requests for owner and pet data without data corruption.