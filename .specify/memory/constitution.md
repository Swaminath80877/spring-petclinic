# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations MUST be minimal and clearly justified, primarily for cross-cutting concerns like caching or internationalization as seen in `CacheConfiguration.java` and `WebConfiguration.java`.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and significant bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, while integration tests (e.g., `OwnerControllerTests.java`, `ClinicServiceTests.java`, `MySqlIntegrationTests.java`) MUST validate interactions between components and with the data layer.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with minimal dependencies, primarily focused on representing the core entities and their relationships. Persistence concerns SHOULD be handled by repositories.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) as demonstrated by `WebConfiguration.java` and `I18nPropertiesSyncTest.java`. Logging and error handling SHOULD be implemented to facilitate debugging and monitoring.

## Additional Constraints

The project MUST utilize Spring Boot and Spring Data JPA for its core framework and data access. All new dependencies MUST be carefully evaluated for necessity and impact on the overall architecture. Kubernetes deployment configurations are present in the `k8s/` directory, indicating a consideration for containerized deployments.

## Development Workflow

Development MUST follow a standard Gitflow or similar branching strategy. All code changes MUST be submitted via Pull Requests (PRs) and undergo a thorough code review by at least one other team member. Automated tests MUST pass before a PR can be merged.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15