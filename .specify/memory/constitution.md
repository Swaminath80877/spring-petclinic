# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project requirements beyond standard Spring Boot defaults.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, repositories, models) in isolation. Integration tests (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`, `CrashControllerIntegrationTests.java`) MUST validate interactions between components and with external systems (like databases). Test coverage metrics MUST be tracked and maintained.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner.java`, `Pet.java`, `Vet.java`, `Visit.java`) MUST remain pure Plain Old Java Objects (POJOs) or Jakarta Persistence entities, free from business logic that belongs in service layers. Validation logic MUST be implemented using Jakarta Bean Validation annotations and associated validators (e.g., `PetValidator.java`).

### V. Observability and Debuggability
All controllers and services MUST be designed with observability in mind. This includes clear logging of key operations and potential error conditions. The use of Spring Boot Actuator is encouraged for production monitoring.

## Development Workflow

The standard development workflow follows these steps:
1.  **Feature Branching**: Create a new branch for each feature or bug fix.
2.  **Development**: Implement the feature, adhering to the core principles. Write unit and integration tests concurrently.
3.  **Code Review**: Submit a Pull Request (PR) for review. All PRs MUST pass automated checks (linting, compilation, all tests). Reviewers MUST verify adherence to architectural principles and coding standards.
4.  **Testing**: Ensure all tests pass locally and in the CI pipeline.
5.  **Merge**: Once approved and all checks pass, merge the PR into the main branch.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, a clear justification, and approval by a majority of core maintainers. Any approved amendment MUST include a migration plan for existing code to ensure compliance. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28