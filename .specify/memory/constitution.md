# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories, Repositories interact with the data source). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Compliance
The project MUST leverage Spring Boot conventions for configuration, auto-configuration, and dependency management. Application startup, component scanning, and bean lifecycle management MUST adhere to standard Spring Boot practices. Externalized configuration MUST be managed via `application.properties` or `application.yml`.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify interactions between components and with external systems (e.g., database). Test coverage MUST be maintained at a high level, with a minimum of 80% for critical business logic.

### IV. JPA Repository Pattern Enforcement
Data access MUST be implemented exclusively through Spring Data JPA repositories. Custom query methods MUST be defined within repository interfaces, and direct SQL manipulation within service or controller layers is forbidden. Entities MUST be annotated with JPA annotations for persistence.

### V. RESTful API Design Principles
Controller endpoints MUST follow RESTful principles for resource representation and manipulation. HTTP methods (GET, POST, PUT, DELETE) MUST be used appropriately. Request and response payloads SHOULD be in JSON format.

## Additional Constraints

### Database Agnosticism
While integration tests may target specific databases (e.g., MySQL, PostgreSQL), the core application logic MUST remain database-agnostic. The use of JPA and Spring Data abstractions facilitates this. Any database-specific features or configurations MUST be isolated and clearly documented.

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` enforces this by checking for untranslated strings and ensuring consistent translation across all supported locales.

## Development Workflow

### Code Review and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage requirements. Automated checks, including static analysis and test execution, MUST pass before a pull request can be merged.

### Versioning and Breaking Changes
The project follows semantic versioning (MAJOR.MINOR.PATCH). Breaking changes MUST be introduced in a new MAJOR version. Any breaking change requires a clear migration plan and communication to stakeholders.

## Governance
This Constitution supersedes all other development practices and guidelines for the Spring PetClinic project. Amendments to this Constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a clear migration plan for existing code and documentation. Compliance with this Constitution is a mandatory requirement for all code merged into the main branch.

**Version**: 1.0.0 | **Ratified**: 2026-08-27 | **Last Amended**: 2026-08-27