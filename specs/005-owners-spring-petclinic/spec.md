# Feature Specification: Owner Management

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by providing a prefix of their last name. The system should then display a list of all owners whose last names match the provided prefix.

**Why this priority**: This is a core functionality for navigating and managing existing owners, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name prefix (e.g., "Sm"), and verifying that the correct list of owners is displayed. Delivers immediate value for finding existing clients.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system with last names like "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with a last name starting with "Xyz", **When** a user searches for owners with the last name prefix "Xyz", **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

Users should be able to create a new owner by filling out a form with the owner's details. Upon successful submission of valid information, the new owner should be created, and the user should be redirected to the newly created owner's detail page.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields with valid data, submitting the form, and verifying redirection to the owner's detail page.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone, and submit the form, **Then** the owner is successfully created and the user is redirected to the owner's detail page.

---

### User Story 3 - Handle Owner Creation Errors (Priority: P3)

When a user attempts to create a new owner with invalid or incomplete information, the system should display clear error messages indicating the specific fields that need correction. The user should remain on the creation form to correct the errors.

**Why this priority**: Ensures data integrity and provides a good user experience by guiding users to correct mistakes.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, intentionally leaving required fields blank or entering invalid data (e.g., non-numeric phone number), submitting the form, and verifying that error messages are displayed and the form remains visible.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they submit the form with a blank "Last Name" field, **Then** an error message "Last name must not be blank" is displayed next to the Last Name field, and the user remains on the form.
2. **Given** a user is on the "Add Owner" form, **When** they submit the form with a telephone number containing letters, **Then** an error message indicating an invalid telephone format is displayed, and the user remains on the form.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P1)

Users should be able to add a new pet to an existing owner's record. This involves selecting the owner and providing the pet's details, including name, birth date, and type.

**Why this priority**: Core functionality for managing an owner's pets.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their profile, initiating the "Add Pet" action, filling in valid pet details, and verifying the pet is added to the owner's record.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** a user navigates to John Doe's profile, selects "Add Pet", and provides a valid pet name ("Buddy"), birth date ("2020-05-15"), and selects a pet type ("Dog"), **Then** the pet "Buddy" is successfully added to John Doe's record.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P2)

Users should be able to edit and update the name of an existing pet associated with an owner.

**Why this priority**: Allows for correction of pet names if entered incorrectly or if the pet is renamed.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, initiating the edit pet action, changing the pet's name, saving the changes, and verifying the name update.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Fluffy", **When** the user edits the pet's details and changes the name to "Fluffykins", **Then** the pet's name is updated to "Fluffykins".

---

### Edge Cases

- What happens when an owner is created or updated with a telephone number that is not exactly 10 digits? → Validation error.
- How does the system handle an attempt to edit or view an owner using an ID that does not exist in the database? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a name that already exists for the same owner? → Validation error.
- How does the system handle a visit submission with a date that is in the past? → Validation error.
- What happens when a visit is attempted to be added for a pet ID that does not exist for the specified owner? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow owners to be found by their last name.
- **FR-005**: System SHOULD allow the retrieval of a single owner with their associated pets.
- **FR-006**: System MUST enforce that owner first names are not blank.
- **FR-007**: System MUST enforce that owner last names are not blank.
- **FR-008**: System MUST enforce that owner addresses are not blank.
- **FR-009**: System MUST enforce that owner cities are not blank.
- **FR-010**: System MUST enforce that owner telephone numbers are exactly 10 digits.
- **FR-011**: System MUST enforce that pet names are not blank.
- **FR-012**: System MUST enforce that a pet's name is unique within an owner.
- **FR-013**: System MUST allow the creation of a new owner.
- **FR-014**: System MUST display appropriate validation errors when owner creation fails.
- **FR-015**: System MUST allow the creation of a new visit for an existing pet.
- **FR-016**: System MUST validate visit information during creation.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include address, city, telephone, and a list of associated pets.
- **Pet**: Represents an animal owned by an owner. Attributes include birth date, type, and a list of visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a pet, including a date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and redirection to their detail page completes within 3 seconds.
- **SC-003**: Validation errors for owner and pet creation/updates are displayed to the user within 1 second of submission.
- **SC-004**: Adding a new pet to an owner's record is completed and reflected on the owner's profile within 3 seconds.
- **SC-005**: 95% of owner and pet data entries meet all defined business rules and validation constraints.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data persistence is handled by an underlying database, and the system interacts with it via repositories.
- The "owners" module is part of a larger Spring Petclinic application, and its dependencies on other modules (like Model, Persistence, Spring MVC) are assumed to be correctly configured.
- The date format for birth dates and visit dates is consistently `yyyy-MM-dd`.
- The telephone number format is strictly 10 digits, without any country codes or special characters.