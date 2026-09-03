# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST follow a strict top-down flow (Controller -> Service -> Repository -> Model). Direct dependencies between non-adjacent layers are PROHIBITED.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components in isolation, while integration tests MUST verify interactions between components and with external systems (e.g., database). A minimum of 80% code coverage MUST be maintained for all new code.

### III. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be POJOs with clear responsibilities. Persistence logic MUST be encapsulated within Repository interfaces. Domain entities MUST NOT contain direct database access or complex business logic that belongs in the Service layer.

### IV. Configuration Centralization
Application configuration, including internationalization (`WebConfiguration`) and caching (`CacheConfiguration`), MUST be managed through dedicated configuration classes. Externalized configuration properties MUST be used where appropriate, and hardcoded configuration values are PROHIBITED.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST provide mechanisms for monitoring its health and performance, particularly for database interactions and web requests.

## Development Workflow

The development workflow for Spring PetClinic follows a structured approach to ensure code quality, maintainability, and adherence to architectural principles.

### Code Review Process
All code changes submitted via Pull Requests (PRs) MUST undergo a thorough code review by at least one other team member. Reviewers MUST verify adherence to the project's core principles, coding standards, and test coverage requirements. PRs MUST not be merged until all review feedback is addressed and approved.

### Testing Strategy
*   **Unit Tests:** Focus on testing individual classes and methods in isolation, using mocking frameworks where necessary. These tests reside in `src/test/java/org/springframework/samples/petclinic/...` and typically end with `Tests.java`.
*   **Integration Tests:** Verify the interaction between multiple components and with external dependencies like the database. Examples include `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`, and `CrashControllerIntegrationTests.java`.
*   **Contract Tests:** Where applicable, contract tests should be implemented to ensure compatibility between different services or modules. (Note: This project currently focuses on a monolithic structure, but this principle is a forward-looking guideline).

### Database Interaction
The project utilizes Spring Data JPA for data access. Repository interfaces (`OwnerRepository`, `PetTypeRepository`, `VetRepository`) abstract database operations. Integration tests are provided for common database systems (MySQL, PostgreSQL) to ensure compatibility.

## Governance

This constitution serves as the guiding document for the development and maintenance of the Spring PetClinic repository.

### Amendment Process
Any proposed amendments to this constitution MUST be submitted as a formal proposal, clearly outlining the rationale for the change and its potential impact. Amendments require a majority vote of the core development team and MUST be accompanied by a migration plan if existing practices or code need to be updated.

### Compliance Verification
Adherence to this constitution is a mandatory requirement for all code merged into the main branch. Code reviews MUST explicitly check for compliance with these principles. Any deviation MUST be justified and approved by the core development team.

### Versioning
The constitution will be versioned using semantic versioning (MAJOR.MINOR.PATCH). All changes to the constitution will be tracked and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03