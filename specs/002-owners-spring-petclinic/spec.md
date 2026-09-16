# Feature Specification: Owner Management for Spring PetClinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then the system displays a list of owners whose last names start with the entered value.

**Why this priority**: This is a core functionality for navigating and managing existing owners, essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct owner(s) are displayed. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Smith" into the last name search field and click "Search", **Then** a list of owners whose last names start with "Smith" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist in the system and click "Search", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then a new owner is created and the user is redirected to the owner's details page.

**Why this priority**: This is fundamental for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting, and verifying redirection to the newly created owner's detail page. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is created and the user is redirected to the details page for that owner.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a blank address and click "Add Owner", **Then** a validation error message is displayed for the address field, and the owner is not created.
3. **Given** the user is on the "New Owner" form, **When** they attempt to submit the form with a telephone number that is not 10 digits and click "Add Owner", **Then** a validation error message is displayed for the telephone field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists in the system, When the user navigates to the owner's details page, Then all the owner's information, including their pets, is displayed.

**Why this priority**: Essential for accessing and reviewing all information related to a specific owner and their pets.

**Independent Test**: Can be fully tested by finding an existing owner, clicking on their name/link, and verifying all their details and associated pets are displayed correctly. Delivers the ability to view owner and pet information.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with associated pets, **When** the user navigates to John Doe's owner details page, **Then** the owner's first name, last name, address, city, telephone, and a list of their pets (including pet names and birth dates) are displayed.

---

### User Story 4 - Create a New Pet for an Existing Owner (Priority: P2)

Given a user is viewing an owner's details page, When they choose to add a new pet and submit valid pet information, Then the new pet is associated with the owner.

**Why this priority**: Allows owners to register new pets under their existing account.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, initiating the "Add Pet" action, filling in valid pet details, and verifying the new pet appears in the owner's pet list. Delivers the ability to add pets to an owner's record.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details page for owner "Jane Smith", **When** they click "Add New Pet", fill in the pet's name, birth date, and select a pet type, and click "Add Pet", **Then** the new pet is displayed in Jane Smith's list of pets.
2. **Given** the user is viewing the details page for owner "Jane Smith", **When** they attempt to add a pet with a blank name and click "Add Pet", **Then** a validation error message is displayed for the pet name, and the pet is not added.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P3)

Given a user is viewing an owner's details page with pets, When they choose to edit a pet and submit updated information, Then the pet's details are updated.

**Why this priority**: Allows for correction or modification of pet information.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, selecting a pet to edit, changing a detail (e.g., birth date), saving, and verifying the updated information is displayed. Delivers the ability to modify pet records.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details page for owner "Jane Smith" and her pet "Buddy", **When** they choose to edit "Buddy", change the birth date, and click "Update Pet", **Then** the updated birth date for "Buddy" is displayed.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address?
  System rejects with validation error.
- What happens when an owner is created/updated with a blank city?
  System rejects with validation error.
- What happens when an owner is created/updated with a telephone number not matching the 10-digit pattern?
  System rejects with validation error.
- What happens when attempting to edit an owner with an ID that does not exist?
  System throws `IllegalArgumentException`.
- What happens when a pet is created/updated with a blank name?
  System rejects with validation error.
- What happens when a pet is created with a missing pet type?
  System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner?
  System rejects with validation error.
- What happens when a pet is created/updated with an invalid birth date format?
  System rejects with validation error.
- What happens when a pet is created/updated with a blank birth date?
  System rejects with validation error.
- What happens when attempting to add a visit for a non-existent owner?
  System throws `IllegalArgumentException`.
- What happens when attempting to add a visit for a non-existent pet of an owner?
  System throws `IllegalArgumentException`.
- What happens when searching for owners with a last name that does not exist in the database?
  System displays a "not found" error message.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's details.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD display a list of pet types when creating or updating a pet.
- **FR-005**: System SHOULD handle cases where an owner is not found when attempting to add a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details.
- **FR-008**: System MUST allow searching for owners by last name.
- **FR-009**: System MUST display owner details, including their pets.
- **FR-010**: System MUST validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-011**: System MUST validate pet information (name, birth date) before saving.
- **FR-012**: System MUST enforce that a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with Pets.
- **Pet**: Represents a pet belonging to an owner. Attributes include name and birth date. Has a many-to-one relationship with Owner and PetType, and a one-to-many relationship with Visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Inherits from NamedEntity.
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date. Has a many-to-one relationship with Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created and their details viewed within 1 minute of form submission.
- **SC-003**: Adding a new pet to an existing owner takes less than 30 seconds from initiating the action to seeing the pet listed.
- **SC-004**: 95% of owner and pet data entry operations complete successfully without validation errors when valid data is provided.
- **SC-005**: The system correctly displays all associated pets when viewing an owner's details.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard web application security practices will be applied.
- Data retention policies for owner and pet information will follow industry best practices for veterinary clinics unless otherwise specified.
- The system will use a relational database for persistence.
- The primary users are clinic staff responsible for managing owner and pet information.