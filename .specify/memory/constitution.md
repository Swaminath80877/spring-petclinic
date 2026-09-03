# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing downwards from Controller to Repository, and through Service layers where applicable. Direct dependencies between unrelated layers (e.g., Repository directly calling Controller) are forbidden.

### II. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed using a Test-Driven Development (TDD) approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between layers and external systems (like databases), and end-to-end tests MUST verify critical user flows. A minimum of 80% code coverage MUST be maintained for all production code.

### III. Domain-Driven Design Principles
Core business entities (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST be clearly defined and encapsulate their behavior. Relationships between entities (e.g., `Owner` to `Pet`, `Pet` to `Visit`) MUST be managed consistently, adhering to JPA entity relationships. Business logic MUST reside within service or domain classes, not directly within controllers or repositories.

### IV. Configuration and Externalization
All application configuration, including database connection details, caching settings, and internationalization properties, MUST be externalized from the codebase. The project MUST leverage Spring Boot's configuration properties and profiles for managing environment-specific settings. Hardcoded values for such configurations are prohibited.

### V. Observability and Logging
The application MUST provide adequate logging for debugging and monitoring. Critical events, errors, and significant state changes MUST be logged using structured logging practices. The `src/main/resources/messages/messages.properties` file and its internationalized variants MUST be used for all user-facing strings.

## Development Workflow

The standard development workflow will follow these steps:
1.  **Feature/Bug Identification**: A clear requirement or bug is identified.
2.  **Test-Driven Development**: Write failing unit tests that define the expected behavior.
3.  **Implementation**: Write the minimal code necessary to make the tests pass.
4.  **Refactoring**: Improve the code quality and design while ensuring tests remain green.
5.  **Integration Testing**: Develop and run integration tests to verify interactions between components and layers.
6.  **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The PR MUST include comprehensive unit and integration tests.
7.  **CI/CD Pipeline**: Automated checks, including tests and static analysis, MUST pass before merging.
8.  **Deployment**: Deployment to staging and production environments will follow established CI/CD procedures.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution. Complexity in code or architecture MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03