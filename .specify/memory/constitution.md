# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries in unintended ways (e.g., a Controller directly calling a Repository).

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot features and conventions. This includes using Spring Data JPA for repositories, Spring MVC for controllers, and standard Spring Boot auto-configuration where applicable. Custom configurations MUST be clearly defined and documented.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing functionality MUST be covered by tests. Tests MUST verify business logic, controller behavior, and repository interactions. Integration tests MUST cover interactions between different layers and external dependencies (e.g., database).

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`) MUST remain as pure Plain Old Java Objects (POJOs) with minimal dependencies, primarily focused on data representation and business logic. JPA annotations and validation constraints are acceptable within the domain model.

### V. Observability and Configuration
Application behavior MUST be configurable through standard Spring Boot mechanisms (e.g., `application.properties`, environment variables). Logging MUST be used effectively to monitor application health and diagnose issues. Internationalization (i18n) MUST be handled via dedicated properties files and Spring's i18n support.

## Development Workflow

The development workflow for the Spring PetClinic project is guided by the following practices:

*   **Feature Branching:** All development MUST occur on feature branches, branched from the main development branch.
*   **Code Reviews:** All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the constitution, code quality, and test coverage.
*   **Automated Testing:** CI pipelines MUST execute all unit and integration tests on every commit. Builds MUST fail if tests do not pass.
*   **Incremental Development:** Features should be developed incrementally, with frequent commits and pull requests.
*   **Database Integration:** Integration tests for database interactions MUST be clearly separated and configured to run against appropriate test databases (e.g., H2, PostgreSQL, MySQL).

## Governance

This constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this constitution require a formal proposal, review by the core development team, and a documented migration plan if existing practices are affected. All pull requests and code reviews MUST verify compliance with the principles outlined herein. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28