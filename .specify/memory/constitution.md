# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers.

### II. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed using a TDD approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (like databases), and end-to-end tests MUST verify user flows. Test coverage MUST be maintained at a minimum of 80%.

### III. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST be the central focus of the application. Business logic MUST be encapsulated within these domain objects or associated service layers, not within controllers or repositories.

### IV. Spring Boot Conventions and Best Practices
The project MUST leverage Spring Boot's auto-configuration and conventions. Configuration MUST be externalized using properties files or environment variables. Dependency Injection MUST be used for managing component lifecycles and dependencies.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST provide metrics for key operations, enabling monitoring and debugging.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. JPA and Hibernate MUST be used for data persistence. The application is designed to be deployable within a containerized environment (e.g., Docker).

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs). Each PR MUST include comprehensive unit and integration tests. Code reviews are mandatory, with at least one reviewer approving the changes. Automated CI/CD pipelines MUST run all tests and perform static code analysis before merging.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic project. Amendments to this Constitution require a formal proposal, a review period, and approval by a majority of core maintainers. All existing code MUST be migrated to comply with any amendments within a reasonable timeframe, as defined by the amendment proposal. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02