# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controller depending on Service, Service depending on Repository).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `@Configuration` classes. Dependency Injection MUST be used for component wiring.

### III. Test-Driven Development (TDD) & Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and with external systems (e.g., database). Existing tests MUST be maintained and extended.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. Direct SQL queries within business logic are forbidden. Entity classes MUST adhere to JPA specifications.

### V. Internationalization (i18n) Compliance
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Additional Constraints

### Technology Stack
The project MUST utilize Java as the primary programming language, with Spring Boot as the core framework. JPA for data persistence, and JUnit 5 for testing are mandatory.

### Database Agnosticism
While integration tests may target specific databases (e.g., MySQL, PostgreSQL), the core application logic MUST remain agnostic to the underlying database technology.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to these principles, code quality, and test coverage.

### Quality Gates
Automated checks, including static analysis, unit tests, and integration tests, MUST pass before code can be merged. Continuous Integration (CI) pipelines MUST enforce these gates.

## Governance
This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments must include a migration plan if necessary. All pull requests and code reviews must verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02