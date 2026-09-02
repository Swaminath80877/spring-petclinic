# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Compliance
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `@Configuration` classes. Dependency injection MUST be achieved using Spring's annotations (`@Autowired`, `@Component`, etc.).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (like databases), and end-to-end tests MUST verify user flows. All tests MUST pass before code is merged.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. Direct SQL queries within business logic are prohibited. All repository interfaces MUST extend `JpaRepository` or a similar Spring Data interface.

### V. Observability and Logging
Application behavior and potential issues MUST be observable through structured logging. All significant events, errors, and state changes MUST be logged using a consistent format. The `Logback` framework, as provided by Spring Boot, MUST be used for logging.

## Additional Constraints

**Technology Stack**: The project MUST be built using Java and Spring Boot. Dependencies MUST be managed via Maven. The primary database technology is relational (e.g., MySQL, PostgreSQL, H2 for testing).

**Security**: Input validation MUST be performed at the controller layer to prevent common web vulnerabilities. Sensitive data MUST NOT be logged or stored in plain text.

**Internationalization (i18n)**: All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is encouraged, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All Pull Requests (PRs) MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to the constitution, code quality, and test coverage.

**Quality Gates**: Automated checks, including static analysis (e.g., SonarQube integration if applicable), unit tests, and integration tests, MUST pass before a PR can be merged.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All Pull Requests and code reviews MUST verify compliance with this Constitution. Complexity and deviation from these principles MUST be explicitly justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02