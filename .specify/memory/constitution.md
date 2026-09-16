# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Configuration, Domain/Model). Code MUST NOT cross layer boundaries in an unintended direction (e.g., Controllers directly calling Repositories without a Service layer, which is absent here).

### II. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, and integration tests MUST validate interactions between layers and with external dependencies (e.g., databases). Existing tests MUST be maintained and extended.

### III. Explicit Dependency Management
Dependencies between components MUST be explicitly declared through Spring's dependency injection mechanisms. Avoid implicit dependencies or direct instantiation of components outside their defined layers.

### IV. Data Persistence Abstraction
Data access MUST be exclusively handled through the defined Repository interfaces. Business logic SHOULD NOT contain direct SQL queries or low-level database interaction code.

### V. Observability and Configuration
Application behavior MUST be configurable through external properties (e.g., `application.properties`). Logging MUST be used to provide visibility into application flow and potential issues.

## Additional Constraints

**Technology Stack**: The project MUST utilize Spring Boot, JPA for data persistence, and Thymeleaf for server-side templating.
**Database**: The application is designed to work with relational databases, with explicit support for MySQL and PostgreSQL demonstrated through integration tests.
**Internationalization (i18n)**: All user-facing strings MUST be internationalized and managed through properties files. Tests MUST ensure complete translation coverage.

## Development Workflow

**Code Reviews**: All code changes MUST undergo a thorough code review process. Reviewers MUST verify adherence to the core principles, architectural layers, and testing requirements.
**Branching Strategy**: A Gitflow-like branching strategy is recommended, with clear separation of features, releases, and hotfixes.
**Continuous Integration**: Automated builds and tests MUST be executed on every commit to the main development branches.

## Governance

This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers. All existing code MUST be migrated to comply with any amendments within a defined timeframe. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-16 | **Last Amended**: 2026-09-16