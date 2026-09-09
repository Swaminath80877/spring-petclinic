# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-09

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Manage Owner Details (Priority: P1)

As a clinic administrator, I want to be able to view, add, and edit owner details so that I can maintain accurate records of our clients.

**Why this priority**: This is a core functionality for managing the clinic's client base.

**Independent Test**: Can be fully tested by navigating to owner management pages, creating a new owner, editing an existing owner, and verifying the changes. Delivers the fundamental ability to manage owner information.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter a valid owner's last name and click "Search", **Then** I should see a list of owners matching that last name.
2. **Given** I am on the "Find Owners" page, **When** I click "Add Owner", **Then** I should be presented with a form to enter new owner details.
3. **Given** I am on the "Add Owner" form, **When** I fill in all required fields with valid data and click "Add Owner", **Then** the new owner should be created and I should be redirected to their details page.
4. **Given** I am viewing an existing owner's details, **When** I click "Edit Owner", **Then** I should be presented with a form pre-populated with their current details.
5. **Given** I am on the "Edit Owner" form, **When** I update some details and click "Update Owner", **Then** the owner's information should be updated and I should be redirected to their details page.

---

### User Story 2 - Manage Pet Details for an Owner (Priority: P2)

As a clinic administrator, I want to be able to add and edit pet details for an existing owner so that I can keep track of their animals.

**Why this priority**: This is essential for associating pets with their owners and managing animal-specific information.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet to their record, editing an existing pet's details, and verifying the changes. Delivers the ability to manage pet information linked to owners.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's details, **When** I click "Add Pet", **Then** I should be presented with a form to enter new pet details, including selecting a pet type.
2. **Given** I am on the "Add Pet" form, **When** I fill in all required pet fields with valid data and select a pet type, **Then** the new pet should be added to the owner's record and displayed on their details page.
3. **Given** I am viewing an owner's details and they have existing pets, **When** I click "Edit" next to a specific pet, **Then** I should be presented with a form pre-populated with that pet's current details.
4. **Given** I am on the "Edit Pet" form, **When** I update the pet's details and click "Update Pet", **Then** the pet's information should be updated and displayed on the owner's details page.

---

### User Story 3 - Handle Duplicate Pet Names (Priority: P3)

As a clinic administrator, when adding a new pet for an owner, I want the system to prevent me from adding a pet with a name that already exists for that same owner, so that pet names are unique per owner.

**Why this priority**: Ensures data integrity and avoids confusion when managing multiple pets for a single owner.

**Independent Test**: Can be tested by attempting to add a second pet with the same name as an existing pet for a given owner. Delivers a crucial data validation rule.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add another pet for the same owner and enter "Buddy" as the name, **Then** the system should display an error message indicating that a pet with this name already exists for this owner, and the new pet should not be created.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the "\\d{10}" regex → validation error.
- **Blank Owner First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Owner Last Name**: Owner creation/update with a blank last name → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date that does not match the expected format → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Submitting a visit with a date that is not in the future → validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` indicating pet not found.
- **Exception Trigger**: Navigating to the "/oups" endpoint → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System SHOULD validate owner information before saving (address, city, telephone).
- **FR-006**: System SHOULD validate pet information before saving (name, type, birth date).
- **FR-007**: System SHOULD display a form for creating or updating owner details.
- **FR-008**: System SHOULD display a form for creating or updating pet details.
- **FR-009**: System SHOULD populate a dropdown with available pet types when creating or updating a pet.
- **FR-010**: System MUST prevent the creation of a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Person**: Represents an individual with basic contact information (first name, last name, address, city, telephone).
- **Owner**: Extends Person, representing a client of the pet clinic. Can have multiple pets.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog, Hamster).
- **Pet**: Represents an animal owned by an Owner. Has a name, birth date, and type. Can have multiple visits.
- **Visit**: Represents a single visit to the clinic for a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully add and edit owner details in under 1 minute.
- **SC-002**: Users can successfully add and edit pet details for an owner in under 1.5 minutes.
- **SC-003**: 100% of owner and pet creation/update attempts with invalid data result in clear validation error messages.
- **SC-004**: The system successfully prevents duplicate pet names for the same owner in 100% of attempts.
- **SC-005**: The system correctly displays all associated pets when viewing an owner's details.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing Person base class for Owner details.
- The system will use standard web form validation for all input fields.
- The list of available PetTypes is managed elsewhere and will be provided to the pet creation/update forms.
- The system will use standard JPA for data persistence.