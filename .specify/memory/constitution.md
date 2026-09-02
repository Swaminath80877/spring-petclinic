# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration properties MUST be managed via `application.properties` or `application.yml`. Dependency Injection MUST be achieved using Spring annotations.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, and integration tests MUST validate interactions between layers and external systems (e.g., database). All tests MUST pass before merging code.

### IV. Data Persistence Abstraction
Data access MUST be performed exclusively through Spring Data repositories. Direct SQL queries or manual JDBC operations are forbidden, except in highly specialized, well-justified scenarios.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) for user-facing messages, as evidenced by the presence of `messages*.properties` files and `WebConfiguration`. Logging MUST be used for debugging and monitoring.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., MySQL, PostgreSQL, H2).

**Security**: Input validation MUST be performed at the controller layer to prevent common web vulnerabilities.

**Performance**: Caching mechanisms, as indicated by `CacheConfiguration`, SHOULD be utilized where appropriate to improve performance.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for ongoing development, and feature branches for new work.

**Code Reviews**: All Pull Requests (PRs) MUST undergo at least one thorough code review by a team member familiar with the project. Reviews MUST verify adherence to this constitution.

**Quality Gates**: Automated checks, including compilation, static analysis (e.g., SonarQube), and all unit/integration tests, MUST pass before a PR can be merged.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02