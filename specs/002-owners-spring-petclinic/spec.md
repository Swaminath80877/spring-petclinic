# Feature Specification: Owner Management Enhancements

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-16

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for users to locate existing pet owners, enabling further actions like viewing details or adding pets.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a partial or full last name, submitting, and verifying the displayed list against expected results. Delivers immediate value for owner lookup.

**Acceptance Scenarios**:

1. **Given** the system has owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** the system has owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Jones", **Then** only owner "Jones" is displayed.
3. **Given** the system has no owners with the last name "Williams", **When** the user searches for "Williams", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form with all required fields populated, Then the owner is created and the user is redirected to the owner's details page.

**Why this priority**: This is essential for onboarding new clients and expanding the customer base of the pet clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all valid required fields, submitting, and verifying redirection to a newly created owner's detail page.

**Acceptance Scenarios**:

1. **Given** the user is on the new owner form, **When** they enter a valid first name, last name, address, city, and telephone number, **Then** the owner is successfully created and the user is redirected to the owner's detail page.
2. **Given** the user is on the new owner form, **When** they attempt to submit with a blank address, **Then** a validation error for the address field is displayed, and the owner is not created.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

Given an owner exists, When the user navigates to the owner's detail page and initiates the process to add a new pet, and submits a valid pet form (name, birth date, type), Then the new pet is associated with the owner and displayed on the owner's detail page.

**Why this priority**: This allows pet owners to register their pets, which is a fundamental part of managing pet health records.

**Independent Test**: Can be fully tested by selecting an existing owner, adding a new pet with valid details, and verifying the pet appears on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists, **When** the user adds a new pet named "Buddy" with birth date "2020-05-15" and type "Dog" to "John Doe", **Then** "Buddy" is listed under "John Doe's" pets.
2. **Given** an owner "Jane Smith" exists, **When** the user attempts to add a pet with a blank name, **Then** a validation error for the pet's name is displayed, and the pet is not added.

---

### User Story 4 - Handle Duplicate Pet Name Creation (Priority: P3)

Given an owner exists with a pet named "Max", When a new pet is created for the same owner with the name "Max", Then an error message is displayed indicating the name is a duplicate, and the new pet is not created.

**Why this priority**: Prevents data confusion and ensures unique identification of pets within an owner's record.

**Independent Test**: Can be fully tested by creating a pet for an owner, then attempting to create another pet for the same owner with the identical name, and verifying the duplicate name error.

**Acceptance Scenarios**:

1. **Given** owner "Alice" has a pet named "Whiskers", **When** the user attempts to add another pet named "Whiskers" to "Alice", **Then** an error message "Duplicate pet name" is displayed.
2. **Given** owner "Bob" has a pet named "Buddy", **When** owner "Charlie" has a pet named "Buddy", **And** the user attempts to add a pet named "Buddy" to "Alice", **Then** the creation is successful as the duplicate check is per owner.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error for address.
- **Blank City**: Owner creation/update with a blank city → validation error for city.
- **Invalid Telephone**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error for telephone.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error for name.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error for type.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating the name is already in use.
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format (e.g., "2015/02/12") → `typeMismatch` validation error for birth date.
- **Blank Visit Date**: Visit creation/update with a blank date → validation error for date.
- **Visit Date in the Past**: Visit creation/update with a date that is not after the current date → `typeMismatch.visitDate` validation error for the date field.
- **Non-existent Owner ID for Pet Operations**: Attempting to create or update a pet for an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Non-existent Pet ID for Visit Operations**: Attempting to create or update a visit for a pet with an ID that does not exist for a given owner → `IllegalArgumentException` indicating pet not found for the owner.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow the retrieval of all pet types for populating forms.
- **FR-005**: System SHOULD handle potential data integrity violations when saving pet information.
- **FR-006**: System MUST allow searching for owners by their last name.
- **FR-007**: System MUST allow the creation of new owners with valid personal and contact information.
- **FR-008**: System MUST disallow the creation or update of owners with disallowed `id` fields.
- **FR-009**: System MUST disallow the creation or update of visits with disallowed `id` fields.
- **FR-010**: System MUST prevent duplicate pet names for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents an individual pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Dog, Cat, Bird).
- **Visit**: Represents a scheduled or past visit for a pet, including the date and description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is successful for 99% of valid submissions.
- **SC-003**: Adding a new pet to an owner is successful for 98% of valid submissions.
- **SC-004**: The system correctly identifies and prevents duplicate pet names for the same owner in 100% of cases.
- **SC-005**: Validation errors for owner and pet creation/updates are displayed clearly to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will be used by clinic staff to manage owner and pet information.
- The primary language for the application is English.
- Data integrity for existing owners and pets is assumed to be valid prior to new pet additions.
- The system will be deployed in an environment where database access is reliable.