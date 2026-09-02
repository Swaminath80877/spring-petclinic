# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `012-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating and accessing owner information, essential for basic system usability.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's details.

**Acceptance Scenarios**:

1. **Given** the system has an owner with the last name "Franklin", **When** a user searches for owners using "Franklin" as the last name, **Then** the system displays the details page for the owner named "Franklin".
2. **Given** the system has multiple owners with the last name "Franklin", **When** a user searches for owners using "Franklin" as the last name, **Then** the system displays a list of owners with the last name "Franklin".

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Creating new owners is fundamental to populating the system with data and enabling other features.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the owner is created and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they enter valid data for first name, last name, address, city, and telephone, **Then** the owner is successfully created and the user is redirected to the owner's details page or a confirmation page.
2. **Given** a user is on the new owner form, **When** they enter valid data for all fields except telephone, **Then** the owner is successfully created and the user is redirected to the owner's details page or a confirmation page.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the form.

**Why this priority**: Ensures data integrity and provides user feedback for incorrect input.

**Independent Test**: Can be fully tested by navigating to the new owner form, entering invalid data in one or more fields, submitting the form, and verifying that error messages are displayed for the invalid fields and the form remains visible.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** an error message is displayed indicating the address cannot be blank, and the form is redisplayed.
2. **Given** a user is on the new owner form, **When** they submit the form with a telephone number that is not 10 digits, **Then** an error message is displayed indicating an invalid telephone number, and the form is redisplayed.
3. **Given** a user is on the new owner form, **When** they submit the form with a blank city, **Then** an error message is displayed indicating the city cannot be blank, and the form is redisplayed.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P1)

Given an existing owner, When a user navigates to the owner's details and chooses to add a pet, Then a form is presented to create a new pet.

**Why this priority**: Managing pets is a core aspect of the pet clinic functionality.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, and initiating the pet creation process.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user accesses the owner's details page and selects the option to add a pet, **Then** a form for creating a new pet is displayed, pre-populated with the owner's information.
2. **Given** the pet creation form is displayed, **When** the user selects a valid pet type from the dropdown, **Then** the selected pet type is associated with the new pet.

---

### User Story 5 - Update an Existing Pet's Details (Priority: P2)

Given an existing pet, When a user navigates to the pet's details and chooses to edit, Then a form is presented to update the pet's information.

**Why this priority**: Allows for correction of pet information and maintenance of accurate records.

**Independent Test**: Can be fully tested by selecting an existing pet, navigating to its details, and initiating the edit process.

**Acceptance Scenarios**:

1. **Given** an existing pet, **When** the user accesses the pet's details page and selects the option to edit the pet, **Then** a form for updating pet details is displayed, pre-populated with the pet's current information.
2. **Given** the pet update form is displayed, **When** the user modifies the pet's name and saves the changes, **Then** the pet's name is updated in the system.

---

### User Story 6 - Handle Invalid Pet Creation/Update (Priority: P2)

Given a user is on the pet creation or update form, When they submit invalid pet data, Then the system displays an error message and returns to the form.

**Why this priority**: Ensures data integrity for pet records.

**Independent Test**: Can be fully tested by attempting to create or update a pet with invalid data.

**Acceptance Scenarios**:

1. **Given** a user is on the pet creation form, **When** they submit the form with a blank pet name, **Then** an error message is displayed indicating the pet name cannot be blank, and the form is redisplayed.
2. **Given** a user is on the pet creation form, **When** they attempt to create a pet without selecting a pet type, **Then** an error message is displayed indicating a pet type must be selected, and the form is redisplayed.
3. **Given** a user is on the pet update form, **When** they attempt to change a pet's name to one that already exists for the same owner, **Then** an error message is displayed indicating the pet name is already in use, and the form is redisplayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error for address.
- What happens when an owner is created or updated with a blank city? → Validation error for city.
- What happens when an owner is created or updated with a telephone number that is not 10 digits? → Validation error for telephone.
- What happens when attempting to edit or access an owner with an ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created or updated with a blank name? → Validation error for name.
- What happens when a pet is created without selecting a pet type? → Validation error for type.
- What happens when attempting to create a pet with a name that already exists for the same owner? → Validation error indicating the name is already in use.
- What happens when a pet is created or updated with an invalid birth date format? → `typeMismatch` validation error for birthDate.
- What happens when a pet is created or updated with a null birth date? → Validation error for birthDate.
- What happens when searching for owners with a last name that does not match any existing owners? → Validation error `notFound` for lastName.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including name, birth date, and type.
- **FR-004**: System MUST allow the update of an existing pet's details, including name and birth date.
- **FR-005**: System SHOULD validate pet information during creation or update, including name and type.
- **FR-006**: System SHOULD display a form for creating or updating pet details.
- **FR-007**: System SHOULD populate a dropdown list with available pet types when creating or updating a pet.
- **FR-008**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-009**: System MUST display appropriate validation errors for invalid owner and pet data.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet. (Note: While present in the repository context, explicit requirements for Visit management are not detailed in the user description for this feature, so it's included as a related entity but not a primary focus of new requirements here).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find existing owners by last name in under 3 seconds.
- **SC-002**: New owners can be successfully created with valid data in under 1 minute.
- **SC-003**: New pets can be successfully added to an owner's record in under 1 minute.
- **SC-004**: 95% of invalid form submissions for owner or pet creation/update display clear, actionable error messages to the user.
- **SC-005**: The system correctly prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` and `NamedEntity` base classes for owner and pet attributes respectively.
- The system will use standard web form validation mechanisms.
- The list of available pet types will be managed and provided by the system.
- The primary focus of this feature is on owner and pet management; visit management is considered out of scope for this specific specification unless explicitly required.
- The existing `OwnerRepository` and `PetTypeRepository` will be utilized for data persistence and retrieval.