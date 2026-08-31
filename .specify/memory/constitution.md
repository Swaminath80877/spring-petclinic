# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). Direct dependencies MUST only flow downwards (e.g., Controllers depend on Services, Services depend on Repositories). Cross-layer dependencies are forbidden.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project needs beyond default behavior.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), and integration tests MUST verify interactions between layers and with external systems (e.g., database, external APIs). Test coverage MUST be tracked and maintained.

### IV. Domain Model Integrity
Domain entities (`Owner.java`, `Pet.java`, `Vet.java`, `Visit.java`, `PetType.java`, `Specialty.java`) MUST be the single source of truth for data structures. All data manipulation and validation MUST occur through these entities or their associated services.

### V. Observability and Debuggability
Application behavior MUST be observable through structured logging and, where applicable, metrics. The use of `java.util.logging` or `slf4j` is mandated for all logging.

## Additional Constraints

**Technology Stack**: The project MUST utilize Spring Boot, JPA for data persistence, and Thymeleaf for server-side rendering. External dependencies MUST be managed via Maven.

**Database Agnosticism**: While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database technology.

**Internationalization**: All user-facing strings MUST be internationalized using Spring's message source mechanism, as enforced by tests like `I18nPropertiesSyncTest.java`.

## Development Workflow

**Branching Strategy**: Feature development MUST occur on dedicated feature branches. All code MUST be submitted via Pull Requests.

**Code Reviews**: All Pull Requests MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to this constitution.

**Quality Gates**: Automated checks, including static analysis, unit tests, and integration tests, MUST pass before a Pull Request can be merged.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution. Complexity MUST be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31