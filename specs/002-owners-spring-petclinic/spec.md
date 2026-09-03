# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer relationships and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the displayed list. Delivers immediate value for staff looking up existing clients.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" field and click "Search", **Then** the system displays a list of owners whose last names start with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist, **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner profile so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new customers and expanding the clinic's client base.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields, and submitting. Verifies the creation of a new owner record and redirection to their details page.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form, **When** I fill in all required fields (First Name, Last Name, Address, City, Telephone) with valid data and click "Add Owner", **Then** a new owner is created, and I am redirected to the owner's details page.
2. **Given** I am on the "Add Owner" form, **When** I attempt to submit the form with a blank "First Name", **Then** the system displays a validation error for the "First Name" field and the owner is not created.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to add a new pet to an existing owner's profile so that I can manage all of a client's animals in one place.

**Why this priority**: Important for comprehensive pet management, but secondary to core owner management and finding.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, clicking "Add New Pet", filling in the pet details, and saving. Verifies the pet is associated with the correct owner.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add New Pet", fill in the pet's name, birth date, select a pet type, and click "Add Pet", **Then** the new pet is successfully added to the owner's profile.
2. **Given** I am viewing the details of an existing owner, **When** I attempt to add a pet with a blank name, **Then** the system displays a validation error for the pet's name and the pet is not added.

---

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

As a clinic staff member, I want to be able to update an existing pet's details so that I can keep their information current.

**Why this priority**: Necessary for maintaining accurate pet records, but less critical than initial creation or core owner management.

**Independent Test**: Can be fully tested by navigating to an existing pet's details, clicking "Edit Pet", modifying a field (e.g., birth date), and saving. Verifies the updated information is reflected.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing pet, **When** I click "Edit Pet", change the pet's birth date, and click "Update Pet", **Then** the pet's birth date is updated.
2. **Given** I am viewing the details of an existing pet, **When** I attempt to update the pet's name to a name that already exists for the same owner, **Then** the system rejects the update and displays a "duplicate name" error.

---

### User Story 5 - Handle Duplicate Pet Name Creation (Priority: P3)

As a clinic staff member, I want the system to prevent me from creating a pet with a name that already exists for the same owner, so that pet records remain unique and unambiguous.

**Why this priority**: This is a specific business rule that ensures data integrity, but the primary functionality of adding pets is more critical.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet to the same owner with the identical name.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add a new pet for the same owner and enter "Buddy" as the name, **Then** the system rejects the creation and displays a "duplicate name" error for the pet.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → system rejects with validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → system rejects with validation error.
- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → system throws `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → system rejects with validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner for Visit**: Attempting to add a visit for an owner ID that does not exist → system throws `IllegalArgumentException`.
- **Non-existent Pet for Visit**: Attempting to add a visit for a pet ID that does not exist for a given owner → system throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-006**: System MUST validate pet information (name, birth date, type) before saving.
- **FR-007**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-008**: System SHOULD display a form to create or update a pet, pre-populated with owner details.
- **FR-009**: System SHOULD provide a list of available pet types for selection during pet creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the clinic. Includes first name, last name, address, city, telephone, and a list of associated pets.
- **Pet**: Represents an animal belonging to an owner. Includes name, birth date, type, and a list of visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a medical visit for a pet. Includes date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 5 seconds.
- **SC-003**: Adding a new pet to an owner is completed within 5 seconds.
- **SC-004**: 95% of pet creation/update attempts with valid data succeed without errors.
- **SC-005**: Validation errors for owner and pet creation/updates are displayed clearly and immediately to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` base class for owner details.
- The system will use standard web form validation for all input fields.
- The system will use a standard database for storing owner and pet information.
- The system will use a standard date picker for selecting birth dates and visit dates.
- The system will provide a dropdown or similar selection mechanism for pet types.
- The system will handle `IllegalArgumentException` for non-existent IDs as per the provided context.
- The system will handle `DataIntegrityViolationException` for duplicate pet names.