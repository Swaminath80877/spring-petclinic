# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST strictly follow the defined order (e.g., Controllers depend on Services/Repositories, not vice-versa).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual component logic, while integration tests MUST validate interactions between layers and external dependencies (e.g., database, external services). Test coverage metrics MUST be maintained and reviewed.

### IV. Domain Model Integrity
The domain model (`BaseEntity`, `NamedEntity`, `Owner`, `Pet`, `Vet`, `Visit`, `Specialty`, `PetType`) MUST remain the central source of truth. All business logic and data persistence operations MUST originate from or be validated against this model.

### V. Observability and Debuggability
Application behavior MUST be observable through structured logging and appropriate exception handling. Integration tests, particularly those involving database interactions (`MySqlIntegrationTests`, `PostgresIntegrationTests`), MUST be designed to facilitate debugging and root cause analysis.

## Development Workflow

The development workflow for the Spring Petclinic project will adhere to the following process:

1.  **Feature/Bug Identification**: Issues are logged and prioritized in the project's issue tracker.
2.  **Branching Strategy**: Development MUST occur on feature branches, branched from the main development branch (e.g., `develop`).
3.  **Development**: Implement the feature or fix the bug, adhering to the Core Principles. This includes writing unit and integration tests.
4.  **Local Testing**: Run all tests locally to ensure functionality and prevent regressions.
5.  **Code Review**: Submit a Pull Request (PR) to the main development branch. The PR MUST include a clear description of changes and link to the relevant issue. At least one other developer MUST review the code.
6.  **CI/CD Pipeline**: Upon merging to the main development branch, the CI/CD pipeline will automatically build, test, and deploy to staging environments.
7.  **Staging Deployment**: Once validated on staging, the changes can be deployed to production.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic project. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify adherence to this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08