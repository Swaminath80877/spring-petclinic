# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `011-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find and access their information.

**Why this priority**: This is a core functionality for managing owner data and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists in the system, **When** I search for owners using the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** no owners match a given last name prefix, **When** I search for owners using that prefix, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to create a new owner profile so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and verifying the owner is added to the system.

**Acceptance Scenarios**:

1. **Given** I am on the owner creation form, **When** I enter valid first name, last name, address, city, and telephone number, and click "Save", **Then** the new owner is created, and I am redirected to the owner details page or the owner list with the new owner visible.
2. **Given** I am on the owner creation form, **When** I leave the first name blank and click "Save", **Then** a validation error message is displayed for the first name field, and the owner is not created.

---

### User Story 3 - View Owner List (Priority: P3)

As a clinic staff member, I want to view a list of all owners so that I can get an overview of registered clients.

**Why this priority**: Provides a general overview and is a common starting point for other owner-related tasks.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system, **When** I navigate to the "Owners" page, **Then** a list displaying all owners, including their first name, last name, and address, is shown.

---

### User Story 4 - View Owner Details (Priority: P3)

As a clinic staff member, I want to view the details of a specific owner so that I can see their personal information and associated pets.

**Why this priority**: Allows access to detailed information for a specific client.

**Independent Test**: Can be fully tested by clicking on an owner's name from the list and verifying their details and pets are displayed.

**Acceptance Scenarios**:

1. **Given** an owner exists with associated pets, **When** I click on the owner's name from the owner list, **Then** the owner's details (address, city, telephone) and a list of their pets (name, birth date, type) are displayed.

---

### User Story 5 - Add a New Pet for an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet for an existing owner so that I can keep track of all their animals.

**Why this priority**: Crucial for maintaining a complete record of a client's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet addition form, filling in valid pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's details, **When** I click "Add New Pet", **And** I fill in the pet's name, birth date, and select a pet type, **And** click "Save", **Then** the new pet is added to the owner's record and displayed in their pet list.
2. **Given** I am on the "Add New Pet" form for an owner, **When** I leave the pet name blank and click "Save", **Then** a validation error message is displayed for the pet name field, and the pet is not added.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with an invalid telephone format (not 10 digits)? → Validation error.
- What happens when attempting to edit or view an owner with a non-existent ID? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created or updated with a blank name? → Validation error.
- What happens when a pet is created or updated without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when a visit is submitted with an invalid date (not in the future)? → Validation error.
- What happens when attempting to add a visit for a pet belonging to a non-existent owner ID? → `IllegalArgumentException` indicating owner not found.
- What happens when attempting to add a visit for a non-existent pet ID for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when navigating to the "/oups" endpoint? → `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone number.
- **FR-002**: System MUST allow searching for owners by last name prefix.
- **FR-003**: System MUST display a list of all owners.
- **FR-004**: System MUST display the details of a specific owner, including their pets.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and type.
- **FR-006**: System MUST allow the update of an existing pet's details.
- **FR-007**: System SHOULD validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-008**: System SHOULD validate pet information (name, birth date, type) before saving.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD populate a dropdown with available pet types when creating or updating a pet.
- **FR-011**: System MUST handle invalid owner IDs gracefully by indicating the owner was not found.
- **FR-012**: System MUST handle invalid pet IDs gracefully by indicating the pet was not found.
- **FR-013**: System MUST handle invalid owner IDs when adding visits gracefully by indicating the owner was not found.
- **FR-014**: System MUST handle invalid pet IDs when adding visits gracefully by indicating the pet was not found.
- **FR-015**: System MUST display user-friendly error messages for validation failures.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the veterinary clinic. Includes attributes for first name, last name, address, city, and telephone number. Can have multiple associated pets.
- **Pet**: Represents an animal belonging to an owner. Includes attributes for name, birth date, and type. Can have multiple associated visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a veterinary visit for a pet. Includes attributes for date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: New pets can be added to an owner's record in under 1 minute.
- **SC-004**: 95% of form submissions (owner creation/update, pet creation/update) with invalid data display clear validation errors to the user.
- **SC-005**: The system supports displaying up to 100 owners on the owner list page without significant performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics unless otherwise specified.
- The primary users of this feature are clinic staff members.
- The "spring-petclinic" project structure and conventions will be followed.
- The `PetType` entities are pre-populated or managed separately.
- The `Visit` entity is primarily for tracking visit dates and is associated with a `Pet`.
- The `Exception Trigger` for "/oups" is for demonstrating error handling and not a core functional requirement of owner management.