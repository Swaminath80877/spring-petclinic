# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries inappropriately (e.g., a Controller directly calling a Repository).

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot's auto-configuration, dependency injection, and common patterns. Configuration MUST be managed via Spring's mechanisms (e.g., `@Configuration`, `@SpringBootApplication`, properties files).

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST target individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database, external APIs). Test coverage MUST be maintained above 80%.

### IV. Data Persistence Abstraction
Data access MUST be performed exclusively through Spring Data repositories. Direct SQL queries or manual JDBC operations are forbidden, except in highly specialized, documented, and approved scenarios.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using structured logging. The application MUST be configurable to provide different log levels for debugging and production monitoring.

## Development Workflow

The standard development workflow for the Spring Petclinic project is as follows:

1.  **Feature Branching**: All new development MUST occur on feature branches, branched from the main development branch (e.g., `main` or `develop`).
2.  **Local Development**: Developers MUST set up their local development environment using the provided `.devcontainer` configuration or equivalent tooling.
3.  **Code Implementation**: Implement the feature or fix the bug, adhering to the Core Principles.
4.  **Unit Testing**: Write comprehensive unit tests for all new code. Ensure existing tests pass.
5.  **Integration Testing**: Write integration tests to verify the interaction of the new code with other components and the data layer. Ensure existing integration tests pass.
6.  **Code Review**: Submit a Pull Request (PR) to the main development branch. The PR MUST include a clear description of the changes, the problem solved, and how to test it. All PRs MUST undergo at least one review by a project maintainer.
7.  **CI/CD Pipeline**: The CI/CD pipeline will automatically run all tests and static analysis checks upon PR creation and updates.
8.  **Merging**: Once the PR is approved and all checks pass, it can be merged into the main development branch.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, discussion within the core development team, and a majority vote for ratification. Any approved amendments MUST include a clear migration plan for existing code and documentation. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31