# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `020-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find and access their information.

**Why this priority**: This is a core functionality for managing owner data and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with various last names, **When** a user searches for owners by the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** a list of owners exists, **When** a user searches for a last name prefix that matches no owners, **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients and expanding the customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is added to the system and appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields (first name, last name, address, city, telephone), **Then** the owner is created and the user is redirected to the owner's list page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., address), **Then** a validation error is displayed for the blank field, and the owner is not created.

---

### User Story 3 - Update Owner Information (Priority: P2)

As a clinic staff member, I want to update an existing owner's information so that I can keep client records accurate.

**Why this priority**: Maintaining accurate client data is crucial for communication and service delivery.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an existing owner is displayed, **When** the user modifies the owner's telephone number and saves the changes, **Then** the owner's telephone number is updated in the system.
2. **Given** an existing owner is displayed, **When** the user attempts to save with an invalid telephone format (e.g., 9 digits), **Then** a validation error is displayed for the telephone field, and the changes are not saved.

---

### User Story 4 - Add a New Pet for an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: Core functionality for managing a pet owner's associated animals.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling in pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user adds a new pet with a unique name, birth date, and pet type, **Then** the pet is successfully associated with the owner.
2. **Given** an owner exists with existing pets, **When** the user attempts to add a new pet with a name that already exists for that owner, **Then** an error is displayed indicating the pet name is a duplicate, and the pet is not added.

---

### User Story 5 - Update Pet Information (Priority: P3)

As a clinic staff member, I want to update an existing pet's information so that I can keep their details current.

**Why this priority**: Ensures accuracy of pet records, important for treatments and history.

**Independent Test**: Can be fully tested by selecting a pet, modifying its details (e.g., birth date, type), saving the changes, and verifying the updated information.

**Acceptance Scenarios**:

1. **Given** an existing pet's details are displayed, **When** the user updates the pet's birth date and saves, **Then** the pet's birth date is updated in the system.
2. **Given** an existing pet's details are displayed, **When** the user attempts to save with a blank pet name, **Then** a validation error is displayed for the pet name, and the changes are not saved.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- How does the system handle an owner's telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet is created/updated with a blank name? → Validation error.
- What happens when a pet is created/updated without selecting a pet type? → Validation error.
- What happens when a pet is created/updated with a null birth date? → Validation error.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that yields no results? → Validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information.
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow the updating of existing pet information.
- **FR-006**: System MUST validate owner data upon creation or update, enforcing non-blank fields for address, city, and telephone (10 digits).
- **FR-007**: System MUST validate pet data upon creation or update, enforcing non-blank names and valid birth dates.
- **FR-008**: System MUST prevent adding a pet with a name that already exists for the same owner.
- **FR-009**: System SHOULD provide a form to create or update pet details.
- **FR-010**: System SHOULD allow fetching an owner by their ID to associate pets.
- **FR-011**: System MUST disallow the ID field for binding when creating or updating an owner.
- **FR-012**: System MUST disallow the ID field for binding when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include address, city, and telephone. Has a one-to-many relationship with Pet.
- **Pet**: Represents a pet belonging to an owner. Attributes include birthDate and name. Has a many-to-one relationship with PetType and a one-to-many relationship with Visit.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and update operations complete within 3 seconds.
- **SC-003**: 95% of new pet additions for an owner are successful on the first attempt.
- **SC-004**: Validation errors for owner and pet data are displayed to the user within 1 second of submission.
- **SC-005**: The system supports managing up to 1000 owners and their associated pets without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `BaseEntity` and `NamedEntity` from `org.springframework.samples.petclinic.model`.
- Data validation for owner and pet fields will follow the patterns and constraints defined in the repository context.
- The system will handle `DataIntegrityViolationException` for data access issues.
- Error messages for validation will be user-friendly and informative.
- The primary user interface for these operations will be web-based.
- The `PetType` entity will be pre-populated or managed separately.
- The `Visit` entity and its associated logic are considered out of scope for this initial owner-focused specification, though relationships are noted.