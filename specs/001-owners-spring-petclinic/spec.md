# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then they are redirected to the owners list page displaying matching owners.

**Why this priority**: This is a core functionality for users to locate their pets' information quickly.

**Independent Test**: Can be fully tested by entering a known owner's last name and verifying the correct owner details are displayed, delivering the ability to find specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last name" field and click "Search", **Then** the "Owner List" page is displayed showing owners with the last name "Davis".
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist (e.g., "NonExistent") and click "Search", **Then** a "not found" error message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and they are redirected to the owner's details page.

**Why this priority**: Essential for onboarding new pet owners into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner's details page is displayed, delivering the ability to add new owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the owner is created and the user is redirected to the "Owner Details" page for the newly created owner.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank address, **Then** a validation error message is displayed for the address field, and the form is re-rendered.
3. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a telephone number that is not 10 digits, **Then** a validation error message is displayed for the telephone field, and the form is re-rendered.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and initiates the process to add a new pet, Then they are presented with a form to enter pet details, and upon submission of valid data, the new pet is associated with the owner.

**Why this priority**: Allows owners to manage multiple pets within the system.

**Independent Test**: Can be fully tested by selecting an existing owner, adding a new pet with valid details, and verifying the pet appears on the owner's details page, delivering the ability to manage multiple pets per owner.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** the user navigates to "John Doe's" owner details page and clicks "Add New Pet", **Then** a "New Pet" form is displayed, allowing selection of pet type and input of name and birth date.
2. **Given** the user is on the "New Pet" form for "John Doe", **When** they enter a valid pet name (e.g., "Buddy"), select a pet type (e.g., "Dog"), and enter a valid birth date, and click "Add Pet", **Then** the pet "Buddy" is successfully added to "John Doe's" record and appears on their details page.
3. **Given** the user is on the "New Pet" form for "John Doe", **When** they attempt to add a pet with a blank name, **Then** a validation error message is displayed for the pet name, and the form is re-rendered.
4. **Given** the user is on the "New Pet" form for "John Doe", **When** they attempt to add a pet without selecting a pet type, **Then** a validation error message is displayed for the pet type, and the form is re-rendered.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P2)

Given an owner has an existing pet with a specific name, When a new pet is created with the same name for that owner, Then an error message indicating a duplicate name is displayed and the form is re-rendered.

**Why this priority**: Prevents data integrity issues and provides clear feedback to the user.

**Independent Test**: Can be fully tested by creating a pet for an owner, then attempting to create another pet for the same owner with the identical name, verifying the duplicate name error is shown, delivering data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" has a pet named "Max", **When** the user attempts to add another pet for "Jane Smith" with the name "Max", **Then** an error message "The pet name must be unique for a given owner" is displayed, and the "New Pet" form is re-rendered.

---

### User Story 5 - Update Existing Pet Details (Priority: P3)

Given a user is viewing an owner's details page with existing pets, When they choose to edit a specific pet, Then they are presented with a form pre-populated with the pet's current details, and upon submission of valid changes, the pet's information is updated.

**Why this priority**: Allows for correction of errors or updating information for existing pets.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, and verifying the changes are reflected on the owner's details page, delivering the ability to correct pet information.

**Acceptance Scenarios**:

1. **Given** owner "Peter Jones" has a pet named "Fido" (a Dog), **When** the user clicks the "Edit" button for "Fido", **Then** the "Edit Pet" form is displayed, pre-populated with "Fido's" name, type, and birth date.
2. **Given** the user is on the "Edit Pet" form for "Fido", **When** they change the pet's name to "Buddy", select a different pet type (e.g., "Cat"), and click "Update Pet", **Then** the pet's details are updated to "Buddy" (a Cat) and displayed on "Peter Jones's" owner details page.
3. **Given** the user is on the "Edit Pet" form for "Fido", **When** they attempt to submit the form with a blank pet name, **Then** a validation error message is displayed for the pet name, and the form is re-rendered.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → system rejects with validation error.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → system rejects with validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner ID**: Attempting to access or create resources (e.g., pets, visits) for an owner ID that does not exist → system throws an `IllegalArgumentException`.
- **Non-existent Pet ID for Owner**: Attempting to access or update a pet for a specific owner where the pet ID does not exist for that owner → system throws an `IllegalArgumentException`.
- **Find Owner with No Results**: Searching for owners with a last name that does not match any existing owners → system displays a "not found" error message.
- **Exception Trigger**: Navigating to the "/oups" endpoint → system throws a `RuntimeException` to demonstrate exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System SHOULD validate owner information (address, city, telephone) during creation or update.
- **FR-007**: System SHOULD validate pet information (name, type, birth date) during creation or update.
- **FR-008**: System SHOULD display a form for creating or updating owner details.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD allow viewing a list of pet types when creating or updating a pet.
- **FR-011**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-012**: System MUST display user-friendly error messages for validation failures.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details like address, city, and telephone. Can have multiple pets.
- **Pet**: Represents a pet, including its name, birth date, and type. Belongs to an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 2 minutes.
- **SC-003**: New pets can be added to an existing owner in under 1 minute.
- **SC-004**: 95% of users successfully complete owner or pet creation/update forms without encountering validation errors on their first attempt.
- **SC-005**: The system prevents the creation of duplicate pet names for the same owner, with immediate user feedback.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- The primary target users are clinic staff responsible for managing owner and pet information.
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics unless otherwise specified.
- The system will use standard web form validation mechanisms.
- The date format for pet birth dates and visit dates will be "yyyy-MM-dd".
- The telephone number format will be a 10-digit number.
- The system will handle non-existent owner or pet IDs by returning appropriate error messages or exceptions as per existing patterns.
- The "/oups" endpoint is for demonstrating exception handling and is not a core feature requirement.
- The "owners" module is the primary focus, and other modules (like "vets") are out of scope for this specification.