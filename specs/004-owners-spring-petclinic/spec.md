# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic operations.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying the correct details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the "Find Owners" page and enters "Franklin" in the last name field, **Then** the system displays the details page for the owner named "Franklin".
2. **Given** no owners with the last name "Smith" exist in the system, **When** a user navigates to the "Find Owners" page and enters "Smith" in the last name field, **Then** the system displays a "not found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Adding new owners is fundamental to the application's purpose.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner is added and a success message appears.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone, and click "Submit", **Then** the new owner is saved to the system and the user is redirected to the owner's details page or a success confirmation.
2. **Given** a user is on the "Add Owner" form, **When** they enter invalid details (e.g., blank address, invalid phone number), **Then** the system displays validation errors and the owner is not created.

---

### User Story 3 - Handle Duplicate Pet Name Creation (Priority: P2)

Given an owner has a pet named "Buddy", When a user attempts to create a new pet for the same owner with the name "Buddy", Then an error message indicating a duplicate name is displayed.

**Why this priority**: Prevents data integrity issues and provides a clear user experience when adding pets.

**Independent Test**: Can be fully tested by adding a pet to an owner, then attempting to add another pet with the same name to that same owner, and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** a user attempts to add a new pet for the same owner and enters "Buddy" as the pet's name, **Then** the system displays an error message stating that a pet with that name already exists for this owner.

---

### User Story 4 - Update Existing Pet Details (Priority: P2)

Given an existing pet belonging to an owner, When a user updates the pet's details (e.g., name, birth date, type), Then the pet's information is updated successfully.

**Why this priority**: Allows for correction of errors and maintenance of accurate pet information.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Max" with a birth date of "2020-05-15", **When** a user navigates to edit "Max", changes the birth date to "2020-06-20", and saves, **Then** the pet's birth date is updated to "2020-06-20".
2. **Given** an owner has a pet of type "Dog", **When** a user edits the pet and changes its type to "Cat", **Then** the pet's type is updated to "Cat".

---

### User Story 5 - Add a New Pet for an Existing Owner (Priority: P3)

Given an existing owner, When a user adds a new pet for that owner, Then the new pet is associated with the owner.

**Why this priority**: Essential for managing the full lifecycle of a pet within the clinic system.

**Independent Test**: Can be fully tested by selecting an owner and successfully adding a new pet to their record.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** a user navigates to the owner's details page and initiates the process to add a new pet, **Then** the system presents a form to enter new pet details.
2. **Given** an owner and a completed new pet form, **When** the user submits the form, **Then** the new pet is successfully created and linked to the owner.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → system rejects with validation error.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → system rejects with validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner ID**: Attempting to access or modify data for an owner ID that does not exist → system throws `IllegalArgumentException`.
- **Non-existent Pet ID for Owner**: Attempting to access or modify a pet for an owner where the pet ID does not exist → system throws `IllegalArgumentException`.
- **Owner Not Found during Find**: Searching for owners with a last name that does not exist in the database → system returns an empty result and displays a "not found" error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's details.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD populate a list of available pet types when creating or updating a pet.
- **FR-005**: System SHOULD handle cases where an owner is not found when attempting to add or update a pet.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST allow the creation of new owners.
- **FR-008**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-009**: System MUST validate owner's address, city, and telephone number formats.
- **FR-010**: System MUST validate pet's name and birth date.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details like name, address, city, and telephone. It is associated with multiple pets.
- **Pet**: Represents a pet, including its name, birth date, and type. It belongs to an owner and can have multiple visits.
- **PetType**: Represents the classification of a pet (e.g., Dog, Cat).
- **Visit**: Represents a veterinary visit for a pet, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 3 minutes.
- **SC-003**: Pet creation/update operations complete successfully with valid data, with error messages displayed for invalid data within 1 second.
- **SC-004**: 95% of users can successfully add or update pet information without encountering duplicate name errors when the name is unique.
- **SC-005**: The system correctly handles and reports errors for invalid owner and pet data inputs.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The primary language for user interaction is English.
- Data persistence will be handled by a relational database.
- The existing `Person` class will be extended for `Owner` details.
- The `NamedEntity` and `BaseEntity` classes will be used for core data structures.
- Standard validation annotations (`@NotBlank`, `@Pattern`) will be used for input validation.
- Date formats for pet birth dates and visit dates will be `yyyy-MM-dd`.
- The system will use standard Spring Boot conventions for dependency injection and configuration.
- The application will be deployed using Docker.
- Development will be supported by `.devcontainer` configurations.
- The project will adhere to the Spring Petclinic Constitution.