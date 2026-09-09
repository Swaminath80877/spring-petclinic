# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every new feature or modification MUST adhere to the established layered architecture: Controller, Repository, Service (implied but not explicitly shown as a separate layer in the analysis, but common in Spring Boot apps), Domain/Model, and Configuration. Direct dependencies MUST only flow downwards (e.g., Controllers depend on Services, Services depend on Repositories, Repositories depend on Domain/Model).

### II. Test Coverage Mandate
All new code MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (controllers, services, models) in isolation. Integration tests MUST verify the interaction between layers and with external dependencies (e.g., database). Existing tests MUST be updated to reflect any changes.

### III. Spring Boot Conventions Adherence
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed through properties files (`application.properties` or `application.yml`) and Java-based configuration classes (`@Configuration`). Dependency injection MUST be managed by Spring's IoC container.

### IV. RESTful API Design
Controllers MUST expose RESTful APIs following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer MUST primarily use JSON. APIs should be designed for discoverability and statelessness where appropriate.

### V. Database Interaction via Repositories
All data persistence and retrieval operations MUST be handled exclusively through Spring Data JPA repositories. Direct SQL queries or manual JDBC operations are forbidden. Repository interfaces MUST be clearly defined and leverage Spring Data's capabilities for common operations.

## Additional Constraints

**Technology Stack**: The project MUST be built using Java and Spring Boot. Dependencies MUST be managed via Maven. The primary database is assumed to be relational (e.g., MySQL, PostgreSQL, H2), with integration tests demonstrating compatibility.

**Security**: While not explicitly detailed in the provided files, standard Spring Security practices should be considered for future enhancements, ensuring secure access to application endpoints.

**Internationalization (i18n)**: The project demonstrates a commitment to internationalization, as evidenced by `I18nPropertiesSyncTest.java`. All user-facing strings MUST be externalized into resource bundles and managed through this mechanism.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the constitution, code quality, test coverage, and architectural principles.

**Continuous Integration**: Automated builds and tests MUST be executed on every commit to feature branches and upon merging into `develop`. Key quality gates include passing all tests and meeting defined code coverage thresholds.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09