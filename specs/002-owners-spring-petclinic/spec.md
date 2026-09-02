# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic system usability.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** no owners are displayed.

---

### User Story 2 - Create a new owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: Adding new owners is a fundamental operation for populating the system with data.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner appears in the list. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields with valid data (first name, last name, address, city, telephone) and click "Submit", **Then** the new owner is saved and the user is redirected to the "Owners" list page, displaying the newly added owner.

---

### User Story 3 - Handle owner creation errors (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then an error message is displayed and the user remains on the creation form.

**Why this priority**: Ensures data integrity and provides user feedback for incorrect input.

**Independent Test**: Can be fully tested by submitting the new owner form with invalid data and verifying error messages. Delivers robust data input handling.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they leave the "Address" field blank and click "Submit", **Then** an error message indicating the address is required is displayed, and the user remains on the "Add Owner" page.
2. **Given** the user is on the "Add Owner" page, **When** they enter "123" for the "Telephone" field and click "Submit", **Then** an error message indicating an invalid telephone format is displayed, and the user remains on the "Add Owner" page.

---

### Edge Cases

- What happens when an owner's telephone number is not exactly 10 digits? → System rejects with validation error.
- How does system handle attempting to edit a non-existent owner ID? → System throws an `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST validate that the owner's address is not blank.
- **FR-004**: System MUST validate that the owner's city is not blank.
- **FR-005**: System MUST validate that the owner's telephone number is exactly 10 digits.
- **FR-006**: System MUST validate that the owner's first name is not blank.
- **FR-007**: System MUST validate that the owner's last name is not blank.
- **FR-008**: System MUST allow searching for owners by last name prefix.
- **FR-009**: System MUST display a list of owners matching the search criteria.
- **FR-010**: System MUST handle cases where no owners match the search criteria.
- **FR-011**: System MUST display appropriate error messages for invalid owner data.
- **FR-012**: System MUST prevent the creation of an owner with a duplicate telephone number. [NEEDS CLARIFICATION: The repository context mentions duplicate pet names, but not duplicate owner telephone numbers. Assuming this is a desired constraint for owners as well.]

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. It has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal owned by an `Owner`. Attributes include name, birth date, and type. It has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a `Pet`. Attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: 95% of invalid owner submissions result in clear, actionable error messages displayed to the user.
- **SC-004**: The system successfully prevents the creation of owners with duplicate telephone numbers.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet data structures.
- The `OwnerRepository` and `PetTypeRepository` are available for data access.
- Standard Spring Boot validation mechanisms will be used.
- The primary database technology is relational.
- The system will use a 10-digit pattern for telephone numbers as a reasonable default.
- The system will prevent duplicate telephone numbers for owners as a reasonable default.