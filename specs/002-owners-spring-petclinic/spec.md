# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-16

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owner information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed list.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" search field and click "Search", **Then** the system displays a list of owners whose last names start with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist, **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a new owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record so that I can register new clients.

**Why this priority**: This is fundamental to onboarding new customers into the system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting, and verifying the owner is created and displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid owner details (first name, last name, address, city, telephone) and click "Add Owner", **Then** the new owner is created and I am redirected to the owner's details page.
2. **Given** I am on the "New Owner" form, **When** I submit the form with a blank required field (e.g., last name), **Then** the system displays a validation error for the blank field and the owner is not created.

---

### User Story 3 - Add a new pet for an existing owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: This is a common task for existing clients who acquire new pets.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to add a pet, filling in valid pet details, and verifying the pet is added to the owner's record.

**Acceptance Scenarios**:

1. **Given** an existing owner exists, **When** I navigate to the owner's details page and choose to add a new pet, **Then** I can enter the pet's name, birth date, select a pet type, and save the new pet.
2. **Given** an existing owner exists with a pet named "Buddy", **When** I attempt to add a new pet for the same owner and enter "Buddy" as the name, **Then** the system rejects the new pet creation and displays a "duplicate name" error.

---

### User Story 4 - Update an existing pet's details (Priority: P2)

As a clinic staff member, I want to update an existing pet's details so that the information remains accurate.

**Why this priority**: Ensures that pet information is current for treatment and record-keeping.

**Independent Test**: Can be fully tested by selecting an existing pet, editing its details (e.g., birth date, type), saving, and verifying the changes.

**Acceptance Scenarios**:

1. **Given** an existing pet is associated with an owner, **When** I navigate to the pet's details and choose to edit, **Then** I can modify the pet's birth date and pet type and save the changes.

---

### User Story 5 - Record a new visit for a pet (Priority: P3)

As a clinic staff member, I want to record a new visit for a pet so that I can track their medical history.

**Why this priority**: Essential for maintaining a complete medical record for each pet.

**Independent Test**: Can be fully tested by selecting an existing pet, navigating to add a visit, entering a valid date and description, and saving.

**Acceptance Scenarios**:

1. **Given** an existing pet exists, **When** I navigate to the pet's details and choose to add a visit, **Then** I can enter the visit date and description and save the visit.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error with message "{telephone.invalid}".
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` with message "Owner not found with id: {ownerId}. Please ensure the ID is correct and the owner exists in the database."
- **Blank Pet Name**: Pet creation or update with a blank name → validation error with code "required".
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error with code "required".
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error with code "duplicate".
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error with code "typeMismatch.visitDate".
- **Non-existent Owner ID for Pet Visit**: Attempting to add a visit for a pet belonging to an owner ID that does not exist → `IllegalArgumentException` with message "Owner not found with id: {ownerId}. Please ensure the ID is correct ".
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` with message "Pet with id {petId} not found for owner with id {ownerId}.".
- **Exception Trigger**: Navigating to the `/oups` endpoint → `RuntimeException` is thrown, indicating an expected exception scenario.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System MUST allow the recording of a new visit for an existing pet.
- **FR-006**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-007**: System MUST validate pet information (name, birth date, type) before saving.
- **FR-008**: System MUST validate visit information (date, description) before saving.
- **FR-009**: System MUST display a list of owners when searching by last name.
- **FR-010**: System MUST display a list of pet types when creating or updating a pet.
- **FR-011**: System MUST handle cases where an owner is not found when attempting to add a pet or visit.
- **FR-012**: System MUST prevent a pet with a duplicate name from being added to the same owner.
- **FR-013**: System MUST display user-friendly error messages for validation failures.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact information and a list of their pets. Key attributes include first name, last name, address, city, and telephone.
- **Pet**: Represents an animal owned by an owner. Key attributes include name, birth date, and type. It is associated with an Owner and has a list of Visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). It has a name.
- **Visit**: Represents a medical visit for a pet. Key attributes include date and description. It is associated with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 5 seconds from form submission to display of owner details.
- **SC-003**: Adding a new pet to an owner is completed within 5 seconds from form submission to display of updated owner details.
- **SC-004**: 95% of new owner and pet creation forms are submitted successfully on the first attempt due to clear validation.
- **SC-005**: Support tickets related to incorrect owner or pet information are reduced by 30% within one quarter of release.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing Spring Boot conventions and best practices will be followed for implementation.
- The `Person` and `NamedEntity` base classes from `org.springframework.samples.petclinic.model` will be utilized for common attributes.
- Data integrity for relationships between owners, pets, and visits will be managed by the persistence layer.
- The `LocaleResolver` and `LocaleChangeInterceptor` will be configured to support internationalization if needed.
- The `/oups` endpoint is intended for demonstrating exception handling and is not a user-facing feature.