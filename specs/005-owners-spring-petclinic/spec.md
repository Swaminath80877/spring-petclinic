# Feature Specification: Owner Management

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owners, essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed results, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** a message indicating no owners were found is displayed.
3. **Given** there are multiple owners with the same last name, **When** the user searches for that last name, **Then** all matching owners are displayed.
4. **Given** there are owners with various last names, **When** the user searches with an empty last name field, **Then** all owners are displayed.

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the owner creation form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: The ability to add new owners is fundamental to the system's data management capabilities.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and confirming the owner appears in the owner list, delivering the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is saved and the user is redirected to the "Owners" list page, displaying the newly added owner.
2. **Given** the user is on the "Add Owner" page, **When** they attempt to submit the form with a blank first name, **Then** a validation error message is displayed for the first name field, and the form is not submitted.
3. **Given** the user is on the "Add Owner" page, **When** they attempt to submit the form with a telephone number that is not 10 digits, **Then** a validation error message is displayed for the telephone field, and the form is not submitted.

### User Story 3 - Add a New Pet to an Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details and adds a new pet, Then the pet is associated with the owner.

**Why this priority**: Managing pets is a key aspect of owner care within the clinic.

**Independent Test**: Can be fully tested by selecting an existing owner, adding a new pet with valid details, and confirming the pet appears under the owner's profile, delivering the ability to track an owner's pets.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the owner's detail page, selects "Add New Pet", fills in the pet's name, selects a pet type, and provides a birth date, **Then** the new pet is successfully created and linked to the owner.
2. **Given** an existing owner, **When** the user attempts to add a pet with a name that already exists for that owner, **Then** a validation error message is displayed indicating a duplicate pet name, and the pet is not created.

### User Story 4 - Update an Existing Owner (Priority: P2)

Given an owner exists, When a user edits the owner's details and saves the changes, Then the owner's information is updated.

**Why this priority**: Allows for correction of errors or updating of information for existing owners.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, saving the changes, and verifying the updated information is displayed, delivering the ability to maintain accurate owner records.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the owner's detail page, clicks "Edit Owner", modifies the address and city, and clicks "Save", **Then** the owner's address and city are updated, and the updated details are displayed.
2. **Given** an existing owner, **When** the user navigates to the owner's detail page, clicks "Edit Owner", and attempts to save with a blank last name, **Then** a validation error message is displayed for the last name field, and the changes are not saved.

### User Story 5 - View Owner Details (Priority: P3)

Given a list of owners is displayed, When a user clicks on an owner's name, Then the owner's detailed information, including their pets, is displayed.

**Why this priority**: Provides access to comprehensive information about a specific owner and their associated pets.

**Independent Test**: Can be fully tested by clicking on an owner's name from the list and verifying all their details and pets are shown, delivering the ability to view complete owner profiles.

**Acceptance Scenarios**:

1. **Given** a list of owners is displayed, **When** the user clicks on an owner's name, **Then** the owner's first name, last name, address, city, telephone, and a list of their associated pets (with names and types) are displayed.
2. **Given** an owner has no pets, **When** the user views the owner's details, **Then** a message indicating "No pets found" or similar is displayed for the pet section.

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Finding Owners with Empty Last Name**: Performing a search for owners with an empty last name → returns all owners, paginated.
- **Finding Owners with No Matches**: Searching for an owner's last name that does not exist in the database → validation error indicating "not found".
- **Finding Single Owner Match**: Searching for an owner's last name that results in exactly one match → redirects to the owner's detail page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's details (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow the creation of new pets for an owner.
- **FR-004**: System MUST allow updating an existing pet's details (name, type, birth date).
- **FR-005**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-006**: System MUST validate pet information during creation or update, enforcing non-blank names, selection of a pet type, and provision of a birth date.
- **FR-007**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-008**: System MUST display a list of owners, searchable by last name prefix.
- **FR-009**: System MUST display detailed information for a selected owner, including their associated pets.
- **FR-010**: System MUST populate a list of available pet types for selection when adding or editing a pet.
- **FR-011**: System MUST handle requests for non-existent owner IDs gracefully by indicating the owner was not found.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type. A pet belongs to one owner and has one pet type.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster). Attributes include name.
- **Person**: Base entity for Owner, containing first name and last name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner in under 1 minute.
- **SC-002**: Searching for owners by last name prefix returns results in under 2 seconds.
- **SC-003**: Users can add a new pet to an owner in under 3 minutes.
- **SC-004**: 95% of owner and pet creation/update operations complete without validation errors when valid data is provided.
- **SC-005**: All owner and pet data is accurately displayed when viewing owner details.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity structures.
- The system will use standard date formatting for birth dates.
- The system will provide a predefined list of pet types.
- Error messages will be user-friendly and informative.
- The system will handle pagination for owner lists if the number of owners exceeds a reasonable display limit.