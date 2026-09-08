# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly upward (e.g., Controller depends on Service, Service depends on Repository). Direct dependencies between non-adjacent layers are prohibited.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., Controllers, Services, Models) in isolation. Integration tests MUST verify interactions between layers and with external systems (e.g., database, external APIs). Existing tests MUST be maintained and updated to reflect code changes.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and only implemented when standard Spring Boot features are insufficient.

### IV. JPA Repository Pattern Enforcement
Data access MUST be exclusively handled through Spring Data JPA repositories. All database operations MUST be encapsulated within `*-Repository.java` interfaces. Direct SQL queries or manual JDBC operations within service or controller layers are forbidden.

### V. RESTful API Design
Controllers MUST adhere to RESTful principles for API design. Endpoints MUST be resource-oriented, use appropriate HTTP methods (GET, POST, PUT, DELETE), and return standard HTTP status codes. JSON is the primary data format for API interactions.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be compatible with recent stable versions of Spring Boot and Spring Framework.
Database interactions MUST be managed via JPA and Hibernate.
Internationalization (i18n) MUST be handled using Spring's message source mechanism, with all user-facing strings externalized.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST include a clear description of the changes and the problem it solves.
All PRs MUST pass automated checks, including compilation, unit tests, and integration tests.
Code reviews are mandatory for all PRs. At least one reviewer MUST approve the PR before merging.
The `main` branch is protected and can only be merged into via approved PRs.

## Governance
This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution. Complexity MUST be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08