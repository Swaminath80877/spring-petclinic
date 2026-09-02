# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by providing a prefix of their last name. The system should then display a list of all owners whose last names match the provided prefix.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name prefix, and verifying the displayed list of owners. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists in the system, **When** a user searches for owners using the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** no owners match a given last name prefix, **When** a user searches for owners using that prefix, **Then** a message indicating no owners were found is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Users should be able to create a new owner by filling out a form with their details (first name, last name, address, city, telephone). Upon successful submission of a valid form, the new owner should be created and the user redirected to the owner's list page.

**Why this priority**: This is a fundamental operation for adding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the owner creation form, filling in valid details, submitting, and verifying the owner appears in the owner list. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the owner creation form, **When** they submit a valid owner form with all required fields populated correctly, **Then** the owner is created and the user is redirected to the owner's list page, displaying the newly added owner.
2. **Given** a user is on the owner creation form, **When** they submit the form with a blank address, **Then** a validation error message is displayed for the address field, and the form is re-displayed with the entered data preserved.

---

### User Story 3 - Handle Duplicate Pet Name Creation (Priority: P2)

If an owner already has a pet with a specific name, the system should prevent the creation of another pet with the same name for that same owner. An informative error message should be displayed, and the form should be re-displayed.

**Why this priority**: Ensures data integrity and prevents confusion by maintaining unique pet names per owner.

**Independent Test**: Can be fully tested by creating a pet for an owner, then attempting to create a second pet for the same owner with the identical name. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner exists with a pet named "Buddy", **When** a user attempts to create a new pet for the same owner with the name "Buddy", **Then** an error message indicating a duplicate name is displayed, and the pet creation form is re-displayed with the entered data.

---

### User Story 4 - Update an Existing Owner (Priority: P2)

Users should be able to edit the details of an existing owner. After making changes and submitting the form, the owner's information should be updated in the system.

**Why this priority**: Allows for correction of errors or updating of owner information as it changes.

**Independent Test**: Can be fully tested by selecting an existing owner, modifying their details, submitting the form, and verifying the changes are reflected in the owner's profile. Delivers the ability to maintain accurate owner records.

**Acceptance Scenarios**:

1. **Given** an existing owner is displayed, **When** the user edits the owner's telephone number and submits the form, **Then** the owner's telephone number is updated in the system.
2. **Given** an existing owner is displayed, **When** the user attempts to change the owner's city to a blank value and submits the form, **Then** a validation error message for the city field is displayed, and the form is re-displayed with the entered data.

---

### User Story 5 - Add a New Pet to an Owner (Priority: P1)

Users should be able to add a new pet to an existing owner. This involves selecting the owner, providing pet details (name, birth date, type), and associating it with the owner.

**Why this priority**: Core functionality for managing an owner's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the pet addition form, filling in valid pet details, and verifying the new pet is listed under the owner. Delivers the ability to track an owner's pets.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user adds a new pet with a unique name, a valid birth date, and a selected pet type, **Then** the pet is successfully associated with the owner.
2. **Given** an owner exists, **When** the user attempts to add a new pet with a blank name, **Then** a validation error message for the pet name is displayed, and the form is re-displayed.

---

### User Story 6 - View Owner's Pets (Priority: P1)

When viewing an owner's details, all associated pets should be displayed, including their names and types.

**Why this priority**: Provides a complete view of an owner's relationship with their pets.

**Independent Test**: Can be fully tested by selecting an owner who has pets and verifying that all their pets are listed. Delivers a comprehensive owner profile.

**Acceptance Scenarios**:

1. **Given** an owner has multiple pets (e.g., a dog and a cat), **When** the user views the owner's details, **Then** both the dog and the cat are listed with their respective names and types.
2. **Given** an owner has no pets, **When** the user views the owner's details, **Then** a message indicating no pets are associated with the owner is displayed.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → system rejects with validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist in the database → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → system rejects with validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner ID for Visit**: Attempting to add a visit for an owner ID that does not exist → system throws `IllegalArgumentException`.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a pet ID that does not exist for a given owner → system throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST allow the creation of a new pet for an owner.
- **FR-006**: System MUST allow updating an existing pet's name.
- **FR-007**: System MUST validate owner information (first name, last name, address, city, telephone) during creation or update.
- **FR-008**: System MUST validate pet information (name, birth date, type) during creation or update.
- **FR-009**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-010**: System MUST display a list of pets associated with an owner when viewing owner details.
- **FR-011**: System MUST reject owner creation/update with blank address.
- **FR-012**: System MUST reject owner creation/update with blank city.
- **FR-013**: System MUST reject owner creation/update with an invalid telephone format.
- **FR-014**: System MUST reject pet creation/update with a blank name.
- **FR-015**: System MUST reject pet creation with a missing pet type.
- **FR-016**: System MUST handle attempts to edit or access non-existent owner IDs by throwing an `IllegalArgumentException`.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, telephone, and a list of associated pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and pet type. It is associated with an Owner and can have multiple Visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Key attribute is its name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description. It is associated with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be created and displayed in the owner list within 5 seconds of form submission.
- **SC-003**: 95% of pet creation attempts for an owner with a unique pet name are successful on the first try.
- **SC-004**: Validation errors for owner and pet forms are displayed to the user within 1 second of submission.
- **SC-005**: The system successfully prevents duplicate pet names for the same owner 100% of the time.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing validation mechanisms for common data types (e.g., date formats).
- The system will use standard web application patterns for form submission and error handling.
- The telephone number format validation will strictly enforce a 10-digit numerical pattern.
- Pet types will be pre-defined and selectable from a list.
- The system will handle non-existent owner IDs by throwing an `IllegalArgumentException` as per existing patterns.
- The primary focus is on owner and pet management; visit management is considered a separate, though related, feature.