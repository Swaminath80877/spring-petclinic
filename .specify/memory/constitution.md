# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external services (e.g., database). Existing tests MUST be maintained and updated.

### III. Spring Boot Conventions
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application bootstrapping. Custom configurations MUST be clearly defined and documented within the `configuration` layer.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Direct database access from other layers is strictly prohibited. Data access logic MUST be encapsulated and tested.

### V. RESTful API Design
Controller layer components MUST implement RESTful APIs following standard HTTP methods and status codes. Request and response payloads SHOULD be well-defined and consistent.

## Additional Constraints

The project MUST utilize Spring Boot as the primary framework.
Database interactions MUST be managed via Spring Data JPA.
The project MUST be containerized using Docker, with Kubernetes deployment configurations provided in the `k8s/` directory.
Development environment setup MUST be supported via `.devcontainer/`.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST undergo a thorough code review by at least one other team member.
Automated checks, including unit tests, integration tests, and static analysis, MUST pass before a PR can be merged.
Adherence to the established coding style and architectural principles MUST be verified during code reviews.

## Governance
This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. All existing code MUST be migrated to comply with any amendments within a reasonable timeframe, to be defined per amendment. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09