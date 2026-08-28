# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `007-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly find their contact information and pet details.

**Why this priority**: This is a core functionality for managing owner information and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page,
   **When** I enter "Davis" into the "Last name" search field and click "Search",
   **Then** the system displays a list of owners whose last names start with "Davis", including their first name, address, city, and telephone.

2. **Given** I am on the "Find Owners" page,
   **When** I enter a last name that does not exist in the system (e.g., "NonExistent"),
   **Then** the system displays a message indicating that no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients and expanding the clinic's database.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in valid details, submitting, and verifying the owner is created and displayed on their details page. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form,
   **When** I enter valid details for a new owner (First Name: "John", Last Name: "Doe", Address: "123 Main St", City: "Anytown", Telephone: "1234567890") and click "Add Owner",
   **Then** the new owner "John Doe" is created and I am redirected to their owner details page.

2. **Given** I am on the "Add Owner" form,
   **When** I attempt to submit the form with a blank "Last Name" and click "Add Owner",
   **Then** the system displays a validation error message indicating that the last name is required, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet for an existing owner so that I can keep track of all their animals.

**Why this priority**: Important for maintaining a complete record of an owner's pets.

**Independent Test**: Can be fully tested by navigating to an existing owner's details page, initiating the "Add Pet" action, filling in valid pet details, and verifying the new pet appears on the owner's details page. Delivers the ability to associate pets with owners.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists in the system,
   **When** I navigate to John Doe's owner details page, click "Add Pet", and enter valid pet details (Name: "Buddy", Birth Date: "2023-01-15", Type: "Dog") and click "Add Pet",
   **Then** the new pet "Buddy" is associated with John Doe and appears on his owner details page.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

As a clinic staff member, when adding a pet for an owner, I want the system to prevent me from creating a pet with a name that already exists for that same owner, so that pet names are unique per owner.

**Why this priority**: Ensures data integrity and avoids confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by adding a pet for an owner, then attempting to add another pet for the same owner with the exact same name. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" has a pet named "Max" (a dog),
   **When** I navigate to Jane Smith's owner details page, click "Add Pet", and attempt to add another pet with the name "Max" (a cat) and click "Add Pet",
   **Then** the system displays a validation error message "The name of this pet must be unique", and the duplicate pet is not created.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the "\\d{10}" pattern → validation error.
- **Blank Owner Last Name**: Owner search with a blank last name → returns all owners.
- **Non-existent Owner ID**: Accessing an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not after the current date → validation error.
- **Non-existent Owner ID for Visit**: Attempting to add a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the "/oups" endpoint → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST display a form to create or update a pet, pre-populated with owner details.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD allow the application to switch languages using a URL parameter.
- **FR-005**: System SHOULD provide a welcome page accessible at the root URL.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST allow the creation of new owners with their contact details.
- **FR-008**: System MUST prevent the creation of a pet with a duplicate name for the same owner.
- **FR-009**: System MUST disallow the ID field for binding when creating or updating an owner.
- **FR-010**: System MUST disallow the ID field for binding when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal contact information and a list of their pets.
- **Pet**: Represents an individual pet, linked to an owner, with details like name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be successfully created and displayed on their details page within 5 seconds.
- **SC-003**: 99% of attempts to create a duplicate pet name for the same owner result in a clear validation error.
- **SC-004**: The system successfully handles 100 concurrent requests for owner searches without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for data persistence.
- Standard web browser compatibility is assumed.
- The project will use Spring Boot and Spring Data JPA.
- Internationalization (i18n) support will be implemented using standard Spring mechanisms.