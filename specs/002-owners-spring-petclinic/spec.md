# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer relationships and is frequently used.

**Independent Test**: Can be fully tested by entering a last name in the search form and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the "Last Name" field and click "Search", **Then** I should see a list of owners whose last name is "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist, **Then** I should see a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to add new owners to the system so that I can register new clients.

**Why this priority**: Essential for onboarding new customers.

**Independent Test**: Can be fully tested by filling out the "New Owner" form with valid data and verifying the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** I am on the "New Owner" form, **When** I enter valid owner details (First Name, Last Name, Address, City, Telephone) and click "Add Owner", **Then** the new owner is created and I am redirected to the owner's details page.
2. **Given** I am on the "New Owner" form, **When** I leave the "First Name" field blank and click "Add Owner", **Then** I should see a validation error message for the "First Name" field.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage all of a client's animals.

**Why this priority**: Important for maintaining complete owner and pet records.

**Independent Test**: Can be fully tested by navigating to an owner's details, adding a new pet with valid information, and verifying the pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an existing owner exists, **When** I navigate to the owner's details page and click "Add New Pet", **Then** I should be presented with a form to add a new pet.
2. **Given** I am on the "Add New Pet" form for an owner, **When** I enter a valid pet name, select a pet type, and provide a birth date, and click "Add Pet", **Then** the new pet is added to the owner's record.

---

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

As a clinic staff member, I want to be able to update an existing pet's details so that I can keep their information accurate.

**Why this priority**: Ensures data accuracy for pets.

**Independent Test**: Can be fully tested by navigating to an owner's details, selecting a pet to edit, changing a detail (e.g., birth date), saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** an owner has an existing pet, **When** I navigate to the owner's details page and click "Edit" next to the pet's name, **Then** I should be presented with a form to edit the pet's details.
2. **Given** I am on the "Edit Pet" form, **When** I change the pet's birth date and click "Update Pet", **Then** the pet's birth date is updated in the system.

---

### User Story 5 - Handle Duplicate Pet Name Creation (Priority: P3)

As a clinic staff member, I want the system to prevent me from adding a pet with a name that already exists for the same owner, so that pet names are unique per owner.

**Why this priority**: Prevents data confusion and ensures unique identification of pets within an owner's profile.

**Independent Test**: Can be fully tested by attempting to add a pet with a name that already exists for the owner and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner has a pet named "Buddy", **When** I attempt to add another pet for the same owner and enter "Buddy" as the name, **Then** I should see an error message stating "Pet name must be unique for this owner."

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation or update with a blank name → validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-004**: System MUST allow the update of an existing pet's details, including name, birth date, and pet type.
- **FR-005**: System MUST validate owner information before saving (first name, last name, address, city, telephone).
- **FR-006**: System MUST validate pet information before saving (name, birth date, pet type).
- **FR-007**: System MUST display a form for creating or updating owner information.
- **FR-008**: System MUST display a form for creating or updating pet information.
- **FR-009**: System MUST populate a dropdown list with available pet types for selection when adding or editing a pet.
- **FR-010**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-011**: System MUST disallow the 'id' field when creating or updating an owner or pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets, including their contact information (name, address, city, telephone).
- **Pet**: Represents an animal owned by an owner, including its name, birth date, and type.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be successfully created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an owner's record in under 2 minutes.
- **SC-004**: 95% of pet updates are completed successfully without errors.
- **SC-005**: Validation errors for owner and pet creation/updates are displayed clearly and immediately upon submission.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `NamedEntity` and `BaseEntity` for common fields.
- The `OwnerRepository`, `PetRepository`, and `PetTypeRepository` are available and functional.
- The `PetValidator` is available for pet data validation.
- The `OwnerController` and `PetController` will handle the user interface and business logic orchestration.
- The `WebConfiguration` and `CacheConfiguration` are correctly set up for the application.
- The project uses standard Spring Boot conventions for data binding and validation.