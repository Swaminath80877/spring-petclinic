# Feature Specification: Owner Management

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find and access their information.

**Why this priority**: This is a core functionality for managing owners and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system with last names like "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with a specific last name prefix, **When** a user searches for owners with that prefix, **Then** an empty list or a "no results found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to create a new owner record so that I can register new clients in the system.

**Why this priority**: Essential for onboarding new customers.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they submit a valid owner form with all required fields (first name, last name, address, city, telephone), **Then** the owner is created and the user is redirected to the newly created owner's detail page.
2. **Given** a user is on the "New Owner" form, **When** they submit the form with a blank required field (e.g., last name), **Then** the form is redisplayed with validation errors indicating the missing field.

---

### User Story 3 - Edit an Existing Owner (Priority: P2)

As a clinic staff member, I want to edit an existing owner's details so that I can update their contact information or address.

**Why this priority**: Important for maintaining accurate customer data.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, saving, and verifying the changes.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** the user navigates to the owner's detail page, clicks "Edit", modifies their telephone number, and saves the changes, **Then** the owner's telephone number is updated on their detail page.
2. **Given** an owner exists, **When** the user attempts to edit the owner's address to be blank, **Then** the system rejects the change with a validation error for a blank address.

---

### User Story 4 - Add a New Pet to an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: Core functionality for managing an owner's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the "Add Pet" section, filling out the pet form with valid data, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user navigates to the owner's detail page and selects "Add New Pet", **Then** a form is displayed to enter pet details (name, birth date, type).
2. **Given** the "Add Pet" form is displayed for an owner, **When** the user enters a valid pet name, birth date, and selects a pet type, and submits the form, **Then** the new pet is created and associated with the owner, and the owner's pet list is updated.

---

### User Story 5 - Edit an Existing Pet's Details (Priority: P3)

As a clinic staff member, I want to edit an existing pet's details so that I can update information like their birth date or type.

**Why this priority**: Necessary for maintaining accurate pet records.

**Independent Test**: Can be fully tested by selecting a pet, editing its details, saving, and verifying the changes.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** the user navigates to the pet's detail page and selects "Edit Pet", **Then** a form is displayed pre-populated with the pet's current details.
2. **Given** the "Edit Pet" form is displayed, **When** the user changes the pet's birth date and saves, **Then** the pet's birth date is updated on their detail page.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → System rejects with validation error.
- What happens when an owner is created or updated with a blank last name? → System rejects with validation error.
- What happens when an owner is created or updated with a blank address? → System rejects with validation error.
- What happens when an owner is created or updated with a blank city? → System rejects with validation error.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → System rejects with validation error.
- What happens when attempting to edit or access an owner with an ID that does not exist in the database? → System throws `IllegalArgumentException`.
- What happens when a pet is created or updated with a blank name? → System rejects with validation error.
- What happens when a pet is created or updated without specifying a pet type? → System rejects with validation error.
- What happens when a pet is created or updated with a null birth date? → System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner? → System rejects with validation error.
- What happens when a visit is submitted with a date that is not in the future? → System rejects with validation error.
- What happens when attempting to create a visit for an owner ID that does not exist? → System throws `IllegalArgumentException`.
- What happens when attempting to create a visit for a pet ID that does not exist for the specified owner? → System throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name prefix.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System SHOULD validate pet information before saving.
- **FR-007**: System SHOULD display a form to create or update a pet, pre-populated with owner and pet data if available.
- **FR-008**: System SHOULD provide a list of available pet types for selection during pet creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner with contact and address information. Key attributes include first name, last name, address, city, and telephone number. It has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal belonging to an owner. Key attributes include name, birth date, and type. It has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Key attribute is its name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and subsequent redirection to the owner's detail page completes within 3 seconds.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: The system successfully prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` entity for owner's first and last names.
- The system will use H2 database for development and testing as per project constitution.
- All user-facing strings will be internationalized.
- The `PetType` entity will be pre-populated with common pet types (e.g., Cat, Dog, Bird, Reptile).
- The date format for pet birth dates and visit dates will be `yyyy-MM-dd`.
- The telephone number format is strictly 10 digits.
- The system will handle `IllegalArgumentException` for non-existent IDs gracefully by displaying an appropriate error message to the user.
- The system will use standard Spring Boot validation mechanisms for all fields.
- The system will not handle visit creation or editing as part of this initial owner management feature, focusing on owner and pet data.