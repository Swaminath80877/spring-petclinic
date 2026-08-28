# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-08-28

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find their contact information and pet details.

**Why this priority**: This is a core functionality for managing the clinic's client base and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search bar and verifying the displayed list of owners. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists in the system, **When** a user searches for owners by the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** a list of owners exists in the system, **When** a user searches for an owner last name that does not exist, **Then** an empty list or a "no results found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to create a new owner profile so that I can register myself and my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients to the clinic.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, and submitting. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled correctly, **Then** the owner is created and the user is redirected to the owner's list page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., last name), **Then** a validation error message is displayed for the blank field, and the owner is not created.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As an existing owner, I want to add a new pet to my profile so that I can keep my pet records up-to-date.

**Why this priority**: Allows owners to manage their pets as they acquire new ones.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling in valid pet details, and submitting. Delivers the ability to associate new pets with an owner.

**Acceptance Scenarios**:

1. **Given** an owner exists with existing pets, **When** the owner adds a new pet with a unique name and valid details, **Then** the new pet is successfully associated with the owner's profile.
2. **Given** an owner exists with existing pets, **When** the owner attempts to add a new pet with a name that already exists for that owner, **Then** an error is displayed indicating the pet name is a duplicate, and the pet is not added.

---

### User Story 4 - Update Existing Pet Information (Priority: P2)

As an owner, I want to update my pet's information (e.g., birth date, type) so that my records are accurate.

**Why this priority**: Ensures pet information remains current and accurate.

**Independent Test**: Can be fully tested by selecting an owner, selecting one of their pets, editing its details, and saving. Delivers the ability to correct or update pet data.

**Acceptance Scenarios**:

1. **Given** an owner has an existing pet, **When** the owner updates the pet's birth date and saves, **Then** the pet's birth date is updated in the system.
2. **Given** an owner has an existing pet, **When** the owner attempts to update the pet's name to a name that already exists for another pet owned by them, **Then** a validation error is displayed, and the update fails.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or find an owner with an ID that does not exist in the database → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating the name is already in use.
- **Invalid Visit Date**: Visit creation/update with a date that is not in the future → validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow the updating of existing pet information (name, birth date, type).
- **FR-006**: System SHOULD validate owner data upon creation or update, enforcing non-blank fields for address and city, and a 10-digit format for telephone.
- **FR-007**: System SHOULD validate pet data upon creation or update, enforcing non-blank names and valid birth dates.
- **FR-008**: System SHOULD display a form for creating or updating owner details.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD retrieve a list of available pet types for selection when adding or updating a pet.
- **FR-011**: System MUST prevent the creation of a pet with a name that already exists for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes fields for first name, last name, address, city, and telephone number. Has a relationship with multiple Pets.
- **Pet**: Represents a pet. Includes fields for name, birth date, and PetType. Has a relationship with an Owner and multiple Visits.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Includes a name.
- **Visit**: Represents a visit to the clinic. Includes a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and redirection to the owner list completes within 3 seconds.
- **SC-003**: 95% of users can successfully add a new pet to an existing owner without encountering validation errors on the first attempt.
- **SC-004**: System prevents duplicate pet names for the same owner, providing immediate feedback to the user.
- **SC-005**: All required fields for owner and pet creation/update are clearly indicated, and validation errors are user-friendly and actionable.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the provided context).
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics unless otherwise specified.
- The primary language for user interaction will be English.
- The system will be accessed via a web browser.