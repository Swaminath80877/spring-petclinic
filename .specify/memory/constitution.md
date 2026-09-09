# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database). Existing tests MUST be maintained and updated.

### III. Spring Boot Convention Compliance
The project MUST strictly adhere to Spring Boot conventions for configuration, dependency injection, and application bootstrapping. Auto-configuration MUST be leveraged where appropriate, and custom configurations MUST be clearly documented.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Direct database access from other layers (e.g., Controllers, Services) is FORBIDDEN. Data access logic MUST be encapsulated within repository interfaces.

### V. RESTful API Design
Controllers MUST implement RESTful principles for API design. Resources MUST be exposed via clear, predictable URLs, and HTTP methods (GET, POST, PUT, DELETE) MUST be used appropriately. Responses SHOULD be in JSON format.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. External dependencies MUST be managed via Maven.

**Database**: The application is designed to work with relational databases. Integration tests MUST cover at least one common RDBMS (e.g., PostgreSQL, MySQL).

**Containerization**: Kubernetes manifests are provided in the `k8s/` directory, indicating an intent for containerized deployment.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to core principles, code quality, and test coverage.

**Quality Gates**: Automated checks, including static analysis (e.g., SonarQube integration if applicable) and test execution, MUST pass before merging code into `develop` or `main`.

## Governance
This constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code adheres to the new rules. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09