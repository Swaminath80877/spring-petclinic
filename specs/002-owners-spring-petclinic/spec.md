# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying that the correct owners are displayed. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" search field and click "Search", **Then** the system displays a list of owners whose last names start with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist in the system and click "Search", **Then** the system displays a "not found" error message.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register myself or a new client with the clinic.

**Why this priority**: This is a fundamental requirement for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying that the new owner is created and their details page is displayed. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid details for first name, last name, address, city, telephone, and submit the form, **Then** a new owner record is created, and I am redirected to the owner's details page.
2. **Given** I am on the "New Owner" form, **When** I leave the "First Name" field blank and submit the form, **Then** a validation error is displayed for the "First Name" field.
3. **Given** I am on the "New Owner" form, **When** I enter an invalid telephone number (e.g., 9 digits) and submit the form, **Then** a validation error is displayed for the "Telephone" field.

---

### User Story 3 - Add a New Pet for an Owner (Priority: P2)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage all of a client's animals.

**Why this priority**: This is a common task for managing client relationships and ensuring all pet information is up-to-date.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, initiating the process to add a new pet, filling in the pet's name, selecting a type, and saving. Delivers the ability to associate new pets with owners.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I choose to add a new pet, fill in the pet's name, select a valid pet type (e.g., "Dog"), and save, **Then** the new pet is associated with the owner and appears in their pet list.
2. **Given** I am viewing the details of an existing owner, **When** I choose to add a new pet and leave the pet's name blank, **Then** a validation error is displayed for the pet's name.
3. **Given** I am viewing the details of an existing owner, **When** I choose to add a new pet and do not select a pet type, **Then** a validation error is displayed for the pet type.

---

### User Story 4 - Update Existing Pet Information (Priority: P2)

As a clinic staff member, I want to be able to update an existing pet's information so that I can correct any errors or reflect changes.

**Why this priority**: Ensures data accuracy and allows for modifications to pet details as needed.

**Independent Test**: Can be fully tested by navigating to an owner's details page, selecting an existing pet, modifying a field (e.g., name), and saving the changes. Delivers the ability to correct or update pet details.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an owner with an existing pet, **When** I select the pet to edit, change its name to "Buddy Jr.", and save, **Then** the pet's name is updated to "Buddy Jr." in the owner's pet list.
2. **Given** I am editing an existing pet's information, **When** I change the pet's name to a blank value and attempt to save, **Then** a validation error is displayed for the pet's name.

---

### User Story 5 - Handle Duplicate Pet Name for an Owner (Priority: P3)

As a clinic staff member, I want the system to prevent me from adding a pet with a name that already exists for the same owner, so that pet names are unique per owner.

**Why this priority**: Prevents data confusion and ensures clear identification of pets within an owner's record.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet with the exact same name to the same owner. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add another pet for the same owner and enter "Buddy" as the name, **Then** the system rejects the addition and displays an error message indicating that a pet with that name already exists for this owner.

---

### User Story 6 - Add a Visit for a Pet (Priority: P3)

As a clinic staff member, I want to be able to add a new visit record for a specific pet so that I can track the pet's medical history.

**Why this priority**: Essential for maintaining a complete medical history for each pet.

**Independent Test**: Can be fully tested by navigating to a pet's details, initiating the addition of a visit, entering a description and date, and saving. Delivers the ability to record pet visits.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of a specific pet, **When** I choose to add a new visit, enter a description (e.g., "Annual check-up") and a future date, and save, **Then** the new visit is recorded and displayed in the pet's visit history.
2. **Given** I am viewing the details of a specific pet, **When** I choose to add a new visit and enter a past date, **Then** a validation error is displayed for the visit date.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with a telephone number that does not match the 10-digit pattern? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created or updated with a blank name? → Validation error.
- What happens when a pet is created or updated without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error indicating the name is already in use.
- What happens when a visit is submitted with a date that is not in the future? → Validation error.
- What happens when attempting to add a visit for a pet belonging to an owner ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when attempting to edit an owner without providing an owner ID? → `IllegalArgumentException` indicating owner not found.
- What happens when searching for owners with a last name that does not exist in the database? → Displays "not found" error message.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow the creation of new pets for an owner.
- **FR-004**: System MUST allow the updating of existing pet information (name, birth date, type).
- **FR-005**: System MUST allow the creation of new visits for a pet.
- **FR-006**: System MUST validate owner data upon creation or update according to defined business rules (BR-001 to BR-005).
- **FR-007**: System MUST validate pet data upon creation or update according to defined business rules (BR-006, BR-007).
- **FR-008**: System MUST validate visit data upon creation or update (e.g., visit date must be in the future, description must not be blank).
- **FR-009**: System MUST display a form for creating or updating owner details.
- **FR-010**: System MUST display a form for creating or updating pet details.
- **FR-011**: System MUST display a form for creating or updating visit details.
- **FR-012**: System MUST populate a list of available pet types for selection when creating or updating a pet.
- **FR-013**: System MUST allow searching for owners by last name.
- **FR-014**: System MUST display a list of owners matching a search query.
- **FR-015**: System MUST display an error message if no owners are found for a given search query.
- **FR-016**: System MUST display an error message if an attempt is made to access or modify a non-existent owner or pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a clinic client, including their personal details (name, address, contact information) and associated pets.
- **Pet**: Represents an animal belonging to an owner, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the different kinds of animals the clinic treats (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a medical visit for a pet, including a description and date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner's details page completes within 5 seconds.
- **SC-003**: Adding a new pet to an owner's record and seeing it reflected on the owner's details page completes within 5 seconds.
- **SC-004**: 99% of all data validation checks (owner, pet, visit) are correctly enforced, preventing invalid data entry.
- **SC-005**: The system successfully prevents the creation of duplicate pet names for the same owner.
- **SC-006**: Support tickets related to incorrect or missing owner/pet information are reduced by 30% within three months of release.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) will be handled separately and are not part of this feature's scope.
- The database schema for owners, pets, pet types, and visits is already defined and accessible.
- The `Person` and `NamedEntity` base classes are available and correctly implemented for inheritance.
- The `LocalDate` type from `java.time` is available for date handling.
- Standard Spring Boot conventions for dependency injection and web handling will be followed.
- Internationalization (i18n) for user-facing strings will be handled as per the project constitution.