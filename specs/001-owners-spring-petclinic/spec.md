# Feature Specification: Owner Management

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-10

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing the clinic's client base and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Davis" into the last name search field and click "Search", **Then** the system displays a list of owners whose last names start with "Davis".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist in the system and click "Search", **Then** the system displays a "Owner not found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record so that I can register new clients.

**Why this priority**: This is fundamental to onboarding new customers into the system.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in valid details, submitting the form, and verifying the owner's details page is displayed.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form, **When** I enter valid owner details (first name, last name, address, city, telephone) and click "Add Owner", **Then** the new owner is created and I am redirected to the owner's details page.
2. **Given** I am on the "Add Owner" form, **When** I leave the "Address" field blank and click "Add Owner", **Then** a validation error is displayed for the address field.
3. **Given** I am on the "Add Owner" form, **When** I enter a telephone number with more or less than 10 digits and click "Add Owner", **Then** a validation error is displayed for the telephone field.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: This is a common task for managing an owner's pets and is important for comprehensive record-keeping.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet list, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add New Pet", **And** I enter a pet name, birth date, and select a pet type, **And** I click "Add Pet", **Then** the new pet is successfully added to the owner's record.
2. **Given** I am viewing the details of an existing owner, **When** I attempt to add a pet with a blank name and click "Add Pet", **Then** a validation error is displayed for the pet's name.
3. **Given** I am viewing the details of an existing owner, **When** I attempt to add a pet without selecting a pet type and click "Add Pet", **Then** a validation error is displayed for the pet type.

---

### User Story 4 - Update an Existing Owner's Information (Priority: P2)

As a clinic staff member, I want to update an existing owner's information so that I can keep their contact details current.

**Why this priority**: Maintaining accurate owner information is crucial for communication and record-keeping.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their edit page, modifying details, and saving the changes.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Edit Owner", **And** I modify the owner's telephone number, **And** I click "Update Owner", **Then** the owner's telephone number is updated.
2. **Given** I am viewing the details of an existing owner, **When** I click "Edit Owner", **And** I clear the owner's city and click "Update Owner", **Then** a validation error is displayed for the city field.

---

### User Story 5 - View Owner Details (Priority: P1)

As a clinic staff member, I want to view the details of a specific owner, including their pets and visits, so that I have a complete overview of their information.

**Why this priority**: This is a fundamental requirement for accessing and managing owner and pet data.

**Independent Test**: Can be fully tested by finding an owner and verifying all their associated information is displayed correctly.

**Acceptance Scenarios**:

1. **Given** an owner exists with associated pets and visits, **When** I search for and select that owner, **Then** the system displays the owner's full name, address, city, telephone, and a list of their pets with their respective types and birth dates.
2. **Given** an owner exists with associated pets and visits, **When** I view the owner's details, **Then** each pet listed also displays its associated visits.

---

### Edge Cases

- What happens when an owner is created or updated with an `id` field? → Validation error.
- What happens when a visit is created or updated with an `id` field? → Validation error.
- What happens when a pet is created for an owner, but the pet's name is a duplicate of an existing pet for that same owner? → Validation error indicating a duplicate name.
- What happens when attempting to edit or access details for an owner ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when accessing the `/oups` endpoint? → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow finding owners by their last name.
- **FR-003**: System MUST allow updating an existing owner's information.
- **FR-004**: System MUST allow retrieving a specific owner and displaying their associated pets.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-006**: System MUST validate owner information during creation or update, enforcing non-blank fields for address and city, and a 10-digit format for telephone.
- **FR-007**: System MUST validate pet information during creation, enforcing a non-blank name and a valid pet type.
- **FR-008**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-009**: System MUST disallow the `id` field when creating or updating an owner.
- **FR-010**: System MUST disallow the `id` field when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, containing personal contact information and a list of their pets. Key attributes include first name, last name, address, city, and telephone.
- **Pet**: Represents an animal belonging to an owner. Key attributes include name, birth date, and type. It is associated with an Owner and can have multiple Visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Key attribute is its name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner's details page completes in under 5 seconds.
- **SC-003**: 95% of new pet creations for existing owners are successful on the first attempt.
- **SC-004**: Owner information updates are reflected immediately upon saving.
- **SC-005**: The system successfully handles 100 concurrent requests for owner lookups without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data validation rules for address and city being non-blank are sufficient for initial implementation.
- The 10-digit telephone number format is a strict requirement.
- Pet names are case-sensitive when checking for duplicates within the same owner.
- The system will provide user-friendly error messages for validation failures.
- The `id` field is disallowed for creation/update operations as a security measure to prevent manual ID manipulation.
- The `/oups` endpoint is intended to simulate an internal server error for testing purposes.