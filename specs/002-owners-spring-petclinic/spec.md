# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic system usability.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list matches the expected owners, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** the owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** a message indicating no owners were found is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Creating new owners is fundamental to populating the system with data and enabling other owner-related functionalities.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner is saved and the user is redirected to their detail page, delivering the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Save", **Then** the new owner is created and the user is redirected to the owner's details page.
2. **Given** the user is on the "Add Owner" page, **When** they attempt to submit the form with a blank "telephone" field, **Then** a validation error message "required" is displayed for the telephone field, and the form is re-rendered.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists with existing pets, When a user attempts to add a new pet for that owner with a unique name, Then the new pet is successfully added to the owner's record.

**Why this priority**: Managing pets is a key aspect of the veterinary clinic's operations, directly impacting owner and pet care.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with a unique name and valid type, and confirming its addition, delivering the ability to register new pets for clients.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with no pets, **When** the user navigates to add a pet for "John Doe", fills in a pet name "Buddy", selects "Dog" as the type, and saves, **Then** "Buddy" is listed as a pet for "John Doe".
2. **Given** an owner "Jane Smith" exists with a pet named "Whiskers", **When** the user navigates to add a new pet for "Jane Smith", enters the name "Whiskers" again, and attempts to save, **Then** a validation error message "duplicate" is displayed for the pet name, and the form is re-rendered.

---

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

Given a pet exists for an owner, When a user edits the pet's details and saves, Then the pet's information is updated.

**Why this priority**: Allows for correction of errors or updating information about a pet, ensuring data accuracy.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying one of its details (e.g., name or type), saving the changes, and verifying the update, delivering the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy" of type "Dog", **When** the user edits "Buddy"'s details, changes the type to "Golden Retriever", and saves, **Then** the pet's type is updated to "Golden Retriever".
2. **Given** an owner "Jane Smith" has a pet named "Whiskers", **When** the user edits "Whiskers"'s details and attempts to save with a blank name, **Then** a validation error message "required" is displayed for the pet name, and the form is re-rendered.

---

### User Story 5 - Handle Duplicate Pet Name for an Owner (Priority: P3)

Given an owner exists with existing pets, When a user attempts to add a new pet with a name that already exists for that owner, Then an error message indicating a duplicate name is displayed, and the form is re-rendered.

**Why this priority**: Prevents data integrity issues by ensuring pet names are unique within an owner's record.

**Independent Test**: Can be fully tested by attempting to add a pet with a name that already exists for the owner and confirming the duplicate name error is shown, delivering data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user attempts to add another pet for "John Doe" with the name "Buddy", **Then** a validation error message "duplicate" is displayed for the pet name, and the form is re-rendered.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with a telephone number not matching the 10-digit pattern? → Validation error.
- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error "required".
- What happens when a pet is created with a missing pet type? → Validation error "required".
- What happens when a pet is created or updated with an invalid birth date format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when a pet is created or updated with a null birth date? → Validation error "required".
- What happens when a visit is created with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that does not exist in the database? → Validation error "notFound" for lastName.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the update of an existing owner's details.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including name, birth date, and type.
- **FR-004**: System MUST allow the update of an existing pet's details.
- **FR-005**: System MUST validate owner information before saving (address, city, telephone, first name, last name).
- **FR-006**: System MUST validate pet information before saving (name, type).
- **FR-007**: System MUST display a form for creating or updating owner details.
- **FR-008**: System MUST display a form for creating or updating pet details.
- **FR-009**: System MUST populate a dropdown list with available pet types when creating or updating a pet.
- **FR-010**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-011**: System MUST allow searching for owners by last name prefix.
- **FR-012**: System MUST display a list of owners matching the last name search criteria.
- **FR-013**: System MUST handle cases where no owners match the search criteria.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details like name, address, city, and telephone. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, and type. A pet belongs to one owner and has one type.
- **PetType**: Represents the classification of a pet (e.g., Dog, Cat).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an owner's record with unique names in under 45 seconds.
- **SC-004**: 95% of users can successfully add or update owner and pet information without encountering validation errors on the first attempt.
- **SC-005**: The system prevents duplicate pet names for the same owner, with immediate feedback to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet attributes respectively.
- Data validation messages will be user-friendly and informative.
- The list of pet types is pre-defined and managed elsewhere.
- The system will use standard web form submission and redirection patterns.
- Error handling for non-existent IDs will result in appropriate exceptions being thrown and handled by the framework.