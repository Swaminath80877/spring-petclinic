# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers, except for explicit dependency injection.

### II. Test-Driven Development (TDD) for New Features
All new features and significant modifications MUST be developed following a TDD approach. Tests MUST be written and pass before the corresponding production code is committed. Existing functionality MUST be covered by comprehensive unit and integration tests.

### III. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST remain pure Plain Old Java Objects (POJOs) or Jakarta Persistence entities, free from presentation logic or direct framework dependencies beyond persistence annotations.

### IV. Explicit Dependency Management
Dependencies between modules and classes MUST be explicit and managed through constructor injection, setter injection, or Spring's `@Autowired` annotation. Implicit dependencies or direct instantiation of other components are forbidden.

### V. Observability and Logging
All significant operations, errors, and state changes MUST be logged using structured logging. The application MUST provide mechanisms for monitoring key metrics and health checks, particularly for database interactions and request handling.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Framework:** Spring Boot 3.x, Jakarta EE 10.
*   **Database:** Primarily uses JPA with H2 for in-memory testing and PostgreSQL/MySQL for integration tests. Database interactions MUST be managed through Spring Data JPA repositories.
*   **Testing:** JUnit 5, AssertJ, Mockito, Spring Test. Integration tests MUST cover database interactions and controller endpoints.
*   **Build Tool:** Maven.
*   **Containerization:** Kubernetes manifests are provided in `k8s/`, indicating an intent for containerized deployment.
*   **Development Environment:** `.devcontainer/` suggests support for containerized development environments.

## Development Workflow

*   **Branching Strategy:** Feature branches MUST be created from the `main` branch. All changes MUST be submitted via Pull Requests (PRs) targeting the `main` branch.
*   **Code Reviews:** All PRs MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviewers MUST verify adherence to this constitution.
*   **Automated Checks:** CI pipelines MUST include static analysis, unit tests, integration tests, and security vulnerability scans.
*   **Deployment:** Deployments to production environments MUST be triggered only after successful completion of all CI checks and explicit approval from a designated release manager.

## Governance
This constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Any proposed amendments to this constitution MUST be documented, justified, and approved by a majority of the core development team. A migration plan MUST be provided for any changes that impact existing code or workflows. All Pull Requests and code reviews MUST verify compliance with these principles. Complexity introduced into the codebase MUST be clearly justified and aligned with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03