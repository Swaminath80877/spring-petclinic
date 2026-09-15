# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external dependencies (e.g., database, external APIs). Test coverage metrics MUST be tracked and maintained.

### III. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit) MUST be the central focus of the application's logic. Business logic SHOULD be encapsulated within these domain objects or associated service layers, minimizing anemic domain models.

### IV. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration SHOULD be externalized via properties files or environment variables. Dependency Injection MUST be used for managing component lifecycles and collaborations.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. Log levels MUST be configured appropriately for different environments. The application SHOULD expose metrics for monitoring key operational aspects.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST use Spring Boot as the core framework.
Database interactions MUST be managed via Spring Data JPA.
The project MUST support multiple database integrations (e.g., MySQL, PostgreSQL) as demonstrated by existing integration tests.
Containerization configurations (e.g., Docker, Kubernetes) SHOULD be maintained and kept up-to-date.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST be reviewed by at least one other team member.
Automated checks (CI pipeline) MUST pass before a PR can be merged. These checks include compilation, unit tests, integration tests, and code quality scans.
The `main` branch MUST always be in a deployable state.
Feature development SHOULD occur on dedicated feature branches.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository.
Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Any deviation from these principles MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15