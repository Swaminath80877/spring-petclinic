# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-08

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a user is on the find owners page, When they enter a last name and submit the form, Then a list of owners whose last name starts with the entered value is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic application usability.

**Independent Test**: Can be fully tested by navigating to the find owners page, entering a known last name, and verifying the correct owner(s) are displayed. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** the user is on the "Find Owners" page, **When** they enter "Davis" into the "Last name" field and click "Search", **Then** a list of owners with the last name "Davis" is displayed.
2. **Given** the user is on the "Find Owners" page, **When** they enter "Smith" into the "Last name" field and click "Search", **Then** a message indicating "No owners found" is displayed if no owner has the last name "Smith".

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is a fundamental operation for adding new customers to the system, crucial for business growth and data management.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting, and verifying redirection to the newly created owner's details page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they enter valid details for "John" "Doe", address "123 Main St", city "Anytown", telephone "1234567890", and click "Add Owner", **Then** the owner "John Doe" is created and the user is redirected to their details page.
2. **Given** the user is on the "New Owner" form, **When** they attempt to submit with a blank "Address" field and click "Add Owner", **Then** a validation error message for the address is displayed, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and initiates adding a new pet, Then they can provide pet details (name, birth date, type) and save the new pet.

**Why this priority**: Managing pets is a core aspect of the pet clinic's service, and adding new pets is a frequent operation.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet management section, adding a new pet with valid details, and verifying the pet appears in the owner's pet list. Delivers the ability to record new animal patients.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details page, clicks "Add New Pet", enters "Buddy" as the name, selects "Dog" as the type, and provides a birth date, **Then** the pet "Buddy" is successfully added to Jane Smith's record.
2. **Given** owner "Jane Smith" exists, **When** the user attempts to add a pet with the name "Buddy" (which already exists for Jane Smith) and clicks "Add Pet", **Then** a validation error message indicating a duplicate pet name is displayed, and the pet is not added.

---

### User Story 4 - Update an Existing Pet's Details (Priority: P2)

Given an owner has existing pets, When a user navigates to an owner's details page and selects a pet to edit, Then they can modify the pet's details (name, birth date, type) and save the changes.

**Why this priority**: Allows for correction of errors or updating information about existing pets.

**Independent Test**: Can be fully tested by selecting an owner, choosing one of their pets, modifying a detail (e.g., changing the pet's name), saving, and verifying the change on the owner's details page. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" has a pet named "Buddy", **When** the user navigates to Jane Smith's details page, selects "Buddy" for editing, changes the name to "Buddy Jr.", and clicks "Update Pet", **Then** the pet's name is updated to "Buddy Jr." on Jane Smith's details page.
2. **Given** owner "Jane Smith" has a pet named "Buddy", **When** the user navigates to Jane Smith's details page, selects "Buddy" for editing, and attempts to change the pet type to a blank selection, **Then** a validation error for the pet type is displayed, and the changes are not saved.

---

### User Story 5 - Handle Invalid Owner Telephone Format (Priority: P3)

Given a user is creating or updating an owner, When they enter a telephone number that is not exactly 10 digits, Then a validation error message is displayed, and the owner is not saved.

**Why this priority**: Ensures data integrity for a critical contact field.

**Independent Test**: Can be fully tested by attempting to create or update an owner with an invalid telephone number (e.g., 9 digits or 11 digits) and verifying the error message. Delivers adherence to data format standards.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they enter "12345" as the telephone number and click "Add Owner", **Then** a validation error message "Telephone must be exactly 10 digits" is displayed.
2. **Given** the user is on the "Edit Owner" form for an existing owner, **When** they change the telephone number to "12345678901" and click "Update Owner", **Then** a validation error message "Telephone must be exactly 10 digits" is displayed.

---

### User Story 6 - Handle Invalid Visit Date (Priority: P3)

Given a user is adding a visit for a pet, When they enter a visit date that is not in the future, Then a validation error message is displayed, and the visit is not saved.

**Why this priority**: Ensures that visit dates are recorded chronologically and logically.

**Independent Test**: Can be fully tested by attempting to add a visit with a past date and verifying the error message. Delivers accurate temporal data for visits.

**Acceptance Scenarios**:

1. **Given** owner "John Doe" has a pet "Max", **When** the user navigates to Max's details, clicks "Add Visit", and enters "2023-01-01" as the date, **Then** a validation error message "Visit date must be in the future" is displayed.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → system rejects with validation error.
- **Blank City**: Owner creation/update with a blank city → system rejects with validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → system rejects with validation error.
- **Blank Pet Name**: Pet creation/update with a blank name → system rejects with validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → system rejects with validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → system rejects with validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to create a pet with a name that already exists for the same owner → system rejects with validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → system rejects with validation error.
- **Non-existent Owner**: Operations (e.g., adding a pet or visit) attempted for an owner ID that does not exist → system throws `IllegalArgumentException`.
- **Non-existent Pet**: Operations (e.g., adding a visit) attempted for a pet ID that does not exist for a given owner → system throws `IllegalArgumentException`.
- **Owner Not Found during Find**: Searching for owners with a last name that does not exist in the database → system displays a "not found" error message.
- **Exception Trigger**: Accessing the `/oups` endpoint → system throws a `RuntimeException` and displays an error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's details.
- **FR-003**: System SHOULD validate pet information (name, birth date, type) before saving.
- **FR-004**: System SHOULD display a form to create or update pet details, including a dropdown for pet types.
- **FR-005**: System MUST allow finding owners by their last name.
- **FR-006**: System MUST allow the creation of a new owner with valid details (first name, last name, address, city, telephone).
- **FR-007**: System MUST validate owner details upon creation or update, enforcing non-blank fields for address and city, and a 10-digit format for telephone.
- **FR-008**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-009**: System MUST allow the creation of a new visit for an existing pet, requiring a future date and a description.
- **FR-010**: System MUST validate visit dates to ensure they are in the future.
- **FR-011**: System MUST display appropriate error messages for invalid input during owner, pet, and visit operations.
- **FR-012**: System MUST handle operations on non-existent owners or pets by throwing an `IllegalArgumentException`.
- **FR-013**: System MUST display a "not found" message when searching for owners with a non-existent last name.
- **FR-014**: System MUST trigger a `RuntimeException` and display an error page when the `/oups` endpoint is accessed.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an individual animal belonging to an owner. Attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a single visit to the clinic for a pet. Attributes include date and description. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and redirection to details page completes within 5 seconds.
- **SC-003**: Adding a new pet to an owner's record is completed and displayed within 4 seconds.
- **SC-004**: Updating an existing pet's details is reflected on the owner's page within 4 seconds.
- **SC-005**: Validation errors for owner, pet, and visit data are displayed to the user immediately upon form submission failure.
- **SC-006**: The system successfully handles 100% of valid owner, pet, and visit creation/update operations.
- **SC-007**: The system correctly displays "No owners found" for 100% of searches yielding no results.

## Assumptions

- Users have stable internet connectivity.
- The application is accessed via a web browser.
- Standard date formats are acceptable for user input, with the system handling parsing.
- The system will be deployed in an environment where database persistence is available.
- The primary users are clinic staff responsible for managing owner and pet information.
- The `/oups` endpoint is intended for testing error handling and is not a user-facing feature.
- The `spring-petclinic` project structure and existing modules (Model, Persistence, Validation, Spring MVC, Spring Core, Spring Data, Java Time) will be utilized.
- The `Person` and `NamedEntity` base classes from the `model` module will be extended for relevant entities.
- Default error handling mechanisms provided by Spring Boot will be leveraged.