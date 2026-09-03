# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owner information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the displayed list of owners.

**Acceptance Scenarios**:

1.  **Given** the system has multiple owners with different last names, **When** a user enters a last name that matches one or more owners, **Then** the system displays a list of owners whose last names start with the entered value.
2.  **Given** the system has owners, **When** a user enters a last name that does not match any existing owners, **Then** the system displays a "not found" error message.
3.  **Given** the system has owners, **When** a user submits the find form without entering a last name, **Then** the system displays a list of all owners.
4.  **Given** the system has multiple owners with the same partial last name, **When** a user enters that partial last name, **Then** the system displays a paginated list of matching owners.
5.  **Given** the system has exactly one owner matching a partial last name, **When** a user enters that partial last name, **Then** the system redirects directly to that owner's detail page.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record so that I can register new clients.

**Why this priority**: This is fundamental to onboarding new clients into the system.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in valid owner details, submitting the form, and verifying the new owner appears in the system and on their detail page.

**Acceptance Scenarios**:

1.  **Given** a user is on the "Add Owner" form, **When** they enter valid owner details (first name, last name, address, city, telephone) and submit the form, **Then** a new owner record is created and the user is redirected to the newly created owner's detail page.
2.  **Given** a user is on the "Add Owner" form, **When** they attempt to submit the form with blank required fields (first name, last name, address, city), **Then** the system rejects the submission and displays validation errors for the blank fields.
3.  **Given** a user is on the "Add Owner" form, **When** they attempt to submit the form with an invalid telephone number format (not 10 digits), **Then** the system rejects the submission and displays a validation error for the telephone field.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: This is a common task for managing client information and is important for pet care tracking.

**Independent Test**: Can be fully tested by navigating to an existing owner's detail page, initiating the "Add Pet" action, filling in valid pet details (name, birth date, type), and verifying the pet is added to the owner's record.

**Acceptance Scenarios**:

1.  **Given** an owner exists, **When** a user navigates to the owner's detail page and adds a new pet with a unique name, valid birth date, and selected pet type, **Then** the new pet is successfully added to the owner's record and displayed on their detail page.
2.  **Given** an owner exists, **When** a user attempts to add a new pet with a blank name, **Then** the system rejects the submission and displays a validation error for the pet's name.
3.  **Given** an owner exists, **When** a user attempts to add a new pet without selecting a pet type, **Then** the system rejects the submission and displays a validation error for the pet type.
4.  **Given** an owner exists, **When** a user attempts to add a new pet with an invalid birth date, **Then** the system rejects the submission and displays a validation error for the birth date.

---

### User Story 4 - Handle Duplicate Pet Name for an Owner (Priority: P2)

As a clinic staff member, I want the system to prevent adding a pet with a name that already exists for the same owner, so that pet names are unique per owner.

**Why this priority**: Ensures data integrity and avoids confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by adding a pet to an owner, then attempting to add another pet to the *same* owner with the *exact same name*, and verifying the error message.

**Acceptance Scenarios**:

1.  **Given** an owner has an existing pet named "Buddy", **When** a user attempts to add another pet for the same owner with the name "Buddy", **Then** the system rejects the new pet creation and displays a "duplicate" error message for the pet's name.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P3)

As a clinic staff member, I want to update an existing pet's details so that the information remains accurate.

**Why this priority**: Important for maintaining up-to-date records.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, selecting a pet, editing its details (name, birth date, type), and verifying the changes are saved.

**Acceptance Scenarios**:

1.  **Given** an owner has an existing pet, **When** a user navigates to the pet's details and updates its name, birth date, or pet type, **Then** the pet's details are successfully updated and reflected on the owner's detail page.
2.  **Given** a user is editing a pet's details, **When** they attempt to save with a blank pet name, **Then** the system rejects the update and displays a validation error for the pet's name.
3.  **Given** a user is editing a pet's details, **When** they attempt to save without selecting a pet type, **Then** the system rejects the update and displays a validation error for the pet type.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → system rejects with validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → system rejects with validation error.
- **Blank Address**: Owner creation or update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation or update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → system rejects with validation error.
- **Non-existent Owner for Pet Addition**: Attempting to add a pet to an owner ID that does not exist → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation or update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with a "duplicate" error.
- **Non-existent Owner for Visit**: Attempting to add a visit for a non-existent owner ID → system throws `IllegalArgumentException`.
- **Non-existent Pet for Visit**: Attempting to add a visit for a non-existent pet ID for a given owner → system throws `IllegalArgumentException`.
- **Unspecified Last Name in Find Form**: Submitting the owner find form without a last name → system treats it as a broad search and returns all owners.
- **No Owners Found**: Owner find form submitted with a last name that does not match any existing owners → system displays a "not found" error.
- **Single Owner Found**: Owner find form submitted with a last name that matches exactly one owner → system redirects to that owner's detail page.
- **Multiple Owners Found**: Owner find form submitted with a last name that matches multiple owners → system displays a paginated list of owners.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-006**: System MUST validate pet information (name, birth date, type) before saving.
- **FR-007**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-008**: System MUST allow searching for owners by last name.
- **FR-009**: System MUST display a list of pet types when creating or updating a pet.
- **FR-010**: System SHOULD handle cases where an owner is not found when attempting to add a pet or visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and pet type. Has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the clinic. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to detail page completes in under 5 seconds.
- **SC-003**: Adding a new pet to an owner is completed and reflected on the owner's detail page in under 4 seconds.
- **SC-004**: 95% of owner and pet data entry operations are successful on the first attempt due to clear validation.
- **SC-005**: System supports up to 500 concurrent users performing owner and pet management tasks without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` base class for owner details.
- The system will use standard web form validation for input fields.
- The system will display a paginated list for owner searches returning multiple results.
- The system will redirect directly to an owner's detail page if only one owner matches a search query.
- The system will display a "not found" message if no owners match a search query.
- The system will display all owners if the search form is submitted without a last name.
- The system will use a standard date picker for pet birth dates.
- The system will present a dropdown or similar selection mechanism for pet types.
- The system will handle `IllegalArgumentException` for non-existent owner or pet IDs when attempting related operations.