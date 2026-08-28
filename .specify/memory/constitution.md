# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between sibling layers or from lower to higher layers are forbidden.

### II. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed using a Test-Driven Development (TDD) approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (like databases), and end-to-end tests MUST verify critical user flows. Test coverage MUST be maintained at a minimum of 80%.

### III. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST be the central focus of the application. Business logic MUST be encapsulated within these domain objects or their associated service layers. Data access MUST be abstracted through repository interfaces.

### IV. Configuration Management and Externalization
Application configuration, including database connection details, caching settings, and internationalization properties, MUST be externalized from the codebase. Spring Boot's configuration mechanisms (e.g., `application.properties`, environment variables) MUST be utilized.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. Log levels MUST be appropriately configured to facilitate debugging and monitoring in various environments.

## Additional Constraints

**Technology Stack**: The project MUST exclusively use Java as the primary programming language, Spring Boot as the application framework, and JPA for data persistence. Frontend technologies are not within the scope of this constitution.

**Database Agnosticism**: While integration tests may target specific databases (e.g., MySQL, PostgreSQL), the core application logic MUST remain agnostic to the underlying database implementation, relying on JPA abstractions.

**Internationalization (i18n)**: All user-facing strings MUST be internationalized using Spring's message source capabilities. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy MUST be employed, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member familiar with the project. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**Continuous Integration**: A CI pipeline MUST be in place to automatically build, test, and analyze the code upon every commit to a feature branch and upon merging to `develop`.

**Deployment**: Deployments to production environments MUST be preceded by successful integration and end-to-end tests in a staging environment that mirrors production.

## Governance

This constitution supersedes all other development practices and conventions for the Spring Petclinic project. Amendments to this constitution require a formal proposal, a documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28