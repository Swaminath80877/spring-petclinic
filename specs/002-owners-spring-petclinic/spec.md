# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly find and access their information.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search bar and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists in the system, **When** a user searches for owners by the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** a list of owners exists in the system, **When** a user searches for an owner last name prefix that yields no results (e.g., "XYZ"), **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register myself or a new client with the clinic.

**Why this priority**: This is fundamental for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields (first name, last name, address, city, telephone), **Then** the owner is created and the user is redirected to the owner's list page, showing the newly created owner.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank first name, **Then** a validation error message "required" is displayed next to the first name field, and the form is redisplayed.
3. **Given** a user is on the new owner form, **When** they submit the form with a telephone number that is not 10 digits, **Then** a validation error message "{telephone.invalid}" is displayed next to the telephone field, and the form is redisplayed.

---

### User Story 3 - Add a New Pet to an Owner (Priority: P2)

As a clinic staff member, I want to be able to add a new pet to an existing owner's profile so that I can keep track of all their animals.

**Why this priority**: This is a key feature for managing an owner's pets and is important for providing comprehensive care records.

**Independent Test**: Can be fully tested by navigating to an owner's profile, initiating the "add pet" action, filling out the pet form with valid data, and verifying the pet is added to the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** a user navigates to the owner's profile and initiates the "add pet" action, **Then** a form to create a new pet is displayed.
2. **Given** the new pet form is displayed for an owner, **When** a user submits the form with a valid pet name, birth date, and selects a valid pet type, **Then** the pet is successfully created and associated with the owner, and the owner's pet list is updated.
3. **Given** the new pet form is displayed for an owner, **When** a user submits the form with a blank pet name, **Then** a validation error message "required" is displayed next to the pet name field, and the form is redisplayed.
4. **Given** the new pet form is displayed for an owner, **When** a user submits the form without selecting a pet type, **Then** a validation error message "required" is displayed next to the pet type field, and the form is redisplayed.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

As a clinic staff member, when adding a pet for an owner, I want to be prevented from creating a pet with a name that already exists for that owner, so that pet names remain unique per owner.

**Why this priority**: This ensures data integrity and prevents confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by attempting to add a second pet with the same name as an existing pet for a given owner.

**Acceptance Scenarios**:

1. **Given** an owner exists with a pet named "Buddy", **When** a user attempts to add a new pet for the same owner and enters "Buddy" as the pet name, **Then** a validation error message "duplicate" is shown, and the form is redisplayed without creating the pet.

---

### User Story 5 - Update Existing Pet Information (Priority: P2)

As a clinic staff member, I want to be able to update the information of an existing pet for an owner so that I can correct any errors or update details like birth date or type.

**Why this priority**: This is important for maintaining accurate and up-to-date pet records.

**Independent Test**: Can be fully tested by navigating to an owner's pet list, selecting a pet to edit, modifying its details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an owner exists with a pet, **When** a user navigates to the owner's pet list and selects the pet to edit, **Then** a form pre-populated with the pet's current information is displayed.
2. **Given** the pet edit form is displayed, **When** a user modifies the pet's birth date and saves the changes, **Then** the updated birth date is reflected in the owner's pet list.
3. **Given** the pet edit form is displayed, **When** a user attempts to save with an invalid birth date format (e.g., "2015/02/12"), **Then** a validation error message "typeMismatch" is displayed, and the form is redisplayed.

---

### User Story 6 - View Owner's Pets (Priority: P1)

As a clinic staff member, I want to be able to view a list of all pets belonging to a specific owner so that I can see their complete animal history at a glance.

**Why this priority**: This is a fundamental requirement for providing comprehensive owner and pet management.

**Independent Test**: Can be fully tested by navigating to an owner's profile and verifying that all their associated pets are listed with their key details.

**Acceptance Scenarios**:

1. **Given** an owner exists with multiple pets, **When** a user navigates to the owner's profile page, **Then** a list of the owner's pets is displayed, showing each pet's name, birth date, and type.

---

### User Story 7 - Add a Visit for a Pet (Priority: P2)

As a clinic staff member, I want to be able to add a new visit record for a specific pet so that I can track the history of medical appointments and treatments.

**Why this priority**: This is crucial for maintaining a complete medical history for each pet.

**Independent Test**: Can be fully tested by selecting a pet, initiating the "add visit" action, filling out the visit form with a valid date and description, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a user navigates to the pet's details and initiates the "add visit" action, **Then** a form to create a new visit is displayed.
2. **Given** the new visit form is displayed, **When** a user submits the form with a valid visit date and description, **Then** the visit is successfully recorded and associated with the pet.
3. **Given** the new visit form is displayed, **When** a user submits the form with an invalid visit date (e.g., a date in the past), **Then** a validation error message "typeMismatch.visitDate" is displayed, and the form is redisplayed.
4. **Given** the new visit form is displayed, **When** a user submits the form with a blank visit description, **Then** a validation error message "required" is displayed next to the visit description field, and the form is redisplayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error "required".
- What happens when an owner is created or updated with a blank last name? → Validation error "required".
- What happens when an owner is created or updated with a telephone number that does not consist of exactly 10 digits? → Validation error "{telephone.invalid}".
- What happens when an owner is created or updated with a blank address? → Validation error "required".
- What happens when an owner is created or updated with a blank city? → Validation error "required".
- What happens when attempting to edit or view an owner with an ID that does not exist in the database? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that yields no results? → A validation error "notFound" for the last name field is displayed.
- What happens when creating or updating a pet with a blank name? → Validation error "required".
- What happens when creating a pet with a missing pet type? → Validation error "required".
- What happens when attempting to add a visit for a pet belonging to an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when accessing the "/oups" endpoint? → A `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating existing owner information.
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow updating existing pet information for an owner.
- **FR-006**: System MUST allow viewing a list of pets belonging to an owner.
- **FR-007**: System MUST provide a form to create or update pet details.
- **FR-008**: System MUST allow adding new visits for a pet.
- **FR-009**: System MUST validate owner data before saving (first name, last name, address, city, telephone).
- **FR-010**: System MUST validate pet data before saving (name, type, birth date).
- **FR-011**: System MUST validate visit data before saving (date, description).
- **FR-012**: System SHOULD prevent duplicate pet names for the same owner.
- **FR-013**: System SHOULD provide user-friendly error messages for validation failures.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, containing personal details like name, address, and contact information. It has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal owned by an `Owner`. It includes details such as name, birth date, and type. It has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a medical visit for a `Pet`, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details within 3 seconds.
- **SC-002**: New owner creation and updates are completed within 5 seconds.
- **SC-003**: Adding a new pet to an owner is completed within 5 seconds.
- **SC-004**: Viewing an owner's list of pets is displayed within 3 seconds.
- **SC-005**: Adding a visit for a pet is completed within 5 seconds.
- **SC-006**: Validation errors are displayed to the user immediately upon form submission failure.
- **SC-007**: The system successfully handles at least 100 concurrent requests for owner and pet data without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date and time formats will be used for user input.
- The underlying database is available and responsive.
- The project's existing layered architecture (Controller, Repository, Domain) will be maintained.
- Internationalization (i18n) support for user-facing strings will be handled by externalizing them into resource bundles.