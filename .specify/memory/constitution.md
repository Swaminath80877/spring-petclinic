# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). The separation of concerns MUST be strictly maintained, with dependencies flowing downwards (e.g., Controllers depend on Services, Services depend on Repositories).

### II. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed using a Test-Driven Development (TDD) approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between layers and external services (e.g., database), and end-to-end tests MUST verify critical user flows. The existing test suite, including integration tests for various databases (MySQL, PostgreSQL), MUST be maintained and expanded.

### III. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST be the central source of truth for application data. They MUST be POJOs (Plain Old Java Objects) with appropriate JPA annotations for persistence and Jakarta Bean Validation annotations for data integrity. Changes to the domain model MUST be carefully considered for their impact on the entire application.

### IV. Spring Boot Convention and Configuration
The project MUST leverage Spring Boot conventions for auto-configuration and dependency management. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly defined and documented, adhering to Spring's best practices.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) as evidenced by the `I18nPropertiesSyncTest` and `WebConfiguration`. All user-facing strings MUST be externalized into resource bundles. Logging and error handling mechanisms MUST be robust to facilitate debugging and monitoring.

## Development Workflow

The standard development workflow will follow these steps:
1.  **Feature/Bug Identification**: A clear requirement or bug is identified.
2.  **Test-First Development**: Write failing unit or integration tests that define the expected behavior.
3.  **Implementation**: Write the minimal code necessary to make the tests pass.
4.  **Refactoring**: Improve the code quality and design while ensuring tests remain green.
5.  **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. PRs MUST include descriptions of changes and link to relevant issues.
6.  **CI/CD Pipeline**: Automated tests and builds are executed upon PR creation and merge.
7.  **Deployment**: Approved and tested code is deployed to production.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, review by at least two senior architects, and a documented migration plan if significant changes are introduced. All Pull Requests and code reviews MUST verify compliance with these principles. Complexity in the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08