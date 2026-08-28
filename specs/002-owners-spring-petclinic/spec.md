# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's detail page.

**Why this priority**: This is a core functionality for navigating and viewing existing owner information, essential for basic application usage.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page. Delivers the ability to locate and view specific owner records.

**Acceptance Scenarios**:

1. **Given** the system has an owner with the last name "Franklin", **When** a user searches for owners with the last name "Franklin", **Then** the system displays the detail page for the owner named "Franklin".
2. **Given** the system has multiple owners with the last name "Franklin", **When** a user searches for owners with the last name "Franklin", **Then** the system displays a list of owners with the last name "Franklin".

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Adding new owners is a fundamental operation for managing the clinic's clientele.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting the form, and verifying that the new owner is created and a success confirmation is shown. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields populated correctly, **Then** the new owner is successfully created and displayed on the owner list page.
2. **Given** a user has successfully created a new owner, **When** they navigate to the owner search page and search for the newly created owner's last name, **Then** the new owner appears in the search results.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then the form is redisplayed with error messages.

**Why this priority**: Ensures data integrity and provides user feedback for incorrect input.

**Independent Test**: Can be fully tested by navigating to the new owner form, intentionally submitting invalid data (e.g., blank required fields, invalid phone number), and verifying that the form redisplays with clear error messages indicating the specific fields that need correction. Delivers robust form validation.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** the form is redisplayed with an error message indicating that the address cannot be blank.
2. **Given** a user is on the new owner form, **When** they submit the form with a telephone number that is not 10 digits, **Then** the form is redisplayed with an error message indicating that the telephone number must be 10 digits.

---

### Edge Cases

- What happens when an owner's telephone number is not a 10-digit number? → Validation error for telephone.
- How does the system handle an attempt to edit or view an owner with a non-existent ID? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created or updated with a blank name? → Validation error for name.
- How does the system handle the creation of a pet with a missing pet type? → Validation error for type.
- What happens when attempting to create a pet with a name that already exists for the same owner? → Validation error indicating the name is already in use.
- How does the system handle editing a pet with a blank name? → Validation error for name.
- What happens when editing a pet with an invalid birth date format? → `typeMismatch` validation error for birth date.
- How does the system handle submitting a visit with a date that is not in the future? → Validation error for the visit date.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` indicating the pet was not found for the owner.
- How does the system handle a find owners search with an empty last name? → Returns all owners, paginated.
- What happens when searching for an owner last name that does not exist in the database? → Validation error `notFound` for last name.
- How does the system handle navigating to the `/oups` endpoint? → Throws a `RuntimeException` and displays an error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow the updating of existing pet information.
- **FR-003**: System SHOULD validate pet data upon creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet details.
- **FR-005**: System SHOULD retrieve a list of available pet types for selection.
- **FR-006**: System MUST allow owners to have multiple pets.
- **FR-007**: System MUST allow owners to have multiple visits associated with each pet.
- **FR-008**: System MUST allow searching for owners by their last name.
- **FR-009**: System MUST display owner details, including their pets and visits.
- **FR-010**: System MUST allow creation of new owners.
- **FR-011**: System MUST validate owner details upon creation and update.
- **FR-012**: System MUST display validation errors to the user when owner details are invalid.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet. Key attributes include name, birth date, and pet type. It is associated with an owner and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). It has a name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by their last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Validation errors for owner creation are displayed clearly and immediately upon submission of invalid data.
- **SC-004**: 95% of users can successfully navigate to an owner's detail page after searching by last name.
- **SC-005**: The system supports up to 50 concurrent users browsing owner information without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The existing `Person` class is suitable for owner details and does not require modification for this feature.
- The `NamedEntity` and `BaseEntity` classes from the core model are sufficient for pet and visit entities respectively.
- Standard web application security practices will be applied to protect owner data.
- The application will be deployed in an environment with sufficient resources to handle the expected load.
- Data retention policies for owner information will follow industry best practices for veterinary clinics.
- Error pages for unexpected exceptions (like `/oups`) are user-friendly and provide guidance.