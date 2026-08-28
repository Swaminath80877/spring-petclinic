# Feature Specification: Owner Management

**Feature Branch**: `010-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by their last name. This is a primary function for navigating the application and finding specific owner records.

**Why this priority**: This is a core navigation and lookup feature, essential for daily use of the application.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the correct list of owners is displayed.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the last name search field and click "Search", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter a last name that does not exist in the system and click "Search", **Then** a "notFound" message is displayed on the last name field, and the user remains on the "Find Owners" page.

---

### User Story 2 - Create a New Owner (Priority: P1)

Users should be able to add new owners to the system through a dedicated form.

**Why this priority**: This is a fundamental data entry feature, enabling the growth of the owner database.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields with valid data, submitting the form, and verifying the new owner appears in the system and their details can be viewed.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is created, and the user is redirected to the owner's detail page.
2. **Given** the user is on the "Add Owner" page, **When** they leave the "First Name" field blank and click "Submit", **Then** a validation error message "required" is displayed for the "First Name" field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Users should be able to view the complete details of an existing owner, including their personal information and associated pets.

**Why this priority**: This allows users to access and review all information related to a specific owner.

**Independent Test**: Can be fully tested by finding an existing owner (via search or direct link) and verifying all their associated data is displayed correctly.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with associated pets, **When** the user navigates to John Doe's owner detail page, **Then** the owner's first name, last name, address, city, telephone, and a list of their pets (including pet names and types) are displayed.

---

### User Story 4 - Edit Owner Details (Priority: P2)

Users should be able to modify the information of an existing owner.

**Why this priority**: Allows for correction of errors or updating of owner information.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit page, making a change to a field, saving it, and verifying the change is reflected on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** the user is viewing the details of an owner, **When** they click the "Edit Owner" button, **Then** they are presented with a form pre-populated with the owner's current information.
2. **Given** the user is on the "Edit Owner" form, **When** they change the owner's telephone number and click "Submit", **Then** the owner's telephone number is updated, and the user is redirected to the owner's detail page showing the new telephone number.

---

### User Story 5 - Add a New Pet for an Owner (Priority: P3)

Users should be able to add a new pet to an existing owner's record.

**Why this priority**: Essential for managing an owner's pets within the system.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, initiating the "Add Pet" action, filling out the pet form with valid data, and verifying the new pet is listed under the owner.

**Acceptance Scenarios**:

1. **Given** the user is viewing an owner's details, **When** they click "Add New Pet", **Then** they are presented with a form to enter pet details (name, birth date, type).
2. **Given** the user is on the "Add Pet" form for an owner, **When** they enter a valid pet name, select a pet type, and enter a valid birth date, and click "Submit", **Then** the new pet is associated with the owner, and the owner's pet list is updated.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error on the "First Name" field.
- What happens when an owner is created or updated with a blank last name? → Validation error on the "Last Name" field.
- What happens when an owner is created or updated with a telephone number that is not exactly 10 digits? → Validation error on the "Telephone" field.
- What happens when an owner is created or updated with a blank address? → Validation error on the "Address" field.
- What happens when an owner is created or updated with a blank city? → Validation error on the "City" field.
- What happens when attempting to edit or view an owner with an ID that does not exist? → An `IllegalArgumentException` is thrown, and an appropriate error page is displayed.
- What happens when attempting to create or update a pet with a blank name? → Validation error on the "Name" field.
- What happens when attempting to create or update a pet without selecting a pet type? → Validation error on the "Type" field.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error on the "Name" field indicating a duplicate.
- What happens when attempting to create or update a pet with an invalid birth date format? → Validation error indicating a type mismatch for the birth date.
- What happens when attempting to book a visit with a blank date? → Validation error on the "Date" field.
- What happens when attempting to book a visit with a date that is in the past? → Validation error indicating the visit date must be in the future.
- What happens when attempting to book a visit for an owner ID that does not exist? → An `IllegalArgumentException` is thrown, and an appropriate error page is displayed.
- What happens when attempting to book a visit for a pet ID that does not exist for a given owner? → An `IllegalArgumentException` is thrown, and an appropriate error page is displayed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST display owner details, including their pets.
- **FR-004**: System MUST allow updating an existing owner's details.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and type.
- **FR-006**: System SHOULD validate pet information (name, birth date, type) before saving.
- **FR-007**: System SHOULD allow the retrieval of an owner by their last name.
- **FR-008**: System SHOULD allow updating a pet's name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type. A pet belongs to one owner and has one pet type.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog). Attributes include the name of the pet type.
- **Visit**: Represents a veterinary visit for a pet. Attributes include the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created successfully with all required fields in under 1 minute.
- **SC-003**: Owner details are displayed completely and accurately within 2 seconds of navigation.
- **SC-004**: 95% of users can successfully add a new pet to an owner's record on their first attempt.
- **SC-005**: Validation errors for owner and pet creation/updates are displayed clearly and immediately upon form submission.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date formats will be used for birth dates and visit dates.
- The system will use a relational database for data persistence.
- Existing authentication mechanisms (if any) will be leveraged for user access control, though this feature focuses on data management.
- The primary language for the application is English.