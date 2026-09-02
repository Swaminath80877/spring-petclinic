# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer relationships and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a known last name (e.g., "Franklin"), and verifying that the correct owner(s) are displayed. Delivers the ability to locate existing owners.

**Acceptance Scenarios**:

1. **Given** an owner exists with the last name "Franklin", **When** a user searches for owners by last name "Franklin", **Then** the system displays a list containing the owner with the last name "Franklin".
2. **Given** multiple owners exist with the last name "Smith", **When** a user searches for owners by last name "Smith", **Then** the system displays a list of all owners with the last name "Smith".
3. **Given** no owners exist with the last name "XYZ", **When** a user searches for owners by last name "XYZ", **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register my pet with the clinic.

**Why this priority**: This is a fundamental requirement for onboarding new clients and is critical for business growth.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting the form, and verifying that the new owner is created and their details page is displayed. Delivers the ability to add new clients to the system.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields populated, **Then** the new owner is created and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank first name, **Then** the system displays a validation error for the first name and the owner is not created.
3. **Given** a user is on the new owner form, **When** they submit the form with an invalid telephone number (e.g., 9 digits), **Then** the system displays a validation error for the telephone number and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

As an owner, I want to be able to add a new pet to my existing owner profile so that I can register all my pets with the clinic.

**Why this priority**: This allows owners to manage their pets effectively within the system.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, initiating the process to add a new pet, filling in valid pet details (name, birth date, type), and saving it. Delivers the ability to associate multiple pets with an owner.

**Acceptance Scenarios**:

1. **Given** an existing owner exists, **When** the owner navigates to their profile and initiates adding a new pet, **And** provides valid pet details (name, birth date, type), **Then** the new pet is successfully added to the owner's profile.
2. **Given** an existing owner exists, **When** the owner attempts to add a new pet with a blank name, **Then** the system displays a validation error for the pet's name and the pet is not added.
3. **Given** an existing owner exists, **When** the owner attempts to add a new pet without selecting a pet type, **Then** the system displays a validation error for the pet type and the pet is not added.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

As an owner, I want the system to prevent me from adding a pet with a name that already exists for my other pets, so that I can maintain unique pet identifiers.

**Why this priority**: Ensures data integrity and avoids confusion when managing multiple pets.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet with the exact same name to the same owner. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner exists with a pet named "Buddy", **When** the owner attempts to add a new pet with the name "Buddy" for the same owner, **Then** the system rejects the creation and displays a "duplicate" error message for the pet's name.
2. **Given** an owner exists with two pets, "Max" and "Lucy", **When** the owner attempts to add a new pet named "Max", **Then** the system displays a validation error indicating the name is already in use.

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation or update with a blank name → validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → validation error indicating the name is already in use.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error `typeMismatch.visitDate`.
- **Non-existent Owner for Visit**: Attempting to create a visit for an owner ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Non-existent Pet for Visit**: Attempting to create a visit for a pet ID that does not exist for the specified owner → `IllegalArgumentException` indicating pet not found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System SHOULD validate pet information before saving.
- **FR-006**: System SHOULD display a form for creating or updating pet information.
- **FR-007**: System SHOULD populate a dropdown list with available pet types when creating or updating a pet.
- **FR-008**: System MUST prevent the creation of a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact details (address, city, telephone) and a list of associated pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 1 minute from form submission to confirmation.
- **SC-003**: 95% of pet creation attempts for existing owners are successful (excluding validation errors).
- **SC-004**: The system correctly identifies and prevents duplicate pet names for the same owner on the first attempt.
- **SC-005**: Support tickets related to owner or pet data entry errors are reduced by 30% within one month of release.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be reused if applicable for owner management.
- The set of PetTypes will be managed separately and available for selection.
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics.