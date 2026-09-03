# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Configuration, Domain/Model, Test, System). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified. Default Spring Boot conventions for dependency injection, component scanning, and property management MUST be followed.

### III. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed using a Test-Driven Development (TDD) approach. Unit tests MUST cover individual components, while integration tests (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`, `CrashControllerIntegrationTests`) MUST validate interactions between components and with external systems. All tests MUST pass before code is merged.

### IV. Domain Model Integrity
The `org.springframework.samples.petclinic.model` package MUST contain core, framework-agnostic domain entities (`BaseEntity`, `NamedEntity`). All other domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST extend these base classes and adhere to JPA and Bean Validation standards.

### V. Observability and Internationalization
Application behavior MUST be observable through structured logging. Internationalization (i18n) MUST be implemented using Spring's message source capabilities, and the `I18nPropertiesSyncTest` MUST pass to ensure all user-facing strings are translatable and consistently translated across all supported locales.

## Development Workflow

The standard development workflow involves:
1.  **Branching:** Create a new feature branch from `main`.
2.  **Development:** Implement functionality following the Core Principles, writing tests first.
3.  **Testing:** Ensure all unit and integration tests pass locally.
4.  **Code Review:** Submit a Pull Request (PR) to `main`. All PRs MUST be reviewed by at least one other team member.
5.  **CI/CD:** Automated checks (linting, testing, build) will run on the PR.
6.  **Merging:** Once approved and all checks pass, the PR can be merged into `main`.

## Governance

This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, a clear justification for the change, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All Pull Requests and code reviews MUST verify adherence to these principles.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03