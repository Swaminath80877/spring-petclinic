# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories, Repositories interact with the data source). Direct dependencies between non-adjacent layers are prohibited unless explicitly justified and documented.

### II. Spring Boot Convention Compliance
The project MUST leverage Spring Boot's auto-configuration and conventions. Configuration MUST be managed via properties files (`application.properties` or `application.yml`) and Java-based configuration classes (e.g., `WebConfiguration.java`, `CacheConfiguration.java`). Dependency injection MUST be managed by Spring's IoC container.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify interactions between components and with external systems (e.g., database). Test coverage MUST be maintained at a minimum of 80% for critical business logic.

### IV. Data Persistence Abstraction
Data access MUST be performed exclusively through Spring Data repositories (e.g., `OwnerRepository`, `VetRepository`). Direct SQL queries or manual JDBC operations within business logic or controller layers are forbidden. Entities MUST adhere to JPA specifications.

### V. Internationalization and Localization
All user-facing strings MUST be externalized into resource bundles (e.g., `messages.properties`). The `WebConfiguration` MUST correctly configure locale resolution and handling. Tests MUST verify the presence and consistency of translations across supported locales.

## Development Workflow

The development workflow is structured to ensure code quality, maintainability, and adherence to the core principles.

1.  **Feature Development**: New features or bug fixes begin with the creation of relevant unit and integration tests that define the expected behavior.
2.  **Code Implementation**: The feature is then implemented, ensuring it adheres to the layered architecture and Spring Boot conventions.
3.  **Local Testing**: All tests (unit and integration) MUST pass locally before committing.
4.  **Code Review**: A Pull Request (PR) MUST be created for all code changes. The PR MUST include a clear description of the changes and link to any relevant issues. At least one other developer MUST review and approve the PR. Reviewers MUST verify adherence to the constitution's principles.
5.  **CI/CD Pipeline**: Upon merging to the main branch, the CI/CD pipeline will automatically run all tests and static analysis checks.
6.  **Deployment**: Successful pipeline runs enable deployment to staging and production environments.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, a documented justification, and approval by at least two-thirds of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and processes are updated accordingly. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST always be justified with clear benefits.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28