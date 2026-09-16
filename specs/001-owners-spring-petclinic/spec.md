# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-16

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer relationships and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying that the correct owner(s) are displayed in the list.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last name" field and click "Search", **Then** I should see a list of owners whose last name is "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist (e.g., "NonExistent"), **Then** I should see a message indicating no owners were found.
3. **Given** I am on the "Find Owners" page, **When** I leave the "Last name" field blank and click "Search", **Then** I should see a list of all owners.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying that the new owner's details page is displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid details for first name, last name, address, city, and telephone, **Then** the owner is created and I am redirected to the new owner's details page.
2. **Given** I am on the "New Owner" form, **When** I leave the "First name" field blank and attempt to submit, **Then** I should see a validation error message for the first name.
3. **Given** I am on the "New Owner" form, **When** I enter an invalid telephone number (e.g., "123") and attempt to submit, **Then** I should see a validation error message for the telephone number.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As an owner, I want to be able to add a new pet to my existing profile so that I can register all my animals with the clinic.

**Why this priority**: This allows existing clients to manage their pets over time, which is a common requirement.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their details page, initiating the process to add a new pet, filling in valid pet details, and verifying the pet is listed under the owner.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add New Pet", **And** I enter a valid pet name and select a pet type, **Then** the new pet is added to the owner's profile.
2. **Given** I am viewing the details of an existing owner, **When** I attempt to add a new pet with a blank name, **Then** I should see a validation error message for the pet name.
3. **Given** I am viewing the details of an existing owner, **When** I attempt to add a new pet without selecting a pet type, **Then** I should see a validation error message for the pet type.

---

### User Story 4 - Update an Existing Pet's Information (Priority: P2)

As an owner, I want to be able to update the information for an existing pet so that I can keep my records accurate.

**Why this priority**: Allows for correction of errors or changes in pet details.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, modifying a field (e.g., name), saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing pet, **When** I change the pet's name to a new valid name and save, **Then** the pet's name is updated.
2. **Given** I am viewing the details of an existing pet, **When** I attempt to change the pet's name to a blank value and save, **Then** I should see a validation error message for the pet name.

---

### User Story 5 - Handle Duplicate Pet Name Creation (Priority: P3)

As an owner, I want to be prevented from creating a pet with a name that already exists for my other pets so that my pet records are unique and unambiguous.

**Why this priority**: This is a data integrity rule that prevents confusion.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet with the exact same name to the same owner, and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add another pet for the same owner and name it "Buddy", **Then** an error message is displayed indicating the pet name is a duplicate.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Owner Last Name**: Owner search with a blank last name → broad search is performed.
- **Non-existent Owner ID**: Accessing an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Duplicate Pet Name**: Attempting to create a pet with a name that already exists for the same owner → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Invalid Pet Birth Date Format**: Pet update with an incorrectly formatted birth date (e.g., "2015/02/12") → `typeMismatch` validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → `typeMismatch.visitDate` validation error.
- **Non-existent Owner ID for Visit**: Creating a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Creating a visit for a pet ID that does not exist for the given owner → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's name.
- **FR-005**: System SHOULD validate pet information during creation or update.
- **FR-006**: System MUST prevent the creation of a pet with a duplicate name for the same owner.
- **FR-007**: System MUST display appropriate validation errors for invalid owner and pet data.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. A pet belongs to one owner and has one pet type.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Key attribute is the name of the pet type.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date. A visit is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 1 minute from form submission to confirmation.
- **SC-003**: 95% of users successfully add a new pet to an existing owner on their first attempt.
- **SC-004**: Validation errors for owner and pet data are displayed clearly and immediately upon form submission.
- **SC-005**: The system prevents duplicate pet names for a given owner with a clear error message.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The primary language for the application is English.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The `spring-petclinic` project structure and existing modules (like `model`, `persistence`, `validation`) will be leveraged.
- The H2 database will be used for development and testing.
- The `PetType` entities (Cat, Dog, etc.) will be pre-populated or managed through a separate mechanism.