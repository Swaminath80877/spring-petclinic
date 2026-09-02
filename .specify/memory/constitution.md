# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST be strictly unidirectional, flowing downwards (e.g., Controllers depend on Services, Services depend on Repositories).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring Boot patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), while integration tests MUST validate interactions between layers and with external systems (e.g., database, external APIs). Test coverage MUST be tracked and maintained.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be the central focus. Business logic resides within the domain or service layers, not directly in controllers or repositories. Entities MUST be POJOs with appropriate JPA annotations for persistence.

### V. Observability and Debuggability
Application behavior MUST be observable through structured logging and clear exception handling. The `CrashController` serves as an example of handling unexpected errors. Internationalization (`I18nPropertiesSyncTest`) is a key aspect of user-facing observability.

## Development Workflow

The typical development workflow for the Spring PetClinic project is as follows:

1.  **Feature/Bug Identification**: A new feature request or bug is identified.
2.  **Design & Planning**: The impact on the existing architecture and layers is assessed. Any proposed changes to core principles or established patterns must be documented and approved.
3.  **Development**:
    *   Write comprehensive unit tests for new or modified components.
    *   Implement the feature or fix the bug, ensuring adherence to layered architecture and domain-driven principles.
    *   Write integration tests to verify interactions and end-to-end functionality.
    *   Ensure all new code is properly internationalized where applicable.
4.  **Code Review**: All code changes MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, architectural integrity, test coverage, and code quality.
5.  **Testing**: Automated tests (unit and integration) MUST pass in the CI/CD pipeline. Manual testing may be performed as needed.
6.  **Deployment**: Approved changes are deployed to staging and production environments.

## Governance

This constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan for existing code to ensure compliance. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST always be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02