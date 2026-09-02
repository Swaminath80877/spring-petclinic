# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - View and Manage Owners (Priority: P1)

**Description**: As a clinic administrator, I want to be able to view a list of all owners, search for owners by last name, and view the details of a specific owner, so that I can manage owner information effectively.

**Why this priority**: This is a core functionality for managing the clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the owner list, searching by last name, and clicking on an owner to view their details, delivering the ability to find and access owner information.

**Acceptance Scenarios**:

1.  **Given** a list of owners exists, **When** a user searches for owners by a last name prefix (e.g., "S"), **Then** a list of owners whose last names start with "S" is displayed.
2.  **Given** an owner exists, **When** a user clicks on an owner's name from the list, **Then** the owner's details (name, address, city, telephone, and associated pets) are displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

**Description**: As a clinic administrator, I want to be able to create a new owner record by filling out a form with their personal and contact details, so that new clients can be added to the system.

**Why this priority**: Essential for onboarding new clients.

**Independent Test**: Can be fully tested by navigating to the new owner form, submitting valid data, and verifying the owner appears in the owner list, delivering the ability to add new clients.

**Acceptance Scenarios**:

1.  **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and the user is redirected to the owner's list page.
2.  **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., first name, last name, address, city, or telephone), **Then** an error message is displayed for the invalid field, and the owner is not created.
3.  **Given** a user is on the new owner form, **When** they submit the form with an invalid telephone number format (not 10 digits), **Then** a validation error is displayed for the telephone field, and the owner is not created.

---

### User Story 3 - Add and Manage Pets for an Owner (Priority: P2)

**Description**: As a clinic administrator, I want to be able to add new pets to an existing owner's record and ensure that pet names are unique for a given owner, so that accurate pet information is maintained.

**Why this priority**: Managing pet information is crucial for providing veterinary care.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet with valid details, and attempting to add a duplicate pet name, delivering the ability to associate pets with owners and prevent duplicate names.

**Acceptance Scenarios**:

1.  **Given** an owner exists, **When** a user adds a new pet with a unique name and valid details (type, birth date), **Then** the pet is successfully added to the owner's record.
2.  **Given** an owner exists with existing pets, **When** a user attempts to add a new pet with a name that already exists for that owner, **Then** an error is displayed indicating the pet name is a duplicate, and the pet is not added.
3.  **Given** an owner exists, **When** a user attempts to add a new pet with a blank name, **Then** a validation error is displayed, and the pet is not added.
4.  **Given** an owner exists, **When** a user attempts to add a new pet without selecting a pet type, **Then** a validation error is displayed, and the pet is not added.

---

### User Story 4 - Add and Manage Visits for a Pet (Priority: P2)

**Description**: As a clinic administrator, I want to be able to add new visits for a pet, ensuring the visit date is valid, so that a complete history of veterinary care is recorded.

**Why this priority**: Tracking visits is essential for patient care and history.

**Independent Test**: Can be fully tested by selecting a pet, adding a new visit with a future date, and attempting to add a visit with an invalid date, delivering the ability to record pet visit history.

**Acceptance Scenarios**:

1.  **Given** a pet exists for an owner, **When** a user adds a new visit with a valid future date, **Then** the visit is successfully recorded for the pet.
2.  **Given** a pet exists for an owner, **When** a user attempts to add a visit with a date that is on or before the current date, **Then** a validation error is displayed, and the visit is not recorded.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future (i.e., on or before the current date) → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` indicating pet not found.
- **Finding Owners with No Results**: Searching for owners by last name when no matching owners are found → validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name prefix.
- **FR-003**: System MUST display owner details including their associated pets.
- **FR-004**: System MUST allow the creation of a new pet for an owner, including pet name, birth date, and type.
- **FR-005**: System MUST validate that a pet's name is unique for a given owner.
- **FR-006**: System MUST validate that pet information (name, type) is provided during creation or update.
- **FR-007**: System MUST allow the retrieval of all available pet types.
- **FR-008**: System MUST allow the creation of a new visit for a pet, including a visit date.
- **FR-009**: System MUST validate that the visit date is in the future.
- **FR-010**: System MUST handle potential data integrity violations when saving pet information.
- **FR-011**: System MUST display validation errors for blank required fields (owner name, address, city; pet name) and invalid formats (telephone, visit date).
- **FR-012**: System MUST handle requests for non-existent owner or pet IDs gracefully with appropriate error messages.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the veterinary clinic. Includes name, address, city, and telephone number. Can have multiple pets.
- **Pet**: Represents an animal belonging to an owner. Includes name, birth date, and type. Can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a pet. Includes the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details within 3 seconds.
- **SC-002**: New owner records can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an owner's record with unique names and valid details in under 2 minutes.
- **SC-004**: New visits can be recorded for a pet with a future date in under 1 minute.
- **SC-005**: Validation errors for all specified edge cases are clearly displayed to the user, preventing invalid data submission.
- **SC-006**: The system correctly prevents the addition of duplicate pet names for the same owner.

## Assumptions

- Users interacting with the owner management system are clinic administrators or authorized personnel.
- The system will use a relational database for data persistence.
- Standard web browser functionality is assumed for user interaction.
- The date format for pet birth dates and visit dates will be `yyyy-MM-dd`.
- Telephone numbers are expected to be 10 digits without any formatting characters.
- The system will provide user-friendly error messages for validation failures.
- The primary language for user interface messages is English.