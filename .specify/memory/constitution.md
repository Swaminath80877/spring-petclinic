# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between unrelated layers are forbidden.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components in isolation, while integration tests MUST validate interactions between components and external systems (e.g., database, external APIs). A minimum of 80% code coverage for critical business logic is required.

### III. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations SHOULD be minimal and clearly documented, adhering to Spring's idiomatic patterns. Avoid unnecessary boilerplate code.

### IV. JPA Repository Best Practices
JPA repositories MUST be used for data access. Custom query methods SHOULD be defined within the repository interfaces, leveraging Spring Data JPA's query derivation or `@Query` annotations. Avoid implementing complex data access logic directly in service or controller layers.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Request and response payloads SHOULD be in JSON format. Input validation MUST be performed at the controller or service layer.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., MySQL, PostgreSQL).

**Containerization**: The project MUST support deployment via Docker, with a `Dockerfile` and Kubernetes manifests provided in the `k8s/` directory.

**Development Environment**: The project MUST be compatible with the `.devcontainer/` configuration for consistent development environments.

## Development Workflow

**Branching Strategy**: Feature development MUST occur on dedicated feature branches. Pull Requests (PRs) MUST be created for merging into the main development branch.

**Code Reviews**: All PRs MUST undergo at least one senior developer review. Reviews MUST verify adherence to this constitution, code quality, test coverage, and architectural integrity.

**Continuous Integration**: Automated builds and tests MUST be executed on every commit to the repository. Successful execution of all tests is a prerequisite for merging code.

**Quality Gates**: Code merged into the main branch MUST pass all automated tests and code review checks. Any introduced regressions will require immediate remediation.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by at least two-thirds of the core development team. Any approved amendments MUST include a migration plan for existing code to ensure compliance. All Pull Requests and code reviews MUST verify compliance with the principles and rules outlined herein.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28