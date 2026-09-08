# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controllers depending on Services, Services depending on Repositories).

### II. Test Suite Completeness
All new features or modifications MUST be accompanied by comprehensive unit and integration tests. Existing tests MUST pass. Integration tests MUST cover interactions between different layers and external services.

### III. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be defined in the `model` or respective domain packages. They MUST adhere to JPA/Jakarta Persistence standards and include necessary validation annotations.

### IV. Configuration Separation
Application configuration, including caching (`CacheConfiguration.java`) and web/internationalization settings (`WebConfiguration.java`), MUST be managed in dedicated configuration classes, separate from business logic.

### V. Consistent Naming and Formatting
Code MUST follow established Java conventions and Spring Boot best practices. Variable, method, and class names MUST be descriptive and consistent throughout the codebase.

## Development Workflow

The development workflow for Spring PetClinic will adhere to the following process:

1.  **Feature Development:** New features or bug fixes will be developed in separate branches.
2.  **Unit Testing:** All code changes MUST be covered by unit tests.
3.  **Integration Testing:** Critical integration points, especially those involving data persistence or external interactions, MUST be covered by integration tests. The project includes specific integration tests for MySQL and PostgreSQL.
4.  **Code Review:** All pull requests MUST undergo a thorough code review by at least one other team member. Reviews will focus on adherence to principles, code quality, and test coverage.
5.  **CI/CD Pipeline:** Successful execution of all tests in the CI/CD pipeline is a prerequisite for merging code.

## Governance

This constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this constitution require a formal proposal, discussion, and approval by a majority of the core development team. Any approved amendments MUST include a clear migration plan and be documented with the date of amendment. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08