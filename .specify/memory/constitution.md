# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every new feature or modification MUST strictly adhere to the established layered architecture: Controller, Repository, Configuration, and Domain/Model. Direct dependencies between non-adjacent layers are prohibited (e.g., Controller cannot directly depend on Repository).

### II. Test Coverage Mandate
All new code MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (controllers, services, models) in isolation. Integration tests MUST verify interactions between layers and with external dependencies (e.g., database, external APIs). Existing tests MUST be maintained and updated to reflect any changes.

### III. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project needs beyond standard Spring Boot defaults.

### IV. JPA Repository Best Practices
All data access MUST be performed through Spring Data JPA repositories. Custom query methods MUST be clearly defined within repository interfaces. Avoid direct SQL queries within service or controller layers.

### V. Observability and Logging
Application behavior and potential issues MUST be observable through structured logging. All significant events, errors, and request flows MUST be logged with appropriate levels (INFO, WARN, ERROR).

## Additional Constraints

Spring PetClinic is a web application built on the Spring Framework. The following constraints are in place:

*   **Technology Stack**: The primary technology stack includes Java, Spring Boot, Spring Data JPA, Thymeleaf for templating, and Maven for build management.
*   **Database**: The application is designed to work with relational databases. Integration tests are provided for MySQL and PostgreSQL, indicating flexibility but requiring careful consideration for production deployments.
*   **Internationalization (i18n)**: The project actively supports internationalization. All user-facing strings MUST be externalized into resource bundles, and the `I18nPropertiesSyncTest.java` MUST pass to ensure consistency across languages.
*   **Containerization**: Kubernetes manifests (`k8s/`) are present, indicating an intention for containerized deployments. Development environments should leverage `.devcontainer/` for consistent setup.

## Development Workflow

*   **Branching Strategy**: Feature development MUST occur on separate branches. All changes MUST be submitted via Pull Requests.
*   **Code Reviews**: All Pull Requests MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to the constitution.
*   **Testing Gates**: CI/CD pipelines MUST enforce that all unit and integration tests pass before merging.
*   **Deployment**: Deployments to production environments MUST be preceded by a successful staging deployment and a final approval from the lead architect or designated reviewer.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST explicitly verify compliance with this constitution. Complexity introduced into the codebase MUST be clearly justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03