# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, and integration tests MUST verify interactions between layers and external services (e.g., database). Existing tests MUST NOT be broken by new changes.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly documented and justified, adhering to Spring best practices.

### IV. Data Persistence Abstraction
All data access operations MUST be performed through the defined Repository interfaces. Direct SQL queries or manual JDBC operations within service or controller layers are forbidden. The use of JPA and Spring Data JPA is mandated for data persistence.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Request and response bodies SHOULD be in JSON format.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be compatible with recent stable versions of Spring Boot and Spring Framework.
Database interactions MUST be managed via JPA entities and Spring Data repositories.
Internationalization (i18n) MUST be handled using Spring's message source mechanisms, and all user-facing strings MUST be externalized.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs).
Each PR MUST include a clear description of the changes and the problem it solves.
All PRs MUST undergo a thorough code review by at least one other team member.
Automated checks (CI pipeline) MUST pass before a PR can be merged. These checks include compilation, unit tests, and integration tests.
New features or significant refactorings SHOULD be discussed and agreed upon by the team before implementation.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team.
Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Complexity in the codebase MUST be justified and minimized. The principle of "You Ain't Gonna Need It" (YAGNI) should be followed.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02