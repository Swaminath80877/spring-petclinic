# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last name" field and click "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: This is a fundamental requirement for adding new individuals to the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the owner appears on the owner list page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the "Owners" list page, displaying the newly added owner.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank required field (e.g., last name), **Then** a validation error message is displayed for the blank field, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page and chooses to add a new pet, Then a form is displayed to enter the pet's details, and upon submission with valid data, the pet is associated with the owner.

**Why this priority**: Managing pets is central to the clinic's operations, and adding new pets is a frequent task.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, initiating the "Add Pet" action, filling out the pet form with valid data, and verifying the new pet appears on the owner's details page. Delivers the ability to register a new animal for a client.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** the user navigates to John Doe's owner details page and clicks "Add New Pet", **Then** a form to add a new pet is displayed, including fields for pet name, birth date, and pet type.
2. **Given** the user is on the "Add New Pet" form for owner "John Doe", **When** they enter "Buddy" for the pet name, select a birth date, choose "Dog" as the pet type, and click "Add Pet", **Then** the pet "Buddy" is successfully added to John Doe's record and displayed on the owner details page.

---

### User Story 4 - Handle Duplicate Pet Name for an Owner (Priority: P3)

Given an owner exists with a pet, When a new pet with a duplicate name is added for the same owner, Then an error indicating a duplicate name is shown.

**Why this priority**: Prevents data integrity issues and provides clear feedback to the user.

**Independent Test**: Can be fully tested by adding a pet for an owner, then attempting to add another pet with the exact same name for the same owner, and verifying the error message. Delivers data consistency and user guidance.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" has a pet named "Max", **When** the user attempts to add another pet for "Jane Smith" with the name "Max", **Then** a validation error message is displayed stating "The pet name must be unique for this owner", and the duplicate pet is not added.

### Edge Cases

- What happens when an owner's first name is blank during creation or update? → Validation error.
- What happens when an owner's last name is blank during creation or update? → Validation error.
- What happens when an owner's address is blank during creation or update? → Validation error.
- What happens when an owner's city is blank during creation or update? → Validation error.
- What happens when an owner's telephone number does not match the 10-digit pattern during creation or update? → Validation error.
- What happens when attempting to find or edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet's name is blank during creation or update? → Validation error.
- What happens when a pet type is not selected during pet creation or update? → Validation error.
- What happens when a pet's birth date is null during creation or update? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error indicating the name is already in use.
- What happens when a visit is submitted with a date that is not in the future? → `typeMismatch.visitDate` validation error.
- What happens when attempting to add a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System MUST validate owner information (address, city, telephone) before saving.
- **FR-007**: System MUST validate pet information (name, birth date, type) before saving.
- **FR-008**: System MUST prevent adding a pet with a name that already exists for the same owner.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD populate pet forms with available pet types.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a collection of their pets.
- **Pet**: Represents a pet, including its name, birth date, and type. It is associated with an Owner and can have multiple Visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic, including the date and associated pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an existing owner's record in under 45 seconds.
- **SC-004**: 95% of users successfully add a new owner or pet on their first attempt without encountering validation errors.
- **SC-005**: The system prevents duplicate pet names for the same owner with a clear error message.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for data modeling.
- Standard validation annotations (`@NotBlank`, `@Pattern`) will be used for data integrity.
- The `LocalDate` type will be used for handling dates.
- The system will leverage Spring's built-in validation framework.
- Existing persistence mechanisms (e.g., JPA repositories) will be used for data storage.
- The `OwnerRepository` and `PetTypeRepository` are available for data access.
- The `PetValidator` will be used for pet-specific validation.
- The `VisitController` will handle visit-related operations.
- The `DataIntegrityViolationException` will be handled for duplicate key violations.
- The `IllegalArgumentException` will be thrown for non-existent entity IDs.