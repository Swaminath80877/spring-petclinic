# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `020-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name in the search form and verifying that the correct owner(s) are displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the last name field and click "Search", **Then** the system displays a list of owners whose last name starts with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist, **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to be able to create a new owner record so that I can onboard new clients.

**Why this priority**: Essential for adding new clients to the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid details (first name, last name, address, city, telephone) and click "Add Owner", **Then** a new owner is created and I am redirected to the owner's details page.

---

### User Story 3 - Add a New Pet to an Owner (Priority: P3)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: Important for managing an owner's complete profile.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the "Add Pet" action, filling out the pet form with valid data, and verifying the pet is added to the owner's record.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add Pet", fill out the pet form with a name, birth date, and select a pet type, and click "Add Pet", **Then** the new pet is associated with the owner and displayed in their pet list.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error is displayed.
- What happens when an owner is created or updated with a blank last name? → Validation error is displayed.
- What happens when an owner is created or updated with a blank address? → Validation error is displayed.
- What happens when an owner is created or updated with a blank city? → Validation error is displayed.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → Validation error is displayed.
- How does the system handle an attempt to find or edit an owner with an ID that does not exist in the database? → An `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error is displayed.
- What happens when a pet is created or updated without selecting a pet type? → Validation error is displayed.
- What happens when a pet is created or updated with a null birth date? → Validation error is displayed.
- What happens when a user attempts to add a pet with a name that already exists for the same owner? → Validation error is displayed for the pet's name, indicating a duplicate.
- What happens when a visit is created with a date that is not in the future? → Validation error is displayed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST display a list of owners matching the search criteria.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-005**: System MUST allow the update of an existing pet's details.
- **FR-006**: System SHOULD validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-007**: System SHOULD validate pet information (name, birth date, pet type) before saving.
- **FR-008**: System SHOULD display a form to create or update a pet, pre-populated with owner and pet details if updating.
- **FR-009**: System SHOULD provide a list of available pet types for selection when creating or updating a pet.
- **FR-010**: System MUST handle attempts to add a pet with a duplicate name for the same owner by displaying an error.
- **FR-011**: System MUST handle attempts to find or edit a non-existent owner ID by throwing an `IllegalArgumentException`.
- **FR-012**: System MUST handle attempts to create a visit with an invalid date by displaying an error.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, containing personal details like name, address, and contact information. It has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal belonging to an owner. It includes details such as name, birth date, and type. It has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat). It has a name.
- **Visit**: Represents a visit to the clinic for a pet, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed within 1 minute of form submission.
- **SC-003**: 95% of pet creation attempts for existing owners are successful.
- **SC-004**: Validation errors for owner and pet forms are displayed to the user within 1 second of submission.
- **SC-005**: The system correctly identifies and prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data retention policies for owner and pet information will follow industry-standard practices for veterinary clinics unless otherwise specified.
- The primary users of this feature are clinic staff.