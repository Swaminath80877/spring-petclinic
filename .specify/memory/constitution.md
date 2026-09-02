# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations MUST be clearly documented and justified.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Existing tests MUST pass, and new tests MUST achieve at least 90% code coverage for new or modified code. Integration tests MUST cover interactions between layers and external services.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`) MUST be POJOs with clear responsibilities. They MUST NOT contain business logic that belongs in the service layer. Persistence concerns (JPA annotations) MUST be confined to the model layer.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST provide mechanisms for monitoring its health and performance.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Technology Stack**: The primary technology stack is Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating.
*   **Database**: The application is designed to work with relational databases, with explicit support for MySQL and PostgreSQL demonstrated through integration tests.
*   **Containerization**: The project includes a `.devcontainer` configuration, indicating an intent to support development within containers. Kubernetes manifests (`k8s/`) suggest deployment considerations.

## Development Workflow

*   **Branching Strategy**: Feature development MUST occur on dedicated feature branches.
*   **Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member familiar with the project. Reviews MUST verify adherence to this constitution.
*   **Continuous Integration**: Automated builds and tests MUST be executed on every commit to the main development branch.
*   **Deployment**: Deployments to production environments MUST be preceded by successful integration and user acceptance testing.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All pull requests and code reviews MUST verify compliance with this constitution. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02