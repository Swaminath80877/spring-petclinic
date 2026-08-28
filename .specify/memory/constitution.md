# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers are prohibited.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external systems (e.g., database, external APIs). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application bootstrapping. Custom configurations MUST be clearly documented and justified. Use of Spring Data JPA for data access is mandatory, and repository interfaces MUST extend appropriate Spring Data interfaces.

### IV. RESTful API Design
Controllers MUST expose RESTful APIs following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer objects (DTOs) SHOULD be used where appropriate to decouple the API from internal domain models.

### V. Observability and Logging
All significant application events, errors, and request flows MUST be logged using structured logging. The application MUST provide mechanisms for monitoring key performance indicators and application health.

## Additional Constraints

The following constraints are critical for the maintainability and stability of the Spring PetClinic project:

*   **Technology Stack**: The project MUST be built using Java and Spring Boot. Dependencies MUST be managed via Maven.
*   **Database**: The primary data store is a relational database. Integration tests MUST support at least one common RDBMS (e.g., PostgreSQL, MySQL).
*   **Internationalization (i18n)**: All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` enforces this.
*   **Security**: While not explicitly a security-focused application, basic security principles like input validation and avoiding sensitive data exposure in logs MUST be followed.

## Development Workflow

The following workflow and quality gates are established for the Spring PetClinic project:

*   **Branching Strategy**: Feature development MUST occur on separate branches, merging back to the main branch via Pull Requests.
*   **Code Reviews**: All Pull Requests MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.
*   **Automated Checks**: CI pipelines MUST include static analysis, unit tests, and integration tests. Builds MUST fail if any of these checks do not pass.
*   **Deployment**: Deployments to production environments require explicit approval from the lead architect or designated release manager.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring PetClinic repository. Amendments to this constitution require:

1.  A formal proposal detailing the proposed changes and their rationale.
2.  A review period of at least one week for community feedback.
3.  Approval by at least two-thirds of the core development team.
4.  A documented migration plan if the amendment introduces breaking changes or requires significant refactoring.

All Pull Requests and code reviews MUST verify compliance with the principles and rules outlined in this constitution. Any deviation MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28