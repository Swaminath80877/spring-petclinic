# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Direct dependencies MUST only flow downwards (e.g., Controllers depend on Services, Services depend on Repositories). Cross-layer dependencies are forbidden.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external dependencies (e.g., database, external APIs). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Compliance
The project MUST strictly adhere to Spring Boot conventions for configuration, dependency injection, and application startup. This includes leveraging auto-configuration where appropriate and using standard annotations (`@Autowired`, `@Service`, `@Repository`, `@Controller`, etc.).

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Direct database access from other layers is prohibited. JPA entities MUST be clearly defined and adhere to standard ORM practices.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The logging framework MUST be configured to provide sufficient detail for debugging and monitoring, with clear separation between different log levels (INFO, WARN, ERROR).

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be compatible with recent stable versions of Spring Boot and Jakarta EE.
Database interactions MUST be managed via Spring Data JPA.
The project MUST support internationalization (i18n) for user-facing messages, as evidenced by the `I18nPropertiesSyncTest`.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST be reviewed by at least one other team member.
Automated checks, including static analysis and unit/integration tests, MUST pass before a PR can be merged.
The `.devcontainer` configuration MUST be used for consistent development environments.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository.
Amendments to this constitution require a formal proposal, review by the core development team, and a majority approval.
All PRs and code reviews MUST verify compliance with these principles.
Any deviation from these principles MUST be explicitly justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28