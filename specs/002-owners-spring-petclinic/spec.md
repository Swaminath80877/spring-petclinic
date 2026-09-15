# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - View and Manage Owners (Priority: P1)

Users should be able to view a list of owners, search for owners by last name, and view the details of a specific owner. They should also be able to create new owners and edit existing owner information.

**Why this priority**: This is a core functionality for managing the pet clinic's clients and is fundamental to the application's purpose.

**Independent Test**: Can be fully tested by navigating through owner lists, search functionality, and owner detail/edit forms, delivering the ability to manage client data.

**Acceptance Scenarios**:

1. **Given** a list of owners exists, **When** a user searches for owners by a last name prefix (e.g., "Sm"), **Then** a list of owners whose last names start with "Sm" is displayed.
2. **Given** an owner's details are available, **When** a user navigates to the owner's detail page, **Then** all of the owner's information (name, address, phone, pets) is displayed.
3. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields populated, **Then** the owner is created and redirected to the owner's list page.
4. **Given** an existing owner's details are displayed, **When** the user edits the owner's information and submits valid changes, **Then** the owner's details are updated and the updated information is reflected.

---

### User Story 2 - Manage Pets for Owners (Priority: P2)

Users should be able to add new pets to an existing owner, update existing pet details, and view a pet's associated visits. The system should prevent duplicate pet names for the same owner.

**Why this priority**: Managing pet information is crucial for providing veterinary services and is a key aspect of client care.

**Independent Test**: Can be fully tested by adding, editing, and viewing pets associated with an owner, and attempting to create duplicate pet names, delivering the ability to manage pet records.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** a user adds a new pet for that owner with valid details and a unique name, **Then** the pet is successfully added to the owner's record.
2. **Given** an existing pet's details are displayed, **When** the user edits the pet's information and submits valid changes, **Then** the pet's details are updated.
3. **Given** an owner exists, **When** a user attempts to create a pet with a name that already exists for that owner, **Then** an error message indicating a duplicate name is displayed, and the pet is not created.

---

### User Story 3 - Manage Visits for Pets (Priority: P3)

Users should be able to add new visits for a pet, and view a pet's visit history.

**Why this priority**: Tracking visits is essential for veterinary care and maintaining a history of a pet's health.

**Independent Test**: Can be fully tested by adding a visit to a pet and viewing the visit history, delivering the ability to track pet appointments.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a user adds a new visit for that pet with a valid date, **Then** the visit is successfully recorded and associated with the pet.
2. **Given** a pet has associated visits, **When** a user views the pet's details, **Then** the list of the pet's visits, including dates, is displayed.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → system rejects with validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → system rejects with validation error.
- **Blank Address**: Owner creation or update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation or update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → system rejects with validation error.
- **Non-existent Owner**: Attempting to edit or find a non-existent owner by ID → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation or update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation or update without specifying a pet type → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner for Visit**: Attempting to create a visit for a non-existent owner → system throws `IllegalArgumentException`.
- **Non-existent Pet for Visit**: Attempting to create a visit for a non-existent pet belonging to an owner → system throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST display the details of a specific owner.
- **FR-006**: System MUST allow the creation of a new pet for an existing owner.
- **FR-007**: System MUST allow the update of an existing pet's details.
- **FR-008**: System MUST display a form for creating or updating pet details.
- **FR-009**: System MUST populate a dropdown with available pet types when creating or updating a pet.
- **FR-010**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-011**: System MUST allow the creation of a new visit for an existing pet.
- **FR-012**: System MUST display a list of visits for a specific pet.
- **FR-013**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-014**: System MUST validate pet information (name, type, birth date) before saving.
- **FR-015**: System MUST validate visit information (date) before saving.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the pet clinic. Includes name, address, city, telephone, and a list of associated pets.
- **Pet**: Represents an animal belonging to an owner. Includes name, birth date, type, and a set of associated visits.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat). Includes a name.
- **Visit**: Represents an appointment or consultation for a pet. Includes a date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create and view owner details within 1 minute of starting the process.
- **SC-002**: Users can add a new pet to an owner in under 30 seconds.
- **SC-003**: The system prevents duplicate pet names for the same owner with immediate user feedback.
- **SC-004**: 95% of owner and pet data entry operations complete without validation errors when valid data is provided.
- **SC-005**: The system displays owner and pet information accurately and without errors.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Existing pet types (e.g., Dog, Cat) will be pre-populated or managed separately.
- The system will use standard date formats for input and display.
- Error messages will be user-friendly and informative.