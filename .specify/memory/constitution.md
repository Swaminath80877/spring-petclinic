# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every new feature or modification MUST strictly adhere to the established layered architecture: Controller, Repository, Configuration, and Domain/Model. Components within a layer MUST interact only with adjacent layers (e.g., Controllers with Services, Services with Repositories). Direct cross-layer communication is forbidden.

### II. Test Coverage Mandate
All new code MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., controllers, services, models), and integration tests MUST verify interactions between layers and with external dependencies (e.g., database, external APIs). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Compliance
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and application bootstrapping. Custom configurations MUST be clearly documented and justified. Use of Spring Data JPA for data access is mandated.

### IV. RESTful API Design
All external-facing endpoints MUST follow RESTful principles. Controllers MUST be stateless, use appropriate HTTP methods (GET, POST, PUT, DELETE), and return standard HTTP status codes. Request and response bodies SHOULD be in JSON format.

### V. Observability and Logging
All significant operations, errors, and state changes MUST be logged using structured logging. The application MUST expose metrics for monitoring key performance indicators and system health.

## Development Workflow

The development workflow is designed to ensure code quality, maintainability, and adherence to the project's principles.

*   **Branching Strategy**: Feature development MUST occur on dedicated feature branches. All changes MUST be merged into the main branch via Pull Requests.
*   **Code Reviews**: All Pull Requests MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to the constitution.
*   **Automated Checks**: CI pipelines MUST automatically run all unit and integration tests, perform static code analysis, and check for constitutional compliance before allowing a merge.
*   **Database Migrations**: Database schema changes MUST be managed using a versioned migration tool (e.g., Flyway, Liquibase). Migrations MUST be tested thoroughly.
*   **Containerization**: Development and deployment environments SHOULD utilize containerization (e.g., Docker) to ensure consistency. Kubernetes manifests are provided for deployment.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this constitution require:

1.  A formal proposal detailing the proposed changes and their justification.
2.  A thorough review and approval by at least two-thirds of the core development team.
3.  A documented migration plan for any existing code that may be affected by the amendment.
4.  All Pull Requests and code reviews MUST verify compliance with this constitution.
5.  Any deviation from these principles MUST be explicitly documented and justified in the Pull Request.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15