# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., a Controller MUST NOT directly call a Repository). Dependencies MUST flow downwards through defined interfaces or service abstractions.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components in isolation, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external APIs). A minimum of 80% code coverage for new code is expected.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations SHOULD be minimal and clearly documented, adhering to standard Spring Boot practices for dependency injection, component scanning, and application setup.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be POJOs with clear responsibilities. They SHOULD encapsulate business logic related to their domain and interact with persistence layers through repositories. Validation constraints (e.g., `@NotNull`, `@NotEmpty`) MUST be applied to domain models to ensure data integrity.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST be designed to support monitoring and debugging through appropriate logging levels and clear log messages.

## Additional Constraints

The Spring PetClinic application is a web application built on the Spring Framework. The following constraints apply:

*   **Technology Stack**: The primary technology stack includes Java, Spring Boot, Spring Data JPA, Thymeleaf for templating, and H2/PostgreSQL/MySQL for database persistence.
*   **Database Interaction**: All data access MUST be performed through Spring Data JPA repositories. Direct SQL queries within controllers or services are discouraged.
*   **Internationalization (i18n)**: All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` enforces this.
*   **Testing Frameworks**: JUnit 5 and AssertJ are the primary testing frameworks. Mockito MAY be used for mocking dependencies in unit tests.
*   **Containerization**: The project includes `.devcontainer` and `k8s` directories, indicating an intent to support containerized development and deployment.

## Development Workflow

*   **Branching Strategy**: Feature development MUST occur on dedicated feature branches. All changes MUST be submitted via Pull Requests (PRs).
*   **Code Reviews**: All PRs MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.
*   **CI/CD**: Continuous Integration is expected to be automated, including building, testing, and static analysis. Continuous Deployment MAY be configured based on successful CI pipelines.
*   **Dependency Management**: Dependencies MUST be managed via Maven `pom.xml`. Updates to dependencies SHOULD be done incrementally and tested thoroughly.

## Governance

This constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02