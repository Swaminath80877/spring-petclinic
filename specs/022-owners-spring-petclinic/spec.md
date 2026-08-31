# Feature Specification: Owner Management

**Feature Branch**: `022-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by providing a partial or full last name. The system should then display a list of all owners whose last names match the provided search term.

**Why this priority**: This is a core functionality for navigating and managing owners within the pet clinic system, enabling quick access to specific owner records.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name prefix, and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with various last names, **When** a user searches for "Smith", **Then** all owners with the last name "Smith" are displayed.
2. **Given** a list of owners exists, **When** a user searches for "Sm", **Then** all owners whose last names start with "Sm" (e.g., Smith, Smothers) are displayed.
3. **Given** no owners match the search term, **When** a user searches for "XYZ", **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Users should be able to add new owners to the system by filling out a form with their details. Upon successful submission of a valid form, the new owner should be created and the user should be redirected to the owner's detail page.

**Why this priority**: This is essential for onboarding new clients and expanding the pet clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, submitting the form, and verifying the owner's details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they enter valid first name, last name, address, city, and a 10-digit telephone number, and submit the form, **Then** the owner is created and the owner's details page is displayed.
2. **Given** a user is on the new owner form, **When** they leave the first name blank and submit the form, **Then** a validation error message for the first name is displayed, and the form is not submitted.
3. **Given** a user is on the new owner form, **When** they enter an invalid telephone number (e.g., 9 digits) and submit the form, **Then** a validation error message for the telephone number is displayed, and the form is not submitted.

---

### User Story 3 - View Owner List (Priority: P2)

Users should be able to view a comprehensive list of all registered owners. This list should provide a quick overview of the clinic's clientele.

**Why this priority**: Provides a central point for viewing all clients, aiding in administrative tasks and quick lookups.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that a list of owners is displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owners list page, **Then** a list displaying the names and potentially other key details of all owners is shown.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P2)

Users should be able to add a new pet to an existing owner's record. This involves selecting the owner and then providing the pet's details.

**Why this priority**: Essential for managing the core entities of the system – pets – and associating them with their owners.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their pet management section, and successfully adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an existing owner exists, **When** a user navigates to the owner's details page and initiates adding a new pet, **Then** they can enter the pet's name, select a pet type, and provide a birth date, and the pet is successfully associated with the owner.
2. **Given** an existing owner exists, **When** a user attempts to add a pet with a blank name, **Then** a validation error is displayed, and the pet is not added.
3. **Given** an existing owner exists, **When** a user attempts to add a pet without selecting a pet type, **Then** a validation error is displayed, and the pet is not added.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P3)

Users should be able to modify the details of an existing pet associated with an owner.

**Why this priority**: Allows for correction of errors or updating information as it changes over time.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, modifying a detail (e.g., name), and verifying the change is saved.

**Acceptance Scenarios**:

1. **Given** an owner has an existing pet, **When** a user navigates to the pet's details and updates its name, **Then** the pet's name is successfully updated.
2. **Given** an owner has an existing pet, **When** a user navigates to the pet's details and attempts to change its type to a non-existent type, **Then** an error is displayed, and the type is not changed.

---

### Edge Cases

- **Blank First Name**: Owner creation or update with a blank first name → validation error.
- **Blank Last Name**: Owner creation or update with a blank last name → validation error.
- **Blank Address**: Owner creation or update with a blank address → validation error.
- **Blank City**: Owner creation or update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation or update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner**: Attempting to find or edit an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation or update with a blank name → validation error.
- **Missing Pet Type**: Pet creation or update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation or update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating the name is already in use.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST validate that the owner's first name, last name, address, and city are not blank.
- **FR-003**: System MUST validate that the owner's telephone number consists of exactly 10 digits.
- **FR-004**: System MUST allow searching for owners by their last name.
- **FR-005**: System MUST display a list of owners matching the search criteria.
- **FR-006**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-007**: System MUST validate that the pet's name is not blank.
- **FR-008**: System MUST allow selection of a pet type from a predefined list when creating or updating a pet.
- **FR-009**: System MUST validate that a pet type is selected.
- **FR-010**: System MUST allow the update of an existing pet's details, including name, birth date, and type.
- **FR-011**: System SHOULD handle cases where an owner is not found when attempting to add a pet.
- **FR-012**: System MUST prevent adding a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, containing personal details like name, address, and contact information. It can have multiple associated pets.
- **Pet**: Represents an animal owned by an owner. It has a name, birth date, and type. A pet belongs to one owner and has one pet type.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). It has a name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation form submission and redirection to the owner's details page completes in under 5 seconds.
- **SC-003**: 95% of users can successfully add a new pet to an owner's record on their first attempt.
- **SC-004**: Validation errors for owner and pet creation/update are displayed to the user immediately upon submission failure.
- **SC-005**: The system supports displaying a list of up to 100 owners without significant performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `spring-core` and `spring-data-jpa` dependencies for data handling and validation.
- The list of pet types is predefined and managed separately.
- Error messages for validation will be user-friendly and informative.
- The system will handle cases where an owner ID is provided but no corresponding owner exists by displaying an appropriate error message.