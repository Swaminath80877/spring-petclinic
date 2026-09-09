# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between non-adjacent layers are prohibited.

### II. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed using a Test-Driven Development (TDD) approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (like databases), and end-to-end tests MUST verify critical user flows. Test coverage MUST be maintained at a minimum of 80%.

### III. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit) and their relationships MUST be modeled accurately and consistently across the application. Business logic MUST be encapsulated within the domain layer or dedicated service classes, not within controllers or repositories.

### IV. Spring Boot Conventions and Best Practices
The project MUST leverage Spring Boot's auto-configuration capabilities and follow its established conventions. Configuration MUST be externalized where appropriate (e.g., `application.properties`, `application.yml`). Dependency injection MUST be used for managing component lifecycles and dependencies.

### V. Observability and Logging
All significant events, errors, and state changes MUST be logged using structured logging. The application MUST expose metrics and health endpoints for monitoring and operational visibility.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST use Spring Framework and Spring Boot as the core application framework.
Database interactions MUST be managed through Spring Data JPA repositories.
The project MUST support multiple database integrations (e.g., MySQL, PostgreSQL) as demonstrated by existing integration tests.
Internationalization (i18n) MUST be implemented for all user-facing strings, as enforced by `I18nPropertiesSyncTest`.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs).
Each PR MUST be reviewed by at least one other team member.
Automated checks, including unit tests, integration tests, and static analysis, MUST pass before a PR can be merged.
Code reviews MUST verify adherence to the principles outlined in this constitution.
New features or significant refactorings require a design discussion and approval from the lead architect.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team.
Any approved amendments MUST include a migration plan to ensure existing code adheres to the new rules.
All Pull Requests and code reviews MUST explicitly verify compliance with this Constitution.
Complexity in the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09