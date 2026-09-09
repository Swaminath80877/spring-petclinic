# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-09

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit, Then the system displays a list of owners whose last names start with the entered value.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Smith" into the last name search field and click "Search", **Then** a list of owners whose last names start with "Smith" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "Xyzzy") and click "Search", **Then** a message indicating "No owners found" is displayed.
3. **Given** the user is on the "Find Owners" page, **When** they leave the last name field blank and click "Search", **Then** all owners are displayed.

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Core functionality for adding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting, and verifying redirection to the new owner's detail page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the owner's details page.
2. **Given** the user is on the "New Owner" form, **When** they leave the "First Name" field blank and click "Add Owner", **Then** a validation error message is displayed for the "First Name" field, and the owner is not created.
3. **Given** the user is on the "New Owner" form, **When** they enter an invalid telephone number (e.g., "123") and click "Add Owner", **Then** a validation error message is displayed for the "Telephone" field, and the owner is not created.

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and adds a new pet with valid information, Then the new pet is associated with the owner.

**Why this priority**: Essential for managing an owner's animals, a key aspect of pet clinic operations.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, adding a new pet with valid details (name, birth date, type), and verifying the pet appears on the owner's details page. Delivers the ability to track an owner's pets.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** the user navigates to John Doe's details page, selects "Add New Pet", enters "Buddy" as the pet name, selects "Dog" as the pet type, and provides a valid birth date, **Then** the pet "Buddy" is successfully added to John Doe's profile.
2. **Given** an existing owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details page, selects "Add New Pet", leaves the pet name blank, and clicks "Add Pet", **Then** a validation error message "required" is displayed for the pet name, and the pet is not added.
3. **Given** an existing owner "Peter Jones" exists, **When** the user navigates to Peter Jones's details page, selects "Add New Pet", enters a pet name, but does not select a pet type, and clicks "Add Pet", **Then** a validation error message "required" is displayed for the pet type, and the pet is not added.

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

Given a pet exists for an owner, When a user navigates to the pet's details and updates its information, Then the pet's details are successfully updated.

**Why this priority**: Allows for correction of errors or updating information about a pet.

**Independent Test**: Can be fully tested by selecting an owner, then a pet, modifying a field (e.g., pet name), saving, and verifying the change. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** an owner "Alice Wonderland" has a pet named "Cheshire Cat", **When** the user navigates to Cheshire Cat's details, changes the name to "Grinning Cat", and clicks "Update Pet", **Then** the pet's name is updated to "Grinning Cat".
2. **Given** an owner "Bob The Builder" has a pet named "Scoop", **When** the user navigates to Scoop's details, changes the birth date to an invalid format (e.g., "2010/05/15"), and clicks "Update Pet", **Then** a validation error message "typeMismatch" is displayed for the birth date, and the pet's details are not updated.

### User Story 5 - Handle Duplicate Pet Name for an Owner (Priority: P3)

Given an owner exists with a pet, When a new pet with a duplicate name is added for the same owner, Then the system rejects the duplicate name and displays an error message.

**Why this priority**: Ensures data integrity by preventing duplicate pet names within the same owner's record.

**Independent Test**: Can be fully tested by adding a pet for an owner, then attempting to add another pet for the same owner with the exact same name. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** owner "Charlie Chaplin" has a pet named "Buster", **When** the user attempts to add another pet for "Charlie Chaplin" with the name "Buster", **Then** a validation error message "duplicate" is displayed, and the pet is not added.

### User Story 6 - View Owner Details (Priority: P1)

Given an owner exists, When a user searches for the owner and selects them, Then the system displays the owner's full details, including their pets and visits.

**Why this priority**: Fundamental for accessing and reviewing all information related to a specific owner and their pets.

**Independent Test**: Can be fully tested by finding an owner and verifying all their associated information (address, contact, pets, visits) is displayed correctly. Delivers comprehensive owner information access.

**Acceptance Scenarios**:

1. **Given** owner "Diana Prince" exists with pets and visits, **When** the user finds and selects "Diana Prince", **Then** all of Diana Prince's contact information, list of pets, and associated visits are displayed.

### User Story 7 - Add a Visit for a Pet (Priority: P2)

Given a pet exists for an owner, When a user navigates to the pet's details and adds a new visit with a valid date and description, Then the visit is recorded for that pet.

**Why this priority**: Essential for tracking the medical history and appointments of pets.

**Independent Test**: Can be fully tested by selecting a pet, adding a visit with a valid date and description, and verifying the visit appears in the pet's history. Delivers pet visit tracking.

**Acceptance Scenarios**:

1. **Given** pet "Fido" owned by "John Doe" exists, **When** the user navigates to Fido's details, selects "Add New Visit", enters a future date and a description "Annual check-up", **Then** the visit is recorded for Fido.
2. **Given** pet "Fido" owned by "John Doe" exists, **When** the user navigates to Fido's details, selects "Add New Visit", enters an invalid date (e.g., a past date) and a description, **Then** a validation error message "typeMismatch.visitDate" is displayed, and the visit is not recorded.

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Blank Owner Last Name Search**: Searching for owners with a blank last name → returns all records.
- **No Owners Found**: Searching for an owner last name that does not exist → validation error "notFound" for lastName.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating a pet without selecting a type → validation error "required".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Blank Pet Birth Date**: Creating or updating a pet with a null birth date → validation error "required".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` indicating pet not found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow searching for owners by last name.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner.
- **FR-006**: System MUST allow the update of an existing pet's details.
- **FR-007**: System MUST display a list of pet types when creating or updating a pet.
- **FR-008**: System MUST handle cases where an owner is not found when attempting to add a pet.
- **FR-009**: System MUST allow the creation of a new visit for an existing pet.
- **FR-010**: System MUST display an owner's details, including their pets and visits.
- **FR-011**: System MUST validate owner first name is not blank.
- **FR-012**: System MUST validate owner last name is not blank.
- **FR-013**: System MUST validate owner address is not blank.
- **FR-014**: System MUST validate owner city is not blank.
- **FR-015**: System MUST validate owner telephone is exactly 10 digits.
- **FR-016**: System MUST validate pet name is not blank.
- **FR-017**: System MUST validate pet name is unique for a given owner.
- **FR-018**: System MUST validate visit date is in the future.
- **FR-019**: System SHOULD validate pet information before saving.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, telephone, and a list of associated Pets.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, type (PetType), and a set of associated Visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 1 minute of form submission.
- **SC-003**: 95% of pet creation attempts with valid data succeed on the first try.
- **SC-004**: System successfully prevents duplicate pet names for the same owner 100% of the time.
- **SC-005**: Owner details pages load within 2 seconds.
- **SC-006**: Support tickets related to incorrect owner or pet information are reduced by 30%.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date formats will be used for input and display.
- The list of pet types is predefined and managed separately.
- Error messages will be user-friendly and informative.
- The system will operate within a single clinic context.