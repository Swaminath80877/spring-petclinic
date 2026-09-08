# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST follow a strict top-down flow (Controller -> Service -> Repository -> Model). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), while integration tests MUST validate interactions between layers and with external systems (e.g., databases via `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`). Test coverage MUST be tracked and maintained.

### IV. Domain Model Integrity
Domain entities (`Owner.java`, `Pet.java`, `Vet.java`, etc.) MUST be POJOs with minimal logic, primarily focused on data representation and relationships. Persistence concerns (JPA annotations) MUST be confined to these entities. Business logic MUST be encapsulated within service classes.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) as evidenced by `I18nPropertiesSyncTest.java` and `WebConfiguration.java`. All user-facing strings MUST be externalized and managed through resource bundles. Logging MUST be implemented to facilitate debugging and monitoring.

## Additional Constraints

The project MUST utilize Spring Framework and Spring Boot as its core foundation. Database interactions MUST be managed through Spring Data JPA. The project MUST be containerizable, as indicated by the presence of `k8s/` and `.devcontainer/` directories.

## Development Workflow

All code changes MUST be submitted via Pull Requests. Each Pull Request MUST undergo a thorough code review by at least one other team member, verifying adherence to this constitution. Automated checks, including static analysis and test execution, MUST pass before merging.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST explicitly verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08