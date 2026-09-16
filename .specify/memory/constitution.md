# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Configuration, Domain/Model). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controllers interacting with Services, Services interacting with Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST include comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., Controllers, Services, Models), and integration tests MUST verify interactions between layers and with external systems (e.g., database, external APIs). Existing tests MUST be maintained and updated to reflect code changes.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and only implemented when standard Spring Boot features are insufficient.

### IV. Data Persistence Abstraction
All data access operations MUST be performed through the defined Repository interfaces (`OwnerRepository`, `PetTypeRepository`, `VetRepository`). Direct SQL queries or manual JDBC operations within service or controller layers are strictly prohibited.

### V. Observability and Logging
Application behavior and potential issues MUST be observable through structured logging. All significant events, errors, and state changes MUST be logged using appropriate log levels. The `spring-boot-starter-logging` dependency MUST be used for consistent logging practices.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Technology Stack**: The primary technology stack is Java with Spring Boot, JPA (Hibernate), and Thymeleaf for templating.
*   **Database**: The application is designed to work with relational databases, with explicit support for MySQL and PostgreSQL demonstrated through integration tests.
*   **Containerization**: Kubernetes manifests (`k8s/`) are provided, indicating an intent for containerized deployment. Development environments should leverage `.devcontainer/` for consistency.
*   **Internationalization (i18n)**: All user-facing strings MUST be internationalized and managed through properties files, as enforced by `I18nPropertiesSyncTest.java`.

## Development Workflow

*   **Branching Strategy**: Feature development MUST occur on dedicated feature branches. All code changes MUST be submitted via Pull Requests (PRs).
*   **Code Reviews**: All PRs MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviewers MUST verify adherence to this constitution.
*   **CI/CD**: Continuous Integration (CI) pipelines MUST automatically build, test, and analyze code quality on every commit to main branches. Continuous Deployment (CD) pipelines MAY be implemented for automated deployments to staging or production environments after successful CI and manual approval.
*   **Testing Gates**: Successful execution of all unit and integration tests is a mandatory gate for merging any code.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this Constitution require:
1.  A formal proposal detailing the proposed changes and their justification.
2.  A review and approval process by at least two senior members of the development team.
3.  A clear migration plan if the amendment necessitates changes to existing code or infrastructure.
4.  Documentation of the amendment in the repository's history.

All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution. Any deviation from these principles MUST be explicitly justified and approved by the governance body.

**Version**: 1.0.0 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-16