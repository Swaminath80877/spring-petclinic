# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST include comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external APIs). Existing tests MUST be maintained and updated.

### III. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be defined in the `model` or respective domain packages and MUST adhere to JPA/Jakarta Persistence standards. Business logic related to these entities SHOULD be encapsulated within the entities themselves or in dedicated service classes.

### IV. Configuration Separation
Application configuration, including caching (`CacheConfiguration.java`) and web/internationalization settings (`WebConfiguration.java`), MUST be managed in dedicated configuration classes. These classes SHOULD be annotated with `@Configuration` and leverage Spring Boot's auto-configuration capabilities where appropriate.

### V. Observability and Logging
All components MUST implement structured logging to facilitate debugging and monitoring. Critical operations and potential failure points SHOULD be logged with appropriate severity levels.

## Additional Constraints

**Technology Stack**: The project MUST utilize Spring Boot, JPA/Hibernate for data persistence, and JUnit 5 for testing. Dependencies MUST be managed via Maven.

**Database Agnosticism**: While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database technology.

**Internationalization**: All user-facing strings MUST be internationalized using Spring's message source mechanism, as enforced by tests like `I18nPropertiesSyncTest.java`.

## Development Workflow

**Branching Strategy**: Feature development MUST occur on dedicated feature branches. All code changes MUST be submitted via Pull Requests.

**Code Reviews**: All Pull Requests MUST undergo at least one thorough code review by a team member familiar with the affected codebase. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**Continuous Integration**: Automated builds and tests MUST be executed on every commit to the main development branches. Builds that fail tests or violate static analysis rules MUST be addressed immediately.

## Governance
This Constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All Pull Requests and code reviews MUST explicitly verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31