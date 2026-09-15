# Feature Specification: Owner Management

**Feature Branch**: `[001-owner-management]`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their details.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a known last name, and verifying that the correct owner's details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system,
   **When** a user searches for owners with the last name "Franklin",
   **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** no owners exist with the last name "Smith",
   **When** a user searches for owners with the last name "Smith",
   **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to be able to create a new owner record so that I can onboard new clients.

**Why this priority**: Essential for adding new customers to the system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting, and verifying the new owner appears in the owner list and their details page is accessible.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form,
   **When** they submit a valid owner form with all required fields filled,
   **Then** the owner is created, and a success message is displayed, and the user is redirected to the owner's details page.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to update an existing owner's details so that I can keep their information current.

**Why this priority**: Important for maintaining accurate customer data.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their edit form, making a change, submitting, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an existing owner record,
   **When** a user updates the owner's telephone number and submits the form,
   **Then** the owner's telephone number is updated, and the change is reflected on the owner's details page.

---

### User Story 4 - Add a New Pet to an Owner (Priority: P3)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage their animals.

**Why this priority**: Core functionality for managing a client's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with valid details, and verifying the pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an existing owner,
   **When** a user adds a new pet with a valid name and type,
   **Then** the pet is associated with the owner and appears in the owner's pet list.

---

### User Story 5 - Handle Invalid Owner Creation (Priority: P3)

As a clinic staff member, I want to receive clear feedback when submitting an invalid owner form so that I can correct the errors.

**Why this priority**: Ensures data integrity and guides users to correct input.

**Independent Test**: Can be fully tested by navigating to the new owner form, intentionally leaving a required field blank or entering invalid data, and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form,
   **When** they submit an invalid owner form (e.g., blank first name),
   **Then** the system displays an error message indicating the invalid field and returns the user to the form.

---

### Edge Cases

- What happens when an owner's first name is blank during creation or update? → System rejects with validation error.
- What happens when an owner's last name is blank during creation or update? → System rejects with validation error.
- What happens when an owner's address is blank during creation or update? → System rejects with validation error.
- What happens when an owner's city is blank during creation or update? → System rejects with validation error.
- What happens when an owner's telephone number does not match the `\d{10}` pattern during creation or update? → System rejects with validation error.
- What happens when attempting to edit or access an owner with an ID that does not exist in the database? → System throws `IllegalArgumentException`.
- What happens when a pet's name is blank during creation or update? → System rejects with validation error.
- What happens when a pet is created or updated without selecting a pet type? → System rejects with validation error.
- What happens when a pet is created or updated with a null birth date? → System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner? → System rejects with validation error.
- What happens when a visit is submitted with a date that is not in the future? → System rejects with validation error.
- What happens when attempting to book a visit for an owner ID that does not exist? → System throws `IllegalArgumentException`.
- What happens when attempting to book a visit for a pet ID that does not exist for the specified owner? → System throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow searching for owners by last name.
- **FR-004**: System MUST display owner details upon successful search.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner.
- **FR-006**: System MUST allow the update of an existing pet's details.
- **FR-007**: System SHOULD validate owner information before saving.
- **FR-008**: System SHOULD display a form for creating or updating owner information.
- **FR-009**: System SHOULD populate pet types when displaying the pet creation/update form.
- **FR-010**: System MUST disallow the 'id' field and any fields containing 'id' when creating or updating an owner.
- **FR-011**: System MUST disallow the 'id' field and any fields containing 'id' when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns one or more pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal belonging to an owner. Attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog, Hamster). Attributes include name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 5 seconds.
- **SC-002**: New owner creation and updates are completed within 10 seconds.
- **SC-003**: 95% of owner data entries are valid according to defined business rules.
- **SC-004**: Users can add a new pet to an owner in under 1 minute.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed by clinic staff with appropriate permissions.
- Existing data for owners and pets will be migrated or available.
- The primary language for the application is English.
- The telephone number format `\d{10}` is sufficient for all regions.
- The date format `yyyy-MM-dd` is universally applicable.
- The system will be deployed in an environment where Spring Boot applications can run.
- The `spring-petclinic` project structure and existing modules will be maintained.
- The `owners` module is the primary focus for this specification.
- No specific performance targets beyond reasonable web application expectations are defined for this initial phase.
- Error messages will be user-friendly and informative.
- The `id` fields are auto-generated by the persistence layer and should not be provided by the user.
- The `PetType` entity will have pre-populated values.
- The `Visit` entity will have a future date validation.
- Non-existent IDs will result in `IllegalArgumentException` as per existing patterns.
- Duplicate pet names for the same owner will be rejected with a validation error.