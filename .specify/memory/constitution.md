# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories). This ensures clear separation of concerns and maintainability.

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot features and follow established Spring conventions. This includes utilizing dependency injection, auto-configuration where appropriate, and adhering to Spring's programming model for web controllers, data access, and configuration.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST verify individual component logic, while integration tests MUST validate interactions between layers and external systems (e.g., database). Test coverage MUST be maintained at a high level, with critical paths having near-complete coverage.

### IV. Data Persistence Abstraction
Data access logic MUST be encapsulated within repository interfaces, leveraging Spring Data JPA. Domain entities MUST be mapped to persistence mechanisms via these repositories. Direct SQL queries or manual persistence management within controllers or services is forbidden.

### V. Observability and Configuration Management
Application configuration MUST be externalized and managed through Spring Boot's configuration properties. Logging MUST be implemented using standard frameworks (e.g., SLF4j) with appropriate levels for debugging and monitoring. Internationalization (i18n) MUST be handled via properties files as demonstrated in `I18nPropertiesSyncTest.java`.

## Development Workflow

The standard development workflow for the Spring Petclinic project is as follows:

1.  **Feature/Bug Identification**: A new feature request or bug is identified.
2.  **Branching**: A new feature branch is created from the main development branch (e.g., `develop`).
3.  **Development**: Code is written, adhering to the Core Principles. This includes:
    *   Implementing new components or modifying existing ones within their respective layers.
    *   Writing comprehensive unit and integration tests for all changes.
    *   Ensuring all new strings are internationalized.
    *   Updating configuration properties as needed.
4.  **Local Testing**: All tests (unit and integration) MUST pass locally.
5.  **Code Review**: A Pull Request (PR) is created against the `develop` branch. The PR MUST include a clear description of the changes and link to the relevant issue or task. All PRs MUST be reviewed by at least one other team member. Reviewers MUST verify adherence to the Core Principles and test coverage.
6.  **CI/CD Pipeline**: Upon merging to `develop`, the CI/CD pipeline automatically builds, tests, and deploys to a staging environment.
7.  **Release**: After successful testing on staging, changes are merged to the main release branch (e.g., `main` or `master`) and deployed to production.

## Governance

This Constitution supersedes all other informal practices and documentation. Amendments to this Constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a clear migration plan if they impact existing code or processes. All Pull Requests and code reviews MUST verify compliance with this Constitution. Complexity MUST always be justified with clear reasoning and documentation.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09