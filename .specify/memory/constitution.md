# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers are forbidden.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and only introduced when explicit control or extension is required.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), and integration tests MUST verify interactions between components and with external systems (e.g., database, external APIs). Test coverage MUST be tracked and maintained.

### IV. JPA Repository Pattern Enforcement
All data access operations MUST be performed through Spring Data JPA repositories. Custom repository implementations are discouraged unless absolutely necessary and MUST be clearly justified. Repositories MUST be designed for efficient data retrieval and manipulation.

### V. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST encapsulate business logic and state. They MUST adhere to JPA standards for persistence and validation constraints MUST be applied to ensure data integrity.

## Additional Constraints

### Technology Stack
The project MUST primarily utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Any deviation from this stack requires a formal proposal and approval.

### Database Agnosticism
While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database technology.

## Development Workflow

### Code Reviews
All code changes submitted via Pull Requests MUST undergo a thorough review by at least one other team member. Reviews MUST verify adherence to core principles, architectural guidelines, and coding standards.

### Testing Gates
Automated tests MUST pass in the CI pipeline before any code can be merged. Integration tests covering critical paths and database interactions are mandatory.

Governance
This constitution supersedes all other development practices. Amendments require a formal proposal, documented justification, and approval by a majority of the core development team. Compliance with this constitution is a mandatory requirement for all code merged into the main branch.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02