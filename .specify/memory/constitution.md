# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controllers depending on Services, Services depending on Repositories).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project needs beyond standard Spring Boot defaults.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database, external APIs). Test coverage metrics MUST be maintained and reviewed.

### IV. JPA Repository Abstraction
Direct database interaction MUST be exclusively handled through Spring Data JPA repositories. Custom SQL queries or direct JDBC calls are forbidden unless absolutely necessary and approved through a formal change request.

### V. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be POJOs with clear responsibilities. They MUST adhere to JPA standards for persistence and validation annotations (e.g., `jakarta.validation`).

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., MySQL, PostgreSQL, H2).

**Internationalization (i18n)**: All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across all supported locales.

**Containerization**: The project MUST support containerization via Docker, as evidenced by the presence of `k8s/` and `.devcontainer/` directories.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

**Code Reviews**: All Pull Requests (PRs) MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to this constitution.

**CI/CD**: A Continuous Integration and Continuous Deployment pipeline MUST be in place, automatically building, testing, and deploying the application. Quality gates MUST be defined within the pipeline to prevent the promotion of non-compliant or untested code.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02