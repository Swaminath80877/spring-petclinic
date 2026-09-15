# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories, Repositories interact with the data source). Direct dependencies between unrelated layers are forbidden.

### II. Spring Boot Convention and Idiomatic Usage
The project MUST leverage Spring Boot conventions and idiomatic patterns. This includes utilizing Spring Data JPA for repository implementations, Spring MVC for web controllers, and standard Spring Boot auto-configuration mechanisms. Custom configurations MUST be clearly defined and documented.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify the interactions between components and with external systems (e.g., database). Test coverage MUST be maintained at a high level, with a minimum of 80% for critical business logic.

### IV. Data Integrity and Validation
All data entities MUST enforce validation rules as defined by Jakarta Bean Validation annotations. Input validation MUST be performed at the controller layer and within domain models to ensure data integrity before persistence.

### V. Observability and Debuggability
The application MUST be instrumented for observability. This includes structured logging for key events and errors. Integration tests MUST cover scenarios involving database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) to ensure data persistence and retrieval are functioning correctly.

## Development Workflow

The development workflow for the Spring Petclinic project will adhere to the following process:

1.  **Feature Development:** Developers will create new features or address bugs by following the principles outlined in this constitution. This includes writing comprehensive tests *before* or *concurrently* with implementation.
2.  **Code Review:** All code changes MUST be submitted as Pull Requests (PRs). PRs MUST be reviewed by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage requirements.
3.  **Testing:** Automated tests (unit and integration) MUST pass on the CI/CD pipeline before a PR can be merged. Specific integration tests, such as database interaction tests (`MySqlIntegrationTests`, `PostgresIntegrationTests`), are crucial for verifying data persistence.
4.  **Deployment:** Deployments will be managed through automated pipelines. Successful completion of all tests and a successful code review are prerequisites for deployment.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic project. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST always be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15