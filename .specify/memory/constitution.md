# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Configuration, Domain/Model). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external services (e.g., database). Existing tests MUST be maintained and updated.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be clearly documented and justified.

### IV. Data Persistence Abstraction
All data access operations MUST be performed through the defined Repository interfaces. Direct SQL queries or manual data manipulation outside of these interfaces is prohibited.

### V. RESTful API Design
Controller classes (e.g., `OwnerController.java`, `PetController.java`) MUST adhere to RESTful principles for API design, utilizing appropriate HTTP methods and status codes.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. Database interactions MUST be managed via JPA and Spring Data repositories. Internationalization (i18n) MUST be handled using standard Spring mechanisms, as evidenced by `WebConfiguration.java` and `I18nPropertiesSyncTest.java`.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs). Each PR MUST include sufficient unit and integration tests. Code reviews MUST verify adherence to the core principles and architectural guidelines. Automated CI/CD pipelines MUST enforce test execution and code quality checks before merging.

## Governance

This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. All existing code MUST be migrated to comply with any amendments within a reasonable timeframe, to be defined in the amendment proposal. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-16