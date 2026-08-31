# Feature Specification: owners for spring-petclinic

**Feature Branch**: `008-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing clinic operations and is essential for day-to-day tasks.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" search field and click "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist in the system and click "Search", **Then** a "not found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record so that I can register new clients.

**Why this priority**: This is fundamental to onboarding new clients into the system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid owner details, submitting the form, and verifying the owner is created and redirected to their details page.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid owner details (first name, last name, address, city, telephone) and click "Add Owner", **Then** the owner is created, and I am redirected to the owner's details page.
2. **Given** I am on the "New Owner" form, **When** I attempt to submit the form with a blank first name, **Then** a validation error is displayed for the first name field, and the form is re-rendered.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage their animals.

**Why this priority**: This is a common task for existing clients who acquire new pets.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, initiating the process to add a new pet, filling in valid pet details, and verifying the pet is added to the owner's record.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add New Pet", **And** I enter a valid pet name, select a pet type (e.g., "Dog"), and enter a birth date, **Then** the new pet is successfully added to the owner's record.
2. **Given** I am viewing the details of an existing owner, **When** I attempt to add a new pet with a name that already exists for that owner, **Then** an error message indicating a duplicate name is displayed, and the pet creation form is re-rendered.

---

### User Story 4 - Update an Existing Pet's Information (Priority: P2)

As a clinic staff member, I want to be able to update an existing pet's information so that I can keep records accurate.

**Why this priority**: Allows for correction of errors or updating details like a pet's name.

**Independent Test**: Can be fully tested by navigating to an owner's details page, selecting a pet to edit, changing a field (e.g., name), saving the changes, and verifying the update.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an owner with an existing pet, **When** I click "Edit" for that pet, **And** I change the pet's name to "Buddy" and click "Update Pet", **Then** the pet's name is updated to "Buddy" on the owner's details page.

---

### User Story 5 - Book a Visit for a Pet (Priority: P3)

As a clinic staff member, I want to be able to book a visit for a pet so that I can schedule appointments.

**Why this priority**: Essential for managing the clinic's appointment schedule.

**Independent Test**: Can be fully tested by navigating to a pet's details, initiating a visit booking, entering a valid date and description, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of a pet, **When** I click "Add Visit", **And** I enter a future date and a description like "Annual check-up", **Then** the visit is successfully booked and displayed for the pet.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → system rejects with validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → system rejects with validation error.
- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → system throws `IllegalArgumentException`.
- **No Owners Found**: Searching for owners with a last name that yields no results → system displays a "not found" error message.
- **Blank Pet Name**: Creating or updating a pet with a blank name → system rejects with "required" validation error.
- **Missing Pet Type**: Creating a pet without specifying a pet type → system rejects with "required" validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with "duplicate" validation error.
- **Invalid Pet Birth Date**: Creating or updating a pet with an invalid birth date format → system rejects with "typeMismatch" validation error.
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → system rejects with "typeMismatch.visitDate" validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → system throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the creation of a new pet for an existing owner.
- **FR-003**: System MUST allow the update of an existing pet's name.
- **FR-004**: System MUST allow the booking of a visit for a pet.
- **FR-005**: System MUST allow searching for owners by last name.
- **FR-006**: System SHOULD validate owner information (first name, last name, address, city, telephone) during creation or update.
- **FR-007**: System SHOULD validate pet information (name, type, birth date) during creation or update.
- **FR-008**: System SHOULD validate visit information (date, description) during booking.
- **FR-009**: System SHOULD provide a list of available pet types for selection during pet creation/update.
- **FR-010**: System SHOULD handle potential data integrity violations when saving owner, pet, or visit information.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a client of the veterinary clinic. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal belonging to an owner. Attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog, Hamster). A pet type can be associated with multiple pets.
- **Visit**: Represents a veterinary visit for a pet. Attributes include date and description. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed successfully with valid data in under 5 seconds.
- **SC-003**: New pets can be added to an owner's record in under 4 seconds.
- **SC-004**: Visits can be booked for a pet in under 4 seconds.
- **SC-005**: 95% of owner searches return results or a "not found" message within the specified time.
- **SC-006**: Validation errors for owner and pet creation/updates are displayed clearly to the user within 1 second of submission.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication and authorization mechanisms will be leveraged if applicable (though not explicitly detailed in this feature description).
- The project will use standard Spring Boot conventions for data persistence and web handling.
- The "owners" module is intended to be a core part of the Spring PetClinic application.
- The telephone number format `\d{10}` is the only supported format for owner telephones.
- The date format `yyyy-MM-dd` is the only supported format for pet and visit dates.