# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `023-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for navigating and managing owners within the pet clinic system. It's essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct owner(s) are displayed. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last Name" search field and click "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist, **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is a fundamental capability for adding new clients to the pet clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to the newly created owner's details page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (First Name, Last Name, Address, City, Telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the owner's details page.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank "First Name", **Then** a validation error message is displayed for the "First Name" field, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and chooses to add a new pet, Then they can enter pet details (name, birth date, type) and save the new pet.

**Why this priority**: This allows for the management of multiple pets per owner, which is a common requirement in a veterinary setting.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, initiating the "Add Pet" action, filling in valid pet details, and verifying the pet appears on the owner's details page. Delivers the ability to associate new pets with existing clients.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** the user navigates to John Doe's details page, clicks "Add Pet", enters "Buddy" as the pet name, selects "Dog" as the pet type, and provides a birth date, **Then** "Buddy" is listed as one of John Doe's pets.
2. **Given** an existing owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details page, clicks "Add Pet", and attempts to save without selecting a pet type, **Then** a validation error is displayed for the pet type, and the pet is not saved.

---

### User Story 4 - Handle Duplicate Pet Name for an Owner (Priority: P2)

Given an owner exists with a pet, When a new pet with a duplicate name is added for the same owner, Then an error message indicating the duplicate name is displayed.

**Why this priority**: Prevents data inconsistencies and ensures clear feedback to the user when attempting to create a pet with a name that already exists for that owner.

**Independent Test**: Can be fully tested by creating an owner with one pet, then attempting to add a second pet for the same owner with the exact same name, and verifying the error message. Delivers data integrity and user feedback.

**Acceptance Scenarios**:

1. **Given** owner "Alice Wonderland" has a pet named "Cheshire Cat", **When** the user attempts to add another pet for "Alice Wonderland" with the name "Cheshire Cat", **Then** an error message "The pet name must be unique for this owner" is displayed, and the duplicate pet is not saved.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P3)

Given a pet exists for an owner, When a user navigates to the pet's details and chooses to edit the pet, Then they can change the pet's name and save the update.

**Why this priority**: Allows for correction of naming errors or changes in pet names.

**Independent Test**: Can be fully tested by selecting an owner, then a pet, initiating the edit action, changing the pet's name, saving, and verifying the name has been updated on the owner's details page. Delivers the ability to correct pet information.

**Acceptance Scenarios**:

1. **Given** owner "Bob The Builder" has a pet named "Scoop", **When** the user navigates to "Scoop's" details, changes the name to "Digger", and saves, **Then** the pet is now listed as "Digger" on Bob The Builder's details page.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` with a "Owner not found" message.
- **Blank Pet Name**: Pet creation or update with a blank name → validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating the name is already in use.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error `typeMismatch.visitDate`.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for the specified owner → `IllegalArgumentException` with a "Pet not found" message.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-003**: System MUST allow the update of an existing pet's name.
- **FR-004**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-005**: System MUST validate pet information during creation or update, enforcing a non-blank name and the selection of a pet type.
- **FR-006**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-007**: System MUST display a list of available pet types when creating or updating a pet.
- **FR-008**: System MUST allow users to find owners by their last name.
- **FR-009**: System MUST handle cases where an owner or pet ID does not exist, returning appropriate error messages.
- **FR-010**: System MUST allow the creation of visits for a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details and a list of their pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, type, and visits.
- **PetType**: Represents the classification of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required information in under 1 minute.
- **SC-003**: New pets can be added to an existing owner's record in under 1 minute.
- **SC-004**: Validation errors for owner and pet creation/updates are displayed clearly and immediately to the user.
- **SC-005**: The system prevents duplicate pet names for the same owner with immediate user feedback.
- **SC-006**: 95% of owner and pet data operations (create, update, find) complete successfully without errors.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled by other modules and are not part of this feature's scope.
- The list of Pet Types is pre-populated or managed by a separate administrative function.
- Data retention policies for owner and pet information are handled at the application level and are not specified here.
- Error messages will be user-friendly and informative.
- The `\d{10}` pattern for telephone numbers is sufficient for all required regions.
- The `yyyy-MM-dd` format for birth dates is universally understood and accepted.