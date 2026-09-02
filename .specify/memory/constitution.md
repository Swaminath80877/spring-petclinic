# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `application.yml`, and Spring Beans MUST be declared using standard annotations (`@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external APIs). Tests MUST cover positive, negative, and edge cases.

### IV. Data Persistence Abstraction
Data access MUST be managed exclusively through Spring Data JPA repositories. Direct SQL queries or manual JDBC operations are forbidden. Entities MUST be clearly defined with appropriate JPA annotations.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using a structured logging framework (e.g., SLF4j with Logback). Log messages MUST be informative and aid in debugging and monitoring.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., H2, MySQL, PostgreSQL).

**Internationalization (i18n)**: All user-facing strings MUST be externalized and managed through properties files. The `I18nPropertiesSyncTest` MUST pass to ensure all strings are translated across all supported locales.

**Containerization**: The project MUST support containerization via Docker, as evidenced by the presence of a `.devcontainer` directory. Kubernetes manifests are also present, indicating deployment considerations.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is implied, with `main` for production-ready code and `develop` for ongoing development. Feature branches should be created off `develop`.

**Code Reviews**: All Pull Requests (PRs) MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**CI/CD Integration**: The project is set up for CI/CD, with tests and builds expected to be automated. Integration tests, including database-specific ones (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`), are crucial for ensuring compatibility.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02