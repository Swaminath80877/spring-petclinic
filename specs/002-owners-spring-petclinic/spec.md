# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-15

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owner data and is frequently used by staff.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a known last name, and verifying the correct owner is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the owner "Franklin" is displayed.
2. **Given** multiple owners with the last name "Smith" exist, **When** a user searches for owners with the last name "Smith", **Then** all owners with the last name "Smith" are displayed.
3. **Given** no owners with the last name "XYZ" exist, **When** a user searches for owners with the last name "XYZ", **Then** a "not found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record so that I can register new clients.

**Why this priority**: Essential for onboarding new customers into the system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting, and verifying the owner is created and their details page is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit a valid owner form with optional fields filled, **Then** the owner is created and redirected to the owner's details page.

---

### User Story 3 - Handle Owner Creation Errors (Priority: P2)

As a clinic staff member, I want to receive clear feedback when submitting an invalid owner form so that I can correct the errors and resubmit.

**Why this priority**: Improves user experience and data integrity by guiding users to correct input.

**Independent Test**: Can be fully tested by navigating to the new owner form, submitting with invalid data (e.g., blank required fields), and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit an invalid owner form (e.g., blank first name), **Then** an error message indicating the specific field error is displayed, and the user remains on the creation form.
2. **Given** a user is on the new owner form, **When** they submit an owner with an invalid telephone format, **Then** a validation error message for the telephone field is displayed.

---

### User Story 4 - Update an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to update an existing owner's information so that I can keep their records accurate.

**Why this priority**: Ensures data accuracy and allows for modifications to owner details.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their edit page, modifying a field, saving, and verifying the changes are reflected.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the owner's edit page and updates their address, **Then** the address is successfully updated.
2. **Given** an existing owner, **When** the user navigates to the owner's edit page and updates their telephone number, **Then** the telephone number is successfully updated.

---

### User Story 5 - Add a Pet to an Owner (Priority: P1)

As a clinic staff member, I want to be able to add a new pet to an existing owner's record so that I can manage their animals' information.

**Why this priority**: Core functionality for managing pet-related data associated with owners.

**Independent Test**: Can be fully tested by finding an owner, navigating to their pet management section, adding a new pet with valid details, and verifying the pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user adds a new pet with a valid name and type, **Then** the pet is successfully associated with the owner.
2. **Given** an existing owner, **When** the user attempts to add a pet with a duplicate name for that owner, **Then** a validation error is displayed.

---

### User Story 6 - Update a Pet's Information (Priority: P2)

As a clinic staff member, I want to be able to update a pet's information so that I can keep their details current.

**Why this priority**: Allows for accurate tracking of pet details over time.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, navigating to the pet's edit page, changing a field (e.g., birth date), saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** an existing pet belonging to an owner, **When** the user updates the pet's birth date, **Then** the birth date is successfully updated.
2. **Given** an existing pet belonging to an owner, **When** the user updates the pet's type, **Then** the pet's type is successfully updated.

---

### User Story 7 - Add a Visit for a Pet (Priority: P1)

As a clinic staff member, I want to be able to add a visit record for a pet so that I can track their medical history.

**Why this priority**: Essential for maintaining a complete medical record for each pet.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, navigating to add a visit, entering valid visit details, and verifying the visit is recorded for the pet.

**Acceptance Scenarios**:

1. **Given** an existing pet, **When** the user adds a new visit with a valid date and description, **Then** the visit is successfully recorded for the pet.
2. **Given** an existing pet, **When** the user attempts to add a visit with a date in the past, **Then** a validation error is displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error.
- What happens when a pet is created or updated without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when submitting a visit with a date that is not after the current date? → Validation error.
- What happens when attempting to add a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for a pet ID that does not exist for the specified owner? → `IllegalArgumentException` is thrown.
- What happens when attempting to edit an owner without providing an owner ID? → `IllegalArgumentException` is thrown.
- What happens when performing a find owners request with an empty last name? → Returns all owners.
- What happens when performing a find owners request where no owners match the provided last name? → Displays a "not found" error message.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD display a form for creating or updating a pet.
- **FR-005**: System SHOULD allow fetching an owner by their last name.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's information.
- **FR-008**: System MUST validate owner information during creation or update, including first name, last name, address, city, and telephone number.
- **FR-009**: System MUST allow adding a visit for an existing pet.
- **FR-010**: System MUST validate visit information during creation, including date and description.
- **FR-011**: System MUST disallow the 'id' field and any nested 'id' fields when creating or updating an owner.
- **FR-012**: System MUST disallow the 'id' field and any nested 'id' fields when creating or updating a visit.
- **FR-013**: System MUST ensure a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (first name, last name, address, city, telephone) and a list of associated pets.
- **Pet**: Represents an animal owned by an owner, including its name, birth date, type, and a list of associated visits.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a medical visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation process takes less than 1 minute for valid data entry.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: System successfully prevents duplicate pet names for the same owner.
- **SC-005**: Visit creation for a pet is completed within 30 seconds.
- **SC-006**: Validation errors for owner and pet forms are displayed to the user within 1 second of submission.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this owner management feature.
- The primary users of this feature are clinic staff members.
- Data persistence is handled by an underlying data store, and the focus here is on the application logic and user interface.
- The `Person` entity, which `Owner` inherits from, has `firstName` and `lastName` fields.
- The `NamedEntity` entity, which `Pet` and `PetType` inherit from, has a `name` field.
- The `Visit` entity has a `date` field.
- The `PetType` entity is pre-populated with common pet types.
- The `LocalDate` type is used for date fields.
- The `List<Pet>` and `Set<Visit>` are managed correctly by the persistence layer.
- The `\\d{10}` pattern for telephone numbers is sufficient for the project's needs.
- The `spring-petclinic` project structure and conventions will be followed.
- The `I18nPropertiesSyncTest` will be used to ensure all user-facing strings are internationalized.
- All new features and bug fixes will include comprehensive unit and integration tests.
- The domain model entities (`Owner`, `Pet`, `PetType`, `Visit`) will remain free from presentation or persistence concerns, with JPA annotations acceptable for mapping.
- The project utilizes Spring Boot, Spring Data JPA, Thymeleaf, and JUnit 5.
- All user-facing strings will be internationalized using Spring's message source mechanism.
- All code changes will comply with the Spring Petclinic Constitution.