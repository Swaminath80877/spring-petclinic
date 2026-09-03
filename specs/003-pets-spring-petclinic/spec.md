# Feature Specification: Pet Management

**Feature Branch**: `003-pets-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a new pet for an owner (Priority: P1)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage all their animals.

**Why this priority**: This is a core function for managing pet information and is essential for day-to-day operations.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling in valid pet details, and verifying the pet is listed under the owner.

**Acceptance Scenarios**:

1. **Given** I am logged in as clinic staff and viewing an owner's details, **When** I click "Add Pet" and fill in the pet's name ("Buddy"), type ("Dog"), and birth date ("2020-05-15"), **Then** the new pet is saved and displayed under the owner's profile with the success message "Pet details has been edited".
2. **Given** I am logged in as clinic staff and viewing an owner's details, **When** I attempt to add a pet with a blank name, **Then** an error message "Pet name must not be blank" is displayed, and the form remains open.
3. **Given** I am logged in as clinic staff and viewing an owner's details, **When** I attempt to add a pet with a blank type, **Then** an error message "Pet type must not be blank" is displayed, and the form remains open.
4. **Given** I am logged in as clinic staff and viewing an owner's details, **When** I attempt to add a pet with a blank birth date, **Then** an error message "Pet birth date must not be blank" is displayed, and the form remains open.

---

### User Story 2 - Prevent creation of a pet with a duplicate name for the same owner (Priority: P2)

As a clinic staff member, I want the system to prevent me from adding a pet with a name that already exists for the same owner, to avoid confusion.

**Why this priority**: Maintaining unique pet names per owner is crucial for accurate record-keeping and avoiding data integrity issues.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet with the exact same name to the same owner.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID `TEST_OWNER_ID` and already has a pet named "Betty", **When** I attempt to create a new pet for the same owner with the name "Betty", **Then** the system rejects the creation with a "duplicate" error for the pet's name, and the form remains on the "createOrUpdatePetForm" view.

---

### User Story 3 - Update an existing pet's details (Priority: P1)

As a clinic staff member, I want to be able to update an existing pet's information (like type or birth date) so that I can keep records accurate.

**Why this priority**: This is a fundamental operation for maintaining up-to-date pet records.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, saving the changes, and verifying the updated information.

**Acceptance Scenarios**:

1. **Given** an owner exists with ID `TEST_OWNER_ID` and has a pet with ID `TEST_PET_ID` named "Buddy", **When** I navigate to edit "Buddy", change its type to "Cat" and its birth date to "2021-01-20", and save, **Then** the pet's information is updated, and a success message "Pet details has been edited" is displayed.
2. **Given** I am editing a pet, **When** I attempt to update the pet's name to a name that already exists for the same owner, **Then** the system rejects the update with a "duplicate" error for the pet's name, and the form remains open.
3. **Given** I am editing a pet, **When** I attempt to update the pet's birth date to a date in the future, **Then** the system rejects the update with a "typeMismatch.birthDate" error, and the form remains open.

---

### User Story 4 - View available pet types (Priority: P1)

As a clinic staff member, when adding or editing a pet, I want to see a list of available pet types so I can select the correct one.

**Why this priority**: Ensures consistency and accuracy in pet type selection.

**Independent Test**: Can be tested by navigating to the add or edit pet form and verifying that a dropdown or list displays predefined pet types.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Pet" form, **When** I look at the "Pet Type" field, **Then** I see a list of available pet types such as "Cat", "Dog", "Lizard", "Hamster".

---

### User Story 5 - Add a visit for a pet (Priority: P2)

As a clinic staff member, I want to be able to add a visit record for a pet so that I can track their medical history.

**Why this priority**: Essential for maintaining a complete medical history for each pet.

**Independent Test**: Can be tested by selecting a pet, navigating to the add visit form, filling in valid visit details (description and future date), and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** I am viewing a pet's details, **When** I click "Add Visit" and enter a description "Routine check-up" and a visit date "2027-01-15", **Then** the visit is saved and displayed in the pet's visit history.
2. **Given** I am on the "Add Visit" form for a pet, **When** I enter a visit date that is in the past or today, **Then** the system rejects the booking with a "typeMismatch.visitDate" error, and the form remains open.

---

### Edge Cases

- **Duplicate Pet Name**: Attempting to create or update a pet with a name that already exists for the same owner → system rejects with a "duplicate" error.
- **Missing Pet Name**: Attempting to create or update a pet without providing a name → system rejects with a "required" error.
- **Missing Pet Type**: Attempting to create a new pet without specifying its type → system rejects with a "required" error.
- **Missing Birth Date**: Attempting to create or update a pet without providing a birth date → system rejects with a "required" error.
- **Future Birth Date**: Attempting to create or update a pet with a birth date in the future → system rejects with a "typeMismatch.birthDate" error.
- **Invalid Visit Date**: Attempting to book a visit with a date that is not in the future (i.e., today or in the past) → system rejects with a "typeMismatch.visitDate" error.
- **Non-existent Owner for Visit**: Attempting to book a visit for a pet belonging to a non-existent owner → system throws an `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate the name, type, and birth date of a pet during creation or update.
- **FR-003**: System SHOULD allow updating an existing pet's information.
- **FR-004**: System SHOULD provide a form for creating or updating a pet, pre-populated with owner and pet details if updating.
- **FR-005**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-006**: System MUST allow the creation of a new visit for an existing pet.
- **FR-007**: System MUST validate the description and date of a visit during creation.
- **FR-008**: System MUST ensure that pet names are unique within the context of a single owner.
- **FR-009**: System MUST ensure that pet birth dates are not in the future.
- **FR-010**: System MUST ensure that visit dates are in the future.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an animal owned by a person. Key attributes include name, birth date, and type. It is associated with an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Bird). Key attribute is its name.
- **Visit**: Represents a medical appointment or interaction for a pet. Key attributes include description and date. It is associated with a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create and update pet records in under 1 minute per pet.
- **SC-002**: The system prevents duplicate pet names for the same owner with 100% accuracy.
- **SC-003**: 95% of pet creation and update operations complete without validation errors for valid data.
- **SC-004**: 98% of visit bookings are successful for valid future dates.
- **SC-005**: Reduction in data entry errors for pet types by 75% due to the selection mechanism.

## Assumptions

- Users interacting with the pet management system are authorized clinic staff.
- The system has access to a predefined list of pet types.
- Owners already exist in the system before pets can be added to them.
- The date format for birth dates and visit dates is consistent and parsable.
- Error messages are user-friendly and informative for clinic staff.