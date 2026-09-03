# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by providing a prefix of their last name. The system should then display a list of all owners whose last names match the provided prefix.

**Why this priority**: This is a core functionality for navigating and managing owners within the pet clinic system, enabling quick access to specific owner information.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name prefix, and verifying the displayed results match the expected owners. Delivers the value of quickly locating specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with last names like "Smith", "Smythe", "Jones", "Davis", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** a list of owners exists, **When** a user searches for an owner last name prefix that does not match any existing owners, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Users should be able to create a new owner by filling out a form with their details (first name, last name, address, city, telephone). Upon successful submission of a valid form, the new owner should be created and the user redirected to the owner's list page.

**Why this priority**: This is a fundamental operation for adding new clients to the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting, and verifying the owner appears in the owner list. Delivers the value of onboarding new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they fill in all required fields with valid data and click "Save", **Then** the new owner is created and the user is redirected to the owner list page, displaying the newly added owner.
2. **Given** a user is on the "Add Owner" page, **When** they leave a required field blank (e.g., last name) and click "Save", **Then** an error message is displayed for the blank field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Users should be able to view the complete details of an existing owner. This includes their first name, last name, address, city, telephone, and a list of their associated pets.

**Why this priority**: Essential for accessing and reviewing all information related to a specific client and their pets.

**Independent Test**: Can be fully tested by finding an owner (e.g., via search) and navigating to their detail page, then verifying all displayed information is correct. Delivers the value of providing a comprehensive view of a client.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with a specific address and telephone number, and has pets "Buddy" and "Lucy", **When** the user navigates to John Doe's owner details page, **Then** the page displays "John Doe", their address, telephone, and a list of their pets: "Buddy" and "Lucy".

---

### User Story 4 - Update Owner Details (Priority: P2)

Users should be able to edit the details of an existing owner. This includes modifying their first name, last name, address, city, and telephone number.

**Why this priority**: Allows for maintaining accurate and up-to-date client information.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit page, making a change (e.g., updating the phone number), saving, and then verifying the updated information on the owner's detail page. Delivers the value of keeping client records current.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists with phone number "1234567890", **When** the user navigates to Jane Smith's edit page, changes the phone number to "0987654321", and clicks "Save", **Then** the owner's detail page shows the updated phone number "0987654321".

---

### User Story 5 - Add a New Pet for an Existing Owner (Priority: P1)

Users should be able to add a new pet to an existing owner's record. This involves providing the pet's name, birth date, and selecting its type from a predefined list.

**Why this priority**: Core functionality for managing a client's pets within the system.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with valid details, and verifying the pet appears in the owner's pet list. Delivers the value of associating new pets with owners.

**Acceptance Scenarios**:

1. **Given** an owner "Alice Wonderland" exists, **When** the user navigates to add a pet for Alice, provides the pet name "Cheshire Cat", birth date "2023-05-10", and selects "Cat" as the type, **Then** the pet "Cheshire Cat" is successfully added to Alice Wonderland's record.

---

### User Story 6 - Update an Existing Pet's Information (Priority: P2)

Users should be able to modify the details of an existing pet, including its name, birth date, and type.

**Why this priority**: Allows for correcting or updating pet information as needed.

**Independent Test**: Can be fully tested by selecting a pet belonging to an owner, navigating to its edit page, making a change (e.g., updating the birth date), saving, and verifying the updated information. Delivers the value of maintaining accurate pet records.

**Acceptance Scenarios**:

1. **Given** a pet "Buddy" owned by "John Doe" has a birth date of "2020-01-15", **When** the user navigates to edit Buddy, changes the birth date to "2020-02-20", and saves, **Then** Buddy's detail page shows the updated birth date "2020-02-20".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation with a missing pet type → validation error "required".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date not in the expected format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Blank Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not after the current date → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for the specified owner → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's information.
- **FR-003**: System SHOULD validate pet data before saving.
- **FR-004**: System SHOULD provide a list of available pet types for selection during pet creation or update.
- **FR-005**: System SHOULD handle potential data integrity violations when saving pet information.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow updating an existing owner's information.
- **FR-008**: System MUST allow searching for owners by last name prefix.
- **FR-009**: System MUST display a list of owners matching a search prefix.
- **FR-010**: System MUST display detailed information for a selected owner.
- **FR-011**: System MUST validate owner data before saving.
- **FR-012**: System MUST validate pet data before saving.
- **FR-013**: System MUST provide a list of available pet types for selection during pet creation or update.
- **FR-014**: System MUST handle potential data integrity violations when saving owner information.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet. Key attributes include name, birth date, and pet type. A pet belongs to one owner and has a type.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Key attribute is the name of the type.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include the date of the visit. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be created and displayed in the owner list within 5 seconds of form submission.
- **SC-003**: Owner and pet details can be updated and reflected on the respective detail pages within 3 seconds.
- **SC-004**: 95% of users can successfully add a new pet to an owner's record without encountering validation errors, assuming valid input.
- **SC-005**: The system supports up to 50 concurrent users performing owner and pet management operations without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing authentication and authorization mechanisms.
- Data validation messages will be user-friendly and localized.
- The list of pet types is managed separately and will be available for selection.
- The system will use standard date formats for input and display.
- The telephone number format `\d{10}` is sufficient for all required regions.
- Error handling for non-existent IDs will result in a user-friendly "not found" message or appropriate exception.
- The `spring-petclinic` application is already set up with a database (e.g., H2, PostgreSQL) and necessary JPA configurations.
- The `OwnerController`, `PetController`, and related services/repositories are the primary components responsible for implementing these features.