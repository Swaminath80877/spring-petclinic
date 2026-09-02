# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find and access their information.

**Why this priority**: This is a core functionality for staff to manage and retrieve owner data efficiently.

**Independent Test**: Can be fully tested by entering a last name prefix in the search bar and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with various last names, **When** a user searches for owners by the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** no owners match a specific last name prefix, **When** a user searches for owners by that prefix, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to create a new owner record so that I can register new clients in the system.

**Why this priority**: Essential for onboarding new customers.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled (first name, last name, address, city, telephone), **Then** the owner is created and the user is redirected to the owner's list page, displaying the newly added owner.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., address), **Then** an error message is displayed for the invalid field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P3)

As a clinic staff member, I want to view the details of a specific owner so that I can see all their information, including their pets and visits.

**Why this priority**: Necessary for providing detailed service and information to clients.

**Independent Test**: Can be fully tested by clicking on an owner's name from the owner list and verifying all their details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner exists with associated pets and visits, **When** the user navigates to the owner's details page by clicking on their name, **Then** all owner attributes (name, address, city, telephone) and a list of their pets (with names and types) are displayed.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → Validation error for the `address` field.
- What happens when an owner is created/updated with a blank telephone number? → Validation error for the `telephone` field.
- How does the system handle an invalid telephone format (not 10 digits)? → Validation error for the `telephone` field.
- What happens when a pet is created/updated with a blank name? → Validation error for the `name` field.
- How does the system handle pet creation with a missing pet type? → Validation error for the `type` field.
- What happens when a pet is created/updated with a null birth date? → Validation error for the `birthDate` field.
- How does the system handle attempting to add a pet with a name that already exists for the same owner? → Validation error indicating the name is already in use for that owner.
- What happens when attempting to access or modify data for a non-existent owner ID? → `IllegalArgumentException` indicating the owner was not found.
- What happens when attempting to access or modify a pet associated with an owner, where the pet ID does not exist for that owner? → `IllegalArgumentException` indicating the pet was not found for the owner.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST display detailed information for a selected owner.
- **FR-006**: System MUST allow the creation of a new pet for an existing owner.
- **FR-007**: System MUST allow updating an existing pet's details (name, birth date, type).
- **FR-008**: System SHOULD validate owner information (first name, last name, address, city, telephone) during creation or update.
- **FR-009**: System SHOULD validate pet information (name, birth date, type) during creation or update.
- **FR-010**: System MUST prevent the creation of a pet with a duplicate name for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, and type. A pet can have multiple visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner list completes within 5 seconds.
- **SC-003**: Owner details page loads all owner and pet information within 4 seconds.
- **SC-004**: 95% of new owner creations are successful with valid data.
- **SC-005**: Validation errors for owner and pet data are displayed clearly to the user within 1 second of submission.

## Assumptions

- Users performing these actions are clinic staff members with appropriate permissions.
- The system has a mechanism for storing and retrieving owner and pet data (e.g., a database).
- The `Person` and `NamedEntity` base classes provide necessary common attributes like `id` and `name`.
- The `BaseEntity` class provides a unique identifier for entities.
- The application's locale is set to English by default.
- Standard web browser functionality is assumed for user interaction.
- The telephone number format validation (`\\d{10}`) is sufficient for the project's needs.
- Pet types are pre-defined and managed separately.
- Visit creation is a separate, but related, feature.

## Assumptions

- Users performing these actions are clinic staff members with appropriate permissions.
- The system has a mechanism for storing and retrieving owner and pet data (e.g., a database).
- The `Person` and `NamedEntity` base classes provide necessary common attributes like `id` and `name`.
- The `BaseEntity` class provides a unique identifier for entities.
- The application's locale is set to English by default.
- Standard web browser functionality is assumed for user interaction.
- The telephone number format validation (`\\d{10}`) is sufficient for the project's needs.
- Pet types are pre-defined and managed separately.
- Visit creation is a separate, but related, feature.