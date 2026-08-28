# Feature Specification: Owners for Spring PetClinic

**Feature Branch**: `015-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly find their records.

**Why this priority**: This is a core functionality for managing the clinic's client base and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the correct owner(s) are displayed. Delivers the ability to locate existing owner records.

**Acceptance Scenarios**:

1. **Given** I am on the "Find Owners" page, **When** I enter "Smith" into the "Last name" field and click "Search", **Then** I should see a list of all owners whose last name starts with "Smith".
2. **Given** I am on the "Find Owners" page, **When** I enter a last name that does not exist in the system and click "Search", **Then** I should see a message indicating that no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register myself and my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields, submitting the form, and verifying the new owner appears on the "Owners" list. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form, **When** I fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is created and I am redirected to the "Owners" list page, showing the newly added owner.
2. **Given** I am on the "Add Owner" form, **When** I leave a required field blank (e.g., "Last name") and click "Submit", **Then** I should see an error message indicating the field is required, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

As a clinic staff member, I want to view the details of a specific owner, including their pets, so that I can access all relevant information about them.

**Why this priority**: Essential for providing personalized service and understanding a client's history.

**Independent Test**: Can be fully tested by finding an existing owner and clicking on their name, then verifying all their details and associated pets are displayed. Delivers the ability to access comprehensive client information.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with pets "Buddy" and "Lucy", **When** I navigate to the "Owners" list and click on "John Doe", **Then** I should see John Doe's contact information (address, city, telephone) and a list of his pets, "Buddy" and "Lucy", with their respective details.

---

### User Story 4 - Add a New Pet to an Existing Owner (Priority: P2)

As a pet owner, I want to add a new pet to my existing owner profile so that I can register my new animal with the clinic.

**Why this priority**: Allows existing clients to easily add new pets without creating a whole new owner profile.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their pet list, clicking "Add Pet", filling in the new pet's details (name, birth date, type), and verifying the pet is added to the owner's profile. Delivers the ability to manage pets for an existing owner.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of an existing owner, **When** I click "Add Pet", fill in the required pet details (name, birth date, type) with valid data, and click "Submit", **Then** the new pet is associated with the owner and appears in their pet list.
2. **Given** I am viewing the details of an existing owner, **When** I attempt to add a pet with a name that already exists for this owner and click "Submit", **Then** I should see a validation error indicating that pet names must be unique for a given owner.

---

### User Story 5 - Update Pet Information (Priority: P3)

As a pet owner, I want to update the information for an existing pet so that I can keep their records accurate.

**Why this priority**: Ensures that pet details like birth dates or types can be corrected if entered incorrectly or changed.

**Independent Test**: Can be fully tested by finding an existing pet belonging to an owner, clicking to edit its details, making a change (e.g., birth date), saving, and verifying the update. Delivers the ability to correct pet information.

**Acceptance Scenarios**:

1. **Given** I am viewing the details of a pet, **When** I click "Edit Pet", change the pet's birth date to a valid new date, and click "Submit", **Then** the pet's birth date is updated in the system.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner is created or updated with a telephone number that is not exactly 10 digits? → Validation error.
- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created or updated with a blank name? → Validation error "required".
- What happens when a pet is created with a missing pet type? → Validation error "required".
- What happens when a pet is validated with a null birth date? → `PetValidator` flags a "required" error.
- What happens when a pet is updated with a birth date in "yyyy/MM/dd" format? → Validation error "typeMismatch".
- What happens when attempting to save a pet with a name that already exists for the same owner? → `ClinicServiceTests` indicates this scenario should fail.
- What happens when attempting to add a visit for a pet with an ID that does not exist for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when submitting a visit with a date that is not after the current date? → Validation error "typeMismatch.visitDate".
- What happens when searching for owners with a last name that yields no results? → System returns an error "notFound" for the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets associated with an owner.
- **FR-002**: System MUST allow the updating of existing pet information.
- **FR-003**: System SHOULD validate pet data upon creation or update.
- **FR-004**: System SHOULD display a list of pet types when creating or updating a pet.
- **FR-005**: System SHOULD handle cases where an owner is not found when attempting to add or update a pet.
- **FR-006**: System MUST allow owners to be searched by last name.
- **FR-007**: System MUST allow the creation of new owner profiles.
- **FR-008**: System MUST display owner details, including their associated pets.
- **FR-009**: System MUST validate owner data upon creation or update, including address, city, and telephone number format.
- **FR-010**: System MUST ensure pet names are unique for a given owner.
- **FR-011**: System MUST validate pet names, birth dates, and pet types upon creation or update.
- **FR-012**: System MUST prevent the creation of visits with dates in the past.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal information (address, city, telephone) and a collection of their pets.
- **Pet**: Represents an animal owned by a specific owner, including its name, birth date, and type. It is associated with an Owner and a PetType.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a clinic visit for a specific pet, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation form submission and success confirmation takes under 1 minute.
- **SC-003**: Owner details page loads completely within 2 seconds.
- **SC-004**: 95% of pet creation/update operations are successful on the first attempt with valid data.
- **SC-005**: Support tickets related to incorrect owner or pet information are reduced by 30% within one quarter of release.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing authentication and authorization mechanisms.
- Data for pet types (e.g., Cat, Dog) will be pre-populated or managed through a separate administrative interface.
- The primary data store is a relational database.
- The system will use standard web browser functionality for user interaction.
- Error messages will be user-friendly and informative.
- The system will adhere to the Spring PetClinic Constitution regarding architecture, testing, and development workflow.