# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for managing pet clinic data, allowing staff to quickly locate specific owners.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list. Delivers the ability to find owners.

**Acceptance Scenarios**:

1. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** the system displays owners "Smith" and "Smythe".
2. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Jo", **Then** the system displays owner "Jones".
3. **Given** the system contains owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with a last name prefix that does not match any owners (e.g., "Xy"), **Then** the system displays a "no owners found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Essential for onboarding new clients and their pets into the clinic's system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying redirection and owner creation. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid first name, last name, address, city, and a 10-digit telephone number, **And** they click "Save", **Then** the owner is created, and the user is redirected to the owner's details page.
2. **Given** a user is on the "Add Owner" form, **When** they enter a blank address, **And** they click "Save", **Then** the system rejects the submission and displays a validation error for the address field.
3. **Given** a user is on the "Add Owner" form, **When** they enter a telephone number that is not 10 digits, **And** they click "Save", **Then** the system rejects the submission and displays a validation error for the telephone field.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists with existing pets, When a user attempts to add a new pet with a name that already exists for that owner, Then an error is displayed indicating the pet name is a duplicate.

**Why this priority**: Prevents data integrity issues and ensures clear feedback to the user.

**Independent Test**: Can be tested by adding a pet to an owner, then attempting to add another pet with the same name for that owner. Delivers data integrity for pet names.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with a pet named "Buddy", **When** a user attempts to add a new pet for "John Doe" with the name "Buddy", **And** they click "Save", **Then** the system rejects the submission and displays an error message stating "Pet name must be unique for this owner".
2. **Given** an owner "Jane Smith" exists with no pets, **When** a user adds a new pet named "Whiskers" for "Jane Smith", **And** they click "Save", **Then** the pet "Whiskers" is successfully added to "Jane Smith".
3. **Given** an owner "Jane Smith" exists with a pet named "Whiskers", **When** a user attempts to add another pet named "Whiskers" for "Jane Smith", **And** they click "Save", **Then** the system rejects the submission and displays an error message stating "Pet name must be unique for this owner".

---

### User Story 4 - Update an Existing Pet's Name (Priority: P2)

Given a pet exists for an owner, When a user updates the pet's name to a unique name, Then the pet's name is updated successfully.

**Why this priority**: Allows for correction of naming errors or changes in pet nomenclature.

**Independent Test**: Can be tested by selecting an existing pet, changing its name, and verifying the update. Delivers the ability to correct pet names.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user navigates to "Buddy's" details, changes the name to "Buddy Jr.", **And** clicks "Save", **Then** the pet's name is updated to "Buddy Jr.".
2. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user navigates to "Buddy's" details, changes the name to a blank string, **And** clicks "Save", **Then** the system rejects the submission and displays a validation error for the pet name.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → System rejects with validation error.
- What happens when an owner is created or updated with a blank city? → System rejects with validation error.
- What happens when an owner is created or updated with a telephone number not matching the 10-digit pattern? → System rejects with validation error.
- What happens when a pet is created or updated with a blank name? → System rejects with validation error.
- What happens when a pet is created or updated without selecting a pet type? → System rejects with validation error.
- What happens when a pet is created or updated without providing a birth date? → System rejects with validation error.
- What happens when a pet is created with a birth date in an incorrect format (e.g., "2015/02/12")? → System rejects with validation error.
- What happens when a visit is created with a date that is not in the future? → System rejects with validation error.
- What happens when operations are performed on a non-existent owner ID? → System throws an `IllegalArgumentException`.
- What happens when operations are performed on a non-existent pet ID for a given owner? → System throws an `IllegalArgumentException`.
- What happens when searching for an owner with a last name that does not exist in the database? → System displays a "not found" error message.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow fetching an owner by their last name.
- **FR-005**: System SHOULD allow fetching a specific owner and their pets.
- **FR-006**: System MUST enforce that an owner's address is not blank.
- **FR-007**: System MUST enforce that an owner's city is not blank.
- **FR-008**: System MUST enforce that an owner's telephone number is exactly 10 digits.
- **FR-009**: System MUST enforce that a pet's name is not blank.
- **FR-010**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-011**: System MUST enforce that a pet has a selected type.
- **FR-012**: System MUST enforce that a pet has a birth date.
- **FR-013**: System MUST enforce that a visit has a date in the future.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. A pet belongs to one owner and has one type.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Key attribute is the name of the type.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date. A visit is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Adding a new pet to an existing owner with valid data completes in under 1 minute.
- **SC-004**: 95% of users successfully add or update owner/pet information without encountering validation errors for valid data.
- **SC-005**: The system correctly identifies and prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The primary users of this feature are clinic staff.
- Data validation messages will be user-friendly and informative.
- The system will use a relational database for data persistence.
- The date format for pet birth dates and visit dates will be `yyyy-MM-dd`.
- The telephone number format is strictly 10 digits.