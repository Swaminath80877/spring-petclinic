# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `[###-owners-for-spring-petclinic]`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly find their information.

**Why this priority**: This is a core functionality for managing customer relationships and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the correct list of owners is displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" search field and click "Search", **Then** I should see a list of owners whose last name starts with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist (e.g., "XYZ"), **Then** I should see a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register my pet at the clinic.

**Why this priority**: This is fundamental for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and redirected to their details page.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid details (first name, last name, address, city, telephone) and click "Add Owner", **Then** the new owner should be created and I should be redirected to the owner's details page.
2. **Given** I am on the "New Owner" form, **When** I leave the "First Name" field blank and click "Add Owner", **Then** I should see a validation error message for the "First Name" field.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

As an owner, I want to be able to add a new pet to my existing owner profile so that I can manage all my pets under one account.

**Why this priority**: This allows owners to manage multiple pets efficiently, improving their experience.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, initiating the pet creation process, and successfully adding a new pet.

**Acceptance Scenarios**:

1. **Given** I am viewing an existing owner's details page, **When** I click "Add New Pet", **And** I fill in the pet's name, birth date, and select a pet type, **And** I click "Add Pet", **Then** the new pet should be associated with the owner and displayed on their details page.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P2)

As an owner, I want to be prevented from adding a pet with a name that already exists for one of my other pets so that I can maintain unique identification for each pet.

**Why this priority**: Prevents data confusion and ensures each pet can be uniquely identified.

**Independent Test**: Can be fully tested by adding a pet, then attempting to add another pet with the same name for the same owner.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add another pet for the same owner and enter "Buddy" as the name, **Then** I should see a validation error message indicating that a pet with this name already exists for this owner.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P3)

As an owner, I want to be able to update the name of an existing pet so that I can correct any naming errors or change it if needed.

**Why this priority**: Provides flexibility for owners to manage their pet's information accurately.

**Independent Test**: Can be fully tested by navigating to a pet's details, initiating an edit, changing the name, and saving the changes.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Max", **When** I navigate to the pet's details and choose to edit it, **And** I change the name to "Maximilian", **And** I save the changes, **Then** the pet's name should be updated to "Maximilian".

---

### Edge Cases

- What happens when an owner is created/updated with a blank first name? → Validation error.
- What happens when an owner is created/updated with a blank last name? → Validation error.
- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when an owner is created/updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet is created/updated with a blank name? → Validation error "required".
- What happens when a pet is created with a missing pet type? → Validation error "required".
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when a pet is created/updated with an invalid birth date format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when attempting to add a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when attempting to edit an owner without providing an owner ID? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a pet without providing an owner ID? → `IllegalArgumentException` is thrown.
- What happens when attempting to edit a pet without providing an owner ID? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet data during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-007**: System MUST enforce that owner first name is not blank.
- **FR-008**: System MUST enforce that owner last name is not blank.
- **FR-009**: System MUST enforce that owner address is not blank.
- **FR-010**: System MUST enforce that owner city is not blank.
- **FR-011**: System MUST enforce that owner telephone is exactly 10 digits.
- **FR-012**: System MUST enforce that pet name is not blank.
- **FR-013**: System MUST enforce that pet type is selected.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their contact information (address, city, telephone) and a list of associated pets.
- **Pet**: Represents an individual pet, including its name, birth date, and type. It is associated with an owner.
- **PetType**: Represents the different types of pets (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created successfully in under 1 minute.
- **SC-003**: Adding a new pet to an existing owner takes less than 45 seconds.
- **SC-004**: Validation errors for owner and pet creation/updates are displayed immediately upon form submission.
- **SC-005**: 99% of owner searches by last name return accurate results.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity base classes for Owner and Pet respectively.
- Data validation will be handled using Jakarta Bean Validation annotations.
- The primary interface for managing owners and pets will be a web-based UI.
- The system will use a relational database for persistence.
- The telephone number format `\d{10}` is considered a valid and complete phone number for the scope of this feature.
- Pet names are case-sensitive when checking for duplicates.