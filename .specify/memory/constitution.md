# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Configuration, Domain/Model). Cross-layer dependencies MUST be strictly unidirectional, flowing from Controller down to Repository and Domain.

### II. Test-Driven Development (TDD) for New Features
All new features and significant modifications MUST be developed following a TDD approach. Tests MUST be written and pass before the corresponding production code is committed. Unit tests MUST cover individual components, and integration tests MUST validate interactions between layers and external systems.

### III. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be clearly documented and justified. Avoid unnecessary boilerplate code.

### IV. Data Access Layer Abstraction
The Repository layer MUST abstract all data access logic. Controllers and Services MUST interact solely with repository interfaces, not directly with underlying data sources or ORM specifics.

### V. Observability and Logging
All components MUST implement appropriate logging. Critical operations, errors, and significant state changes MUST be logged with sufficient detail to facilitate debugging and monitoring. Structured logging is preferred.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Dependencies MUST be managed via Maven.

**Database Agnosticism**: While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database technology.

**Internationalization (i18n)**: All user-facing strings MUST be internationalized and managed through properties files. The `I18nPropertiesSyncTest.java` MUST pass to ensure comprehensive translation coverage.

## Development Workflow

**Code Reviews**: All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Continuous Integration**: Automated builds and tests MUST be executed on every commit to feature branches and on every merge to `develop`.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31