# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories directly; they MUST interact via Services).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project needs beyond standard Spring Boot defaults.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (Controllers, Services, Models), and integration tests MUST verify interactions between layers and with external dependencies (e.g., database, external APIs). Test coverage metrics MUST be maintained and reviewed.

### IV. Domain Model Integrity
The domain model (entities like `Owner`, `Pet`, `Vet`, `Visit`) MUST remain pure and free from presentation or persistence concerns. Entities MUST adhere to JPA standards for persistence and Jakarta Bean Validation for data integrity.

### V. Observability and Diagnostics
The application MUST provide sufficient logging and error reporting to facilitate debugging and monitoring. The `CrashController` and its associated tests indicate a focus on handling and reporting unexpected errors.

## Development Workflow

The development workflow will follow a standard agile approach, emphasizing iterative development and continuous feedback.

*   **Feature Development**: Features will be developed in isolation, adhering to the layered architecture and test coverage principles.
*   **Code Reviews**: All code changes submitted via Pull Requests (PRs) MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.
*   **Testing Gates**: Automated tests (unit and integration) MUST pass successfully before a PR can be merged. CI/CD pipelines will enforce this gate.
*   **Deployment**: Deployments will be managed through automated pipelines, with clear rollback strategies in place.

## Governance

This constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. Any approved amendments MUST include a migration plan to ensure existing code and practices are brought into compliance. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST always be justified with clear benefits.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03