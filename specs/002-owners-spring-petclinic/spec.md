# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic administrator, I want to search for owners by their last name so that I can quickly access their details and manage their pets.

**Why this priority**: This is a core functionality for managing the clinic's customer base and is essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a known last name in the search form and verifying that the correct owner(s) are displayed and the detail page is accessible.

**Acceptance Scenarios**:

1. **Given** there are owners in the system, **When** a user searches for owners by a last name starting with "Franklin", **Then** the system should display a list of owners whose last names start with "Franklin" and redirect to the owner's detail page.
2. **Given** there are owners in the system, **When** a user searches for an owner by a last name with leading or trailing whitespace (e.g., " Franklin "), **Then** the system should treat the search as if the whitespace was not present and display the correct list of owners.
3. **Given** there are owners in the system, **When** a user searches for a last name that does not exist, **Then** the system should display a "No owners found" message and return to the find owners form.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic administrator, I want to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new customers and expanding the clinic's client base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details are displayed correctly.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner creation form, **When** they submit a valid owner form with all required fields populated, **Then** the owner is created, a success message is displayed, and the user is redirected to the owner's detail page.
2. **Given** a user is on the new owner creation form, **When** they submit the form with a blank first name, **Then** a validation error for the first name is displayed, and the form remains open.
3. **Given** a user is on the new owner creation form, **When** they submit the form with a blank last name, **Then** a validation error for the last name is displayed, and the form remains open.
4. **Given** a user is on the new owner creation form, **When** they submit the form with an invalid telephone format (not 10 digits), **Then** a validation error for the telephone number is displayed, and the form remains open.
5. **Given** a user is on the new owner creation form, **When** they submit the form with a blank address, **Then** a validation error for the address is displayed, and the form remains open.
6. **Given** a user is on the new owner creation form, **When** they submit the form with a blank city, **Then** a validation error for the city is displayed, and the form remains open.

---

### User Story 3 - View and Edit Owner Details (Priority: P2)

As a clinic administrator, I want to view and edit an existing owner's details so that I can update their contact information and manage their pets.

**Why this priority**: Allows for ongoing management of client information and ensures data accuracy.

**Independent Test**: Can be fully tested by selecting an existing owner, verifying their details are displayed, and then updating a field and confirming the change is saved.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** a user navigates to the owner's detail page, **Then** all of the owner's information (name, address, city, telephone, and pets) is displayed.
2. **Given** an owner's detail page is displayed, **When** a user clicks the "Edit Owner" button, **Then** the owner's information is presented in an editable form.
3. **Given** an owner's information is displayed in an editable form, **When** a user updates the telephone number and clicks "Save", **Then** the owner's telephone number is updated, and the updated details are displayed.
4. **Given** an owner's information is displayed in an editable form, **When** a user attempts to update the owner with a blank address, **Then** a validation error for the address is displayed, and the changes are not saved.
5. **Given** an owner's information is displayed in an editable form, **When** a user attempts to update the owner with a non-existent owner ID, **Then** an `IllegalArgumentException` indicating the owner was not found is thrown.

---

### User Story 4 - Manage Pets for an Owner (Priority: P2)

As a clinic administrator, I want to add, view, and edit pets associated with an owner so that I can maintain accurate records of their animals.

**Why this priority**: Crucial for providing veterinary care and tracking pet health history.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet, verifying its details, and then editing that pet's information.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** the owner's detail page is viewed, **Then** a list of their associated pets is displayed, including their name, birth date, and type.
2. **Given** an owner's detail page is displayed, **When** the user clicks the "Add New Pet" button, **Then** a form for adding a new pet is presented, including a dropdown for pet types.
3. **Given** the new pet form is displayed, **When** a user enters a valid pet name, birth date, and selects a pet type, **Then** the pet is created and associated with the owner, and the updated pet list is displayed.
4. **Given** the new pet form is displayed, **When** a user enters a blank pet name, **Then** a validation error for the pet name is displayed, and the form remains open.
5. **Given** the new pet form is displayed, **When** a user attempts to add a pet with a name that already exists for the same owner, **Then** a validation error for duplicate pet name is displayed, and the form remains open.
6. **Given** an existing pet's details are displayed, **When** the user clicks the "Edit Pet" button, **Then** the pet's information is presented in an editable form.
7. **Given** an existing pet's information is displayed in an editable form, **When** the user updates the pet's birth date to an invalid format and clicks "Save", **Then** a validation error for the birth date format is displayed, and the changes are not saved.

---

### User Story 5 - Manage Pet Types (Priority: P3)

As a clinic administrator, I want to manage the list of available pet types so that owners can accurately categorize their pets.

**Why this priority**: Ensures consistency in pet categorization and supports accurate reporting.

**Independent Test**: Can be tested by viewing the list of pet types and potentially adding a new one (if functionality exists).

**Acceptance Scenarios**:

1. **Given** the system is running, **When** a user views the pet creation or edit form, **Then** a dropdown list populated with available pet types (e.g., "cat", "dog") is displayed.
2. **Given** a user is managing pet types, **When** they submit a new pet type with a blank name, **Then** a validation error for the pet type name is displayed.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` indicating owner not found.
- **No Owners Found**: Searching for owners with a last name that yields no results → validation error "notFound" for the `lastName` field, returning the find owners form.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required" for the `name` field.
- **Missing Pet Type**: Creating a pet without specifying a pet type → validation error "required" for the `type` field.
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch" for the `birthDate` field.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate" for the `name` field.
- **Invalid Visit Date**: Booking a visit with a date that is not in the future (i.e., on or before the current date) → validation error "typeMismatch.visitDate" for the `date` field.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` indicating the pet was not found for the owner.
- **Unsynchronized Translation Files**: If translation files are not in sync, missing keys in locale-specific property files → test failure reporting missing keys.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name, supporting partial matches and ignoring leading/trailing whitespace.
- **FR-003**: System MUST display a list of owners matching the search criteria, redirecting to the owner's detail page upon selection.
- **FR-004**: System MUST display an error message if no owners are found for a given search.
- **FR-005**: System MUST allow viewing the details of an existing owner, including their associated pets.
- **FR-006**: System MUST allow editing of an existing owner's details.
- **FR-007**: System MUST validate owner information upon creation and update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-008**: System MUST allow the creation of a new pet for an existing owner, including pet name and birth date.
- **FR-009**: System MUST allow the update of an existing pet's details, including name and birth date.
- **FR-010**: System SHOULD validate pet information before saving, enforcing non-blank pet name and a valid birth date format.
- **FR-011**: System SHOULD populate a dropdown list with available pet types when creating or updating a pet.
- **FR-012**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-013**: System MUST prevent the creation or update of an owner or visit with disallowed 'id' fields.
- **FR-014**: System MUST display a list of pet types.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a list of their pets. Extends `Person`.
- **Pet**: Represents a pet belonging to an owner, including its birth date and a set of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created successfully in under 1 minute.
- **SC-003**: Pet details can be added or updated for an owner in under 45 seconds.
- **SC-004**: 95% of owner and pet data entry operations complete without validation errors when valid data is provided.
- **SC-005**: The system supports up to 500 concurrent users browsing owner information without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be used to secure access to owner management features.
- The list of pet types will be pre-populated or managed through a separate administrative interface.
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics.
- The `Person` class is available and provides basic name fields.
- The `NamedEntity` class is available and provides an `id` field.
- The `I18nPropertiesSyncTest` indicates that internationalization is a consideration, and user-facing strings should be externalized.