# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers (e.g., Controllers directly accessing Repositories) are forbidden.

### II. Domain-Driven Design Principles
Domain entities (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST encapsulate their state and behavior. Business logic MUST reside within the domain or service layers, not within controllers or repositories. Data access MUST be abstracted by repository interfaces.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and with external dependencies (e.g., database). Test coverage MUST be maintained above 80%.

### IV. Explicit Configuration Management
Application configuration, including database connections, caching, and internationalization, MUST be managed through dedicated configuration classes (e.g., `CacheConfiguration.java`, `WebConfiguration.java`). Externalized configuration properties MUST be used where appropriate.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST provide mechanisms for monitoring its health and performance, particularly around database interactions and request handling.

## Additional Constraints

**Technology Stack**: The project MUST utilize Spring Boot, Spring Data JPA, and Thymeleaf for web rendering. Dependencies MUST be managed via Maven.

**Database Agnosticism**: While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database implementation.

**Internationalization (i18n)**: All user-facing strings MUST be internationalized using properties files. The `I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across all supported locales.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**Continuous Integration**: Automated builds, tests, and static analysis MUST be executed on every commit to feature branches and on every merge to `develop`.

**Deployment Gates**: Successful CI builds, passing integration tests against a staging environment, and explicit approval from the release manager are required before deployment to production.

## Governance
This constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15