# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST follow a strict unidirectional flow: Controllers depend on Services, Services depend on Repositories, and all layers depend on Models. Direct dependencies between unrelated layers (e.g., Controller directly accessing Repository) are forbidden.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., controllers, services, models) in isolation. Integration tests MUST verify interactions between components and with external systems (e.g., database, external APIs). A minimum of 80% code coverage MUST be maintained for all production code.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application startup. Configuration properties MUST be externalized and managed via `application.properties` or `application.yml`. Auto-configuration MUST be leveraged where appropriate, and custom configurations MUST be clearly documented.

### IV. RESTful API Design
Controllers exposing HTTP endpoints MUST follow RESTful principles. Resources MUST be identified by URIs, and standard HTTP methods (GET, POST, PUT, DELETE) MUST be used appropriately. Responses MUST utilize standard HTTP status codes to indicate success or failure.

### V. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Direct database access from other layers is strictly prohibited. JPA entities and their relationships MUST be clearly defined and validated.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java 17+, Spring Boot 3.x, Spring Data JPA, and Thymeleaf for templating.
**Database**: The primary database is H2 for development and testing. Integration tests for PostgreSQL and MySQL are provided, indicating support for these RDBMS.
**Containerization**: Kubernetes manifests (`k8s/`) are present, suggesting an intention for containerized deployment.
**Development Environment**: `.devcontainer/` indicates support for containerized development environments.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production releases, `develop` for integration, and feature branches for new development.
**Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member familiar with the project. Reviews MUST verify adherence to core principles, test coverage, and code quality.
**CI/CD**: Continuous Integration is expected, with automated builds, tests, and static analysis triggered on every commit to feature branches. Continuous Deployment to staging/production environments should be automated based on successful CI and manual approvals.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by at least two-thirds of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and practices comply with the changes. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-16