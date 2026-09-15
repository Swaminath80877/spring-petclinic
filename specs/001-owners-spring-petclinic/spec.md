# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name starting with "Franklin", Then the system should redirect to the owner's details page.

**Why this priority**: This is a core functionality for users to find their pets' information quickly.

**Independent Test**: Can be fully tested by entering "Franklin" in the owner search field and verifying navigation to the correct owner's details page.

**Acceptance Scenarios**:

1. **Given** there are owners with last names starting with "Franklin", **When** a user searches for "Franklin", **Then** the system displays a list of owners matching "Franklin" and allows navigation to their details.
2. **Given** there are no owners with last names starting with "Franklin", **When** a user searches for "Franklin", **Then** the system displays a "no owners found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form with all required fields, Then the owner is created and the user is redirected to the owner's details page.

**Why this priority**: Essential for onboarding new pet owners into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and viewable.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit valid first name, last name, address, city, and telephone, **Then** the owner is successfully created and displayed on their respective details page.
2. **Given** a user is on the new owner form, **When** they submit with a blank first name, **Then** a validation error is shown for the first name field.
3. **Given** a user is on the new owner form, **When** they submit with an invalid telephone format, **Then** a validation error is shown for the telephone field.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

Given an owner exists, When a user adds a new pet for that owner with a unique name and a valid pet type, Then the pet is successfully associated with the owner.

**Why this priority**: Allows owners to register new pets, a common operation.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet management section, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** a user adds a pet named "Buddy" of type "Dog" with a birth date, **Then** the pet "Buddy" is listed under the owner's pets.
2. **Given** an owner exists with a pet named "Buddy", **When** a user attempts to add another pet named "Buddy" for the same owner, **Then** a validation error indicating a duplicate pet name is displayed.
3. **Given** an owner exists, **When** a user attempts to add a pet without selecting a pet type, **Then** a validation error indicating a missing pet type is displayed.

---

### User Story 4 - Update Existing Pet Information (Priority: P2)

Given an owner has an existing pet, When a user updates the pet's birth date or type, Then the pet's information is successfully updated.

**Why this priority**: Allows for correction of pet details.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Whiskers" of type "Cat", **When** the user updates the pet's type to "Lion" and saves, **Then** the pet's type is displayed as "Lion".
2. **Given** an owner has a pet with a birth date, **When** the user updates the birth date to a valid new date and saves, **Then** the new birth date is displayed.

---

### User Story 5 - Add a Visit for a Pet (Priority: P3)

Given a pet exists for an owner, When a user adds a new visit for that pet with a valid date and description, Then the visit is successfully recorded for the pet.

**Why this priority**: Tracks veterinary visits, a key aspect of pet care.

**Independent Test**: Can be fully tested by selecting a pet, navigating to its visit history, and adding a new visit with valid details.

**Acceptance Scenarios**:

1. **Given** a pet exists, **When** a user adds a visit with today's date and a description "Annual check-up", **Then** the visit is recorded and displayed in the pet's visit history.
2. **Given** a pet exists, **When** a user attempts to add a visit with an invalid date (e.g., in the past), **Then** a validation error is shown for the visit date.
3. **Given** a pet exists, **When** a user attempts to add a visit with a blank description, **Then** a validation error is shown for the visit description.

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when attempting to find or edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that does not match any records? → "notFound" validation error for lastName.
- What happens when a pet is created or updated with a blank name? → Validation error "required".
- What happens when a pet is created or updated without selecting a pet type? → Validation error "required".
- What happens when attempting to create a visit with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to create a visit for a pet belonging to a non-existent owner? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information.
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow the updating of existing pet information for an owner.
- **FR-006**: System MUST allow the creation of new visits for a pet.
- **FR-007**: System SHOULD validate owner data during creation or update.
- **FR-008**: System SHOULD validate pet data during creation or update.
- **FR-009**: System SHOULD validate visit data during creation or update.
- **FR-010**: System SHOULD provide a list of available pet types for selection during pet creation/update.
- **FR-011**: System SHOULD handle potential data integrity violations when saving owner, pet, or visit information.
- **FR-012**: System MUST ensure a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and pet type. A pet can have multiple visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Key attributes include name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to details page completes within 5 seconds.
- **SC-003**: Adding a new pet to an owner is completed and reflected in the owner's profile within 5 seconds.
- **SC-004**: 95% of users successfully add or update owner and pet information on their first attempt without encountering validation errors for valid data.
- **SC-005**: System handles duplicate pet names for the same owner by displaying a clear error message immediately.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data integrity for owner, pet, and visit information will be maintained through the application's validation and persistence layers.
- The list of available pet types is managed and provided by the system.
- The system will use standard web application conventions for user interaction and navigation.