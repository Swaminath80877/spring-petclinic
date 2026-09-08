# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring Boot patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), while integration tests MUST validate interactions between layers and with external dependencies (e.g., database, external APIs). Test coverage metrics MUST be maintained and reviewed.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be the central focus. Business logic SHOULD be encapsulated within the domain or service layers, not within controllers or repositories. Entities MUST adhere to JPA standards for persistence.

### V. Observability and Logging
All components MUST implement structured logging for debugging and monitoring. Critical events and errors MUST be logged with sufficient detail to facilitate root cause analysis. The `CrashController` serves as an example of handling and reporting errors.

## Development Workflow

### Code Reviews and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage requirements. Automated checks (e.g., static analysis, test execution) MUST pass before merging.

### Database Interaction
Repository interfaces (e.g., `OwnerRepository`, `VetRepository`) MUST be used for all data access operations. Direct SQL queries within service or controller layers are prohibited. Integration tests MUST verify database interactions, including persistence and retrieval of entities.

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source capabilities. The `I18nPropertiesSyncTest` enforces this by checking for untranslated strings and ensuring consistent translation across all supported locales.

## Governance
This constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST explicitly verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08