# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers, except for the explicit dependency on the Model layer.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where applicable. Custom configurations MUST be clearly documented and justified. Dependencies between components MUST be managed primarily through Spring's dependency injection.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual component logic, while integration tests MUST verify interactions between layers and external systems (e.g., database). Test coverage MUST be maintained above 80%.

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces MUST abstract database operations, and entities MUST be mapped using JPA annotations. Direct SQL queries within business logic are prohibited.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using a structured logging format. The application MUST provide mechanisms for monitoring key metrics and tracing requests, especially for controller and service layers.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Technology Stack**: Java 17+, Spring Boot 3.x, Spring Data JPA, Thymeleaf for templating.
*   **Database**: Primarily H2 for development and testing, with support for PostgreSQL and MySQL via Testcontainers for integration testing.
*   **Internationalization (i18n)**: All user-facing strings MUST be internationalized and managed through properties files. Tests MUST ensure consistency across all supported locales.
*   **Containerization**: The application MUST be containerizable, with Kubernetes manifests provided in the `k8s/` directory.

## Development Workflow

*   **Branching Strategy**: Feature development MUST occur on dedicated feature branches. Pull Requests (PRs) MUST be created from feature branches to the main development branch.
*   **Code Reviews**: All PRs MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.
*   **CI/CD**: A Continuous Integration pipeline MUST be established to automatically build, test, and analyze code quality upon every commit to the repository. Deployment to staging and production environments MUST be triggered manually after successful CI and QA sign-off.

## Governance

This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All Pull Requests and code reviews MUST verify compliance with the principles and constraints outlined herein.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02