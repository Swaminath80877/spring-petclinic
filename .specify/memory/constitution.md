# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Cross-layer dependencies MUST follow a strict top-down flow (Controller -> Service -> Repository -> Domain). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal, well-documented, and only introduced when explicit customization is required beyond standard Spring Boot features.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST target individual components in isolation, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external services). Test coverage MUST be maintained at a minimum of 80%.

### IV. Domain Model Integrity
The domain model (entities like `Owner`, `Pet`, `Vet`, `Visit`) MUST remain pure and free from framework-specific annotations or logic where possible, except for necessary JPA/validation annotations. Business logic SHOULD reside in service layers, not directly within domain entities.

### V. Observability and Debuggability
All controllers and services MUST be designed to facilitate logging and tracing. Use of Spring Boot Actuator or similar mechanisms for monitoring health and metrics is encouraged. Error handling MUST be consistent and provide sufficient detail for debugging.

## Development Workflow

### Code Review and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage requirements. Automated checks (e.g., static analysis, test execution) MUST pass before a pull request can be merged.

### Dependency Management
Dependencies MUST be managed via Maven. New dependencies MUST be carefully evaluated for necessity and potential impact on the project. Version conflicts MUST be resolved promptly.

### Database Interaction
All data access MUST be performed through Spring Data JPA repositories. Direct SQL queries should be avoided unless absolutely necessary and clearly justified. Integration tests MUST cover database interactions, including schema changes and data persistence.

## Governance
This constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a clear migration plan if they impact existing code or workflows. Compliance with this constitution is a mandatory requirement for all code merged into the main branch.

**Version**: 1.0.0 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-16