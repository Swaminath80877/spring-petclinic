# Feature Specification: Owner Management

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owners and is frequently used by staff.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with last names "Smith", "Johnson", and "Smythe", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** a list of owners exists, **When** a user searches for a last name prefix that matches no owners, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to create a new owner record so that I can register new clients.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and submitting it, verifying that the owner is created and appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and the user is redirected to the owner's list page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., first name), **Then** a validation error message is displayed for that field, and the form is re-rendered with the entered data preserved.

---

### User Story 3 - Add a New Pet to an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: Important for maintaining a complete record of an owner's pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling it with valid pet details, and submitting, verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** a user adds a new pet with a unique name and valid details, **Then** the pet is successfully added to the owner's record.
2. **Given** an owner exists, **When** a user attempts to add a new pet with a name that already exists for that owner, **Then** an error message indicating a duplicate name is displayed, and the form is re-rendered.

---

### User Story 4 - Update an Existing Pet's Information (Priority: P2)

As a clinic staff member, I want to update an existing pet's information so that I can keep their records accurate.

**Why this priority**: Ensures that pet details are current and correct.

**Independent Test**: Can be fully tested by selecting a pet, editing its details (e.g., birth date, type), and saving the changes, verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a user updates the pet's birth date and saves, **Then** the pet's birth date is updated in the system.
2. **Given** a pet exists for an owner, **When** a user attempts to update the pet's name to a name that already exists for another pet of the same owner, **Then** a validation error message is displayed, and the form is re-rendered.

---

### User Story 5 - Create a Visit for a Pet (Priority: P3)

As a clinic staff member, I want to create a visit record for a pet so that I can track their appointments and treatments.

**Why this priority**: Crucial for maintaining a history of a pet's health and care.

**Independent Test**: Can be fully tested by selecting a pet, navigating to the add visit form, filling it with valid visit details, and submitting, verifying the visit is associated with the pet.

**Acceptance Scenarios**:

1. **Given** a pet exists, **When** a user creates a new visit with a valid date and description, **Then** the visit is successfully recorded for the pet.
2. **Given** a pet exists, **When** a user attempts to create a visit with an invalid date format, **Then** a validation error message is displayed, and the form is re-rendered.

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
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date that does not match the expected format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Blank Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Invalid Visit Date**: Visit creation/update with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Owner for Visit**: Attempting to create a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet for Visit**: Attempting to create a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **No Owners Found**: Searching for owners with a last name that does not match any records → validation error "notFound" on the lastName field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the updating of an existing owner's information (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST allow the creation of a new pet for an owner.
- **FR-005**: System MUST allow the updating of an existing pet's information (birth date, type).
- **FR-006**: System MUST allow the creation of a new visit for a pet.
- **FR-007**: System MUST validate owner information during creation or update (first name, last name, address, city, telephone).
- **FR-008**: System MUST validate pet information during creation or update (name, birth date, type).
- **FR-009**: System MUST validate visit information during creation or update (date, description).
- **FR-010**: System MUST display a list of available pet types when creating or updating a pet.
- **FR-011**: System MUST handle potential data integrity violations when saving owner or pet data, such as duplicate pet names for the same owner.
- **FR-012**: System MUST display appropriate error messages for validation failures.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact details and a list of their pets. Attributes include first name, last name, address, city, and telephone number.
- **Pet**: Represents an animal owned by a client. Attributes include name, birth date, and type. It is associated with an Owner and has a list of Visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a veterinary visit for a pet. Attributes include date and description. It is associated with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and redirection to the owner list completes in under 3 seconds.
- **SC-003**: Adding a new pet to an owner is completed and displayed within 3 seconds.
- **SC-004**: 95% of form submissions with valid data are processed successfully without errors.
- **SC-005**: Validation errors are displayed clearly and immediately upon form submission failure.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for data persistence.
- Standard web application conventions for form handling and navigation will be followed.
- The `spring-petclinic` project's existing structure and conventions will be adhered to.
- The `Person` entity from the `model` module is used as a base for `Owner`'s first and last name.
- The `NamedEntity` and `BaseEntity` from the `model` module are used for `PetType` and `Pet` respectively.
- The `LocalDate` type will be used for dates, with a specified format for user input.
- The telephone number validation will strictly enforce a 10-digit pattern.
- The system will provide user-friendly error messages for all validation failures.
- The `PetController` and `OwnerController` will handle the primary user interactions for managing owners and pets.
- The `VisitController` will handle the creation of visits for pets.
- The `PetValidator` will be used for validating pet data.
- The `ClinicService` will be used for business logic operations related to owners and pets.
- The `OwnerRepository` and `PetTypeRepository` will be used for data access.
- The `VisitRepository` will be used for data access related to visits.
- The `DateTimeFormat` annotation will be used to specify the expected date format for user input.
- The `JoinColumn` and `OrderBy` annotations will be used for managing relationships between entities.
- The `CascadeType.ALL` and `FetchType.EAGER` will be used for pet and visit relationships to ensure data consistency and immediate loading.
- The `Pattern` annotation will be used for validating the telephone number format.
- The `@NotBlank` annotation will be used to ensure that certain fields are not empty.
- The `@Valid` annotation will be used to trigger validation of form data.
- The `@ModelAttribute` annotation will be used to bind form data to model objects.
- The `@PathVariable` annotation will be used to extract values from URI paths.
- The `@Autowired` annotation will be used for dependency injection.
- The `@Controller` annotation will be used to mark classes as controllers.
- The `@GetMapping` and `@PostMapping` annotations will be used to map HTTP requests to controller methods.
- The `@DateTimeFormat` annotation will be used to specify the expected date format for user input.
- The `@JoinColumn` and `@OrderBy` annotations will be used for managing relationships between entities.
- The `@NotBlank` annotation will be used to ensure that certain fields are not empty.
- The `@Pattern` annotation will be used for validating the telephone number format.
- The `@Valid` annotation will be used to trigger validation of form data.
- The `@ModelAttribute` annotation will be used to bind form data to model objects.
- The `@PathVariable` annotation will be used to extract values from URI paths.
- The `@Autowired` annotation will be used for dependency injection.
- The `@Controller` annotation will be used to mark classes as controllers.
- The `@GetMapping` and `@PostMapping` annotations will be used to map HTTP requests to controller methods.
- The `IllegalArgumentException` will be thrown for non-existent owner or pet IDs when creating visits.
- The `typeMismatch` validation error will be used for incorrect date formats.
- The `required` validation error will be used for blank pet names.
- The `duplicate` validation error will be used for duplicate pet names within the same owner.
- The `notFound` validation error will be used when no owners are found for a given last name search.