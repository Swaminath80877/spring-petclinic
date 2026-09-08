# Feature Specification: Owner Management for Spring PetClinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners, allowing users to quickly locate specific owner information.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" in the "Last Name" field, **Then** the system displays the details for the owner named Franklin.
2. **Given** no owner with the last name "Smith" exists in the system, **When** a user navigates to the owner search page and enters "Smith" in the "Last Name" field, **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - View a List of Owners (Priority: P2)

Given multiple owners exist, When a user navigates to the owners list page, Then all owners are displayed.

**Why this priority**: Provides an overview of all registered owners, useful for administrative purposes and general browsing.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed with their relevant details.

**Acceptance Scenarios**:

1. **Given** at least three owners exist in the system, **When** a user navigates to the owners list page, **Then** all owners are displayed, showing their first name, last name, address, city, and telephone number.

---

### User Story 3 - Create a New Owner (Priority: P3)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Essential for onboarding new pet owners into the system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the owner is created and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone number, and submit the form, **Then** the new owner is successfully created and displayed on the owners list page, and a success message is shown.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address?
- What happens when an owner is created or updated with a blank telephone number?
- How does the system handle an owner's telephone number that does not match the 10-digit pattern?
- What happens when a pet is created or updated with a blank name?
- How does the system handle a pet creation or update where the pet type is missing?
- What happens when a pet is created or updated with an invalid (null) birth date?
- How does the system handle an attempt to add a pet with a name that already exists for the same owner?
- What happens when a visit is submitted with a date that is not in the future?
- How does the system handle operations (e.g., adding a pet or visit) attempted for an owner ID that does not exist?
- How does the system handle operations (e.g., adding a visit) attempted for a pet ID that does not exist for a given owner?
- What happens when the "/oups" endpoint is accessed?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone number.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST validate that the owner's address is not blank.
- **FR-004**: System MUST validate that the owner's city is not blank.
- **FR-005**: System MUST validate that the owner's telephone number is exactly 10 digits.
- **FR-006**: System MUST validate that the owner's first name is not blank.
- **FR-007**: System MUST validate that the owner's last name is not blank.
- **FR-008**: System MUST allow searching for owners by their last name.
- **FR-009**: System MUST display a list of all owners.
- **FR-010**: System MUST allow the creation of a new pet for an existing owner.
- **FR-011**: System MUST allow the update of an existing pet's details.
- **FR-012**: System SHOULD validate pet information during creation or update.
- **FR-013**: System SHOULD display a form to create or update a pet, pre-populated with owner details.
- **FR-014**: System SHOULD provide a list of available pet types for selection during pet creation or update.
- **FR-015**: System MUST validate that a pet's name is not blank.
- **FR-016**: System MUST validate that a visit's description is not blank.
- **FR-017**: System MUST validate that a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes fields for address, city, and telephone number. Has a relationship with `Pet`.
- **Pet**: Represents a pet. Includes fields for birth date and type. Has relationships with `Owner` and `Visit`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic. Includes a field for the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 5 seconds.
- **SC-002**: The owner list page loads and displays all owners within 3 seconds.
- **SC-003**: New owner creation form submission and successful creation completes in under 10 seconds.
- **SC-004**: 99% of owner and pet data entries adhere to validation rules (e.g., 10-digit phone number, non-blank fields).

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard web application security practices will be followed.
- The existing `Person` class from `org.springframework.samples.petclinic.model` will be extended for owner details.
- The `NamedEntity` and `BaseEntity` classes from `org.springframework.samples.petclinic.model` will be used for `Pet` and `Visit` respectively.
- The date format for `birthDate` and `date` fields will be "yyyy-MM-dd".
- The system will use a relational database for persistence.
- Error messages for validation failures will be user-friendly and displayed near the relevant form fields.
- The system will handle concurrent access to owner data gracefully.