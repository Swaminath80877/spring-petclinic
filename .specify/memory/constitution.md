# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controller depending on Service, Service depending on Repository).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database, external APIs). Test coverage metrics MUST be maintained and reviewed.

### IV. JPA Repository Pattern Enforcement
All data access operations MUST be performed through Spring Data JPA repositories. Custom repository implementations are discouraged unless absolutely necessary and must be clearly documented.

### V. RESTful API Design Principles
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. Data transfer objects (DTOs) SHOULD be used for API payloads where appropriate to decouple the API from internal domain models.

## Additional Constraints

**Technology Stack**: The project MUST primarily utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., MySQL, PostgreSQL, H2).

**Containerization**: The project MUST support containerization via Docker, as evidenced by the presence of `k8s/` and `.devcontainer/` directories.

**Internationalization (i18n)**: All user-facing strings MUST be internationalized and managed through properties files, as enforced by `I18nPropertiesSyncTest.java`.

## Development Workflow

**Branching Strategy**: A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for ongoing development, and feature branches for new work.

**Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**CI/CD**: Automated builds, testing, and deployments SHOULD be integrated into a Continuous Integration and Continuous Deployment pipeline.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST verify compliance with this Constitution. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02