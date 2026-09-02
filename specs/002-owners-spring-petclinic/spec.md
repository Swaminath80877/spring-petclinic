# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information and manage their pets' care.

**Why this priority**: This is a core functionality for managing existing clients and is frequently used.

**Independent Test**: Can be fully tested by entering a last name in the search field and verifying the correct owners are displayed, delivering immediate access to owner details.

**Acceptance Scenarios**:

1. **Given** a list of owners exists, **When** a user searches for owners by the last name "Franklin", **Then** the system displays a list of owners whose last names start with "Franklin" and allows navigation to their detail page.
2. **Given** a list of owners exists, **When** a user searches for a last name that does not exist, **Then** the system displays a "Owner not found" message.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a new client, I want to be able to register as an owner with my contact and address details so that I can register my pets for care.

**Why this priority**: Essential for onboarding new clients to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and listed, delivering the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created, and the user is redirected to the owner's detail page with a success indication.
2. **Given** a user is on the new owner form, **When** they submit an invalid owner form (e.g., blank city), **Then** an error message is displayed indicating the specific validation failure, and the form is re-rendered with the entered data preserved.

---

### User Story 3 - Add a New Pet for an Owner (Priority: P3)

As an existing owner, I want to add a new pet to my account so that I can register them for veterinary services.

**Why this priority**: Allows owners to manage their growing pet family.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to the "Add Pet" section, filling out the pet details, and verifying the pet is associated with the owner, delivering the ability to manage multiple pets per owner.

**Acceptance Scenarios**:

1. **Given** an existing owner is logged in, **When** they navigate to add a new pet and provide valid pet details (name, type, birth date), **Then** the new pet is successfully created and associated with the owner.
2. **Given** an existing owner is logged in, **When** they attempt to add a new pet with a duplicate name for that owner, **Then** a validation error is displayed, and the pet is not created.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → System rejects with validation error.
- What happens when an owner is created/updated with a blank city? → System rejects with validation error.
- What happens when an owner is created/updated with a telephone number not matching the 10-digit pattern? → System rejects with validation error.
- What happens when a pet is created/updated with a blank name? → System rejects with validation error.
- What happens when a pet is created/updated without selecting a pet type? → System rejects with validation error.
- What happens when a pet is created/updated without providing a birth date? → System rejects with validation error.
- What happens when attempting to create a pet with a name that already exists for the same owner? → System rejects with validation error.
- What happens when submitting a visit with a date in the past? → System rejects with validation error.
- What happens when attempting to access or modify data for a non-existent owner ID? → System throws an `IllegalArgumentException` and displays an appropriate error message.
- What happens when attempting to access or modify a pet for an owner where the pet ID does not exist? → System throws an `IllegalArgumentException` and displays an appropriate error message.
- What happens when navigating to the "/oups" endpoint? → System throws a `RuntimeException` and displays an error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the updating of an existing owner's information.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and type.
- **FR-004**: System MUST allow the updating of an existing pet's information.
- **FR-005**: System MUST validate owner information before saving (address, city, telephone).
- **FR-006**: System MUST validate pet information before saving (name, birth date, type).
- **FR-007**: System SHOULD display a list of available pet types when creating or updating a pet.
- **FR-008**: System SHOULD handle cases where an owner is not found when attempting to add or update a pet.
- **FR-009**: System MUST allow searching for owners by last name.
- **FR-010**: System MUST display a list of owners matching a search query.
- **FR-011**: System MUST display a "not found" message if no owners match a search query.
- **FR-012**: System MUST allow viewing the details of a specific owner, including their pets.
- **FR-013**: System MUST allow adding a visit for a pet.
- **FR-014**: System MUST validate visit information before saving (date).
- **FR-015**: System MUST allow triggering an exception via the "/oups" endpoint for testing error handling.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns pets. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal under the care of the clinic. Key attributes include name, birth date, and type. A pet belongs to an owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Key attribute is the name of the type.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and description. A visit is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for owners by last name and view their details in under 5 seconds.
- **SC-002**: New owners can be created with all required information in under 3 minutes.
- **SC-003**: New pets can be added to an existing owner's record in under 2 minutes.
- **SC-004**: 95% of owner and pet data entries pass validation checks on the first attempt.
- **SC-005**: The system displays clear and actionable error messages for 100% of validation failures.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) will be handled separately.
- The primary users are clinic staff and potentially new clients registering.
- Data for existing owners and pets will be migrated or available.
- The system will use a relational database for persistence.
- Error pages for exceptions like "/oups" are handled by a dedicated system component.