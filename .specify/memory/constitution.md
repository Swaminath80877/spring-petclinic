# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between non-adjacent layers are prohibited.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components in isolation, while integration tests MUST validate interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and updated to reflect code changes.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and component scanning. Auto-configuration SHOULD be leveraged where appropriate, and custom configurations MUST be clearly documented and justified.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Domain entities MUST be designed to be POJOs with appropriate JPA annotations. Data access logic MUST be kept separate from business logic.

### V. RESTful API Design
Controller layer components MUST implement RESTful APIs following standard HTTP methods and status codes. Request and response payloads SHOULD be designed for clarity and efficiency, utilizing DTOs where necessary to decouple API contracts from internal domain models.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST use Maven as the build tool.
The project MUST be compatible with recent stable versions of Spring Boot and its associated dependencies.
Database interactions MUST be managed via Spring Data JPA.
Internationalization (i18n) MUST be handled using Spring's message source capabilities, with all user-facing strings externalized.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST include a clear description of the changes and the problem it solves.
All PRs MUST pass automated checks, including compilation, unit tests, and integration tests.
Code reviews are mandatory for all PRs, with at least one approval required before merging.
New features SHOULD follow an iterative development process, with frequent commits and PRs.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Any deviation from these principles MUST be explicitly justified and approved by the project lead.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28