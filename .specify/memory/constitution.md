# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries in unintended ways (e.g., a Controller directly calling a Repository).

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot conventions and idioms for configuration, dependency injection, and application bootstrapping. This includes utilizing annotations like `@SpringBootApplication`, `@Controller`, `@Repository`, and standard Spring Data JPA practices.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and significant modifications MUST be accompanied by unit and integration tests. Unit tests MUST verify individual component logic, while integration tests MUST validate interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and expanded as needed.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`) MUST remain as plain Java objects with minimal dependencies, primarily focused on representing the core entities and their relationships. Persistence concerns SHOULD be abstracted away by the repository layer.

### V. Internationalization (i18n) Compliance
All user-facing strings MUST be internationalized using Spring's i18n mechanisms. The `I18nPropertiesSyncTest` MUST pass, ensuring all translatable strings are present in all language property files.

## Development Workflow

The development workflow for Spring Petclinic will adhere to the following process:

1.  **Feature Development**: Developers will create new features or modify existing ones following the established layered architecture and core principles.
2.  **Unit Testing**: Comprehensive unit tests MUST be written for all new or modified code.
3.  **Integration Testing**: Integration tests MUST be written to cover interactions between components and with the database. Specific focus will be placed on testing controller-repository interactions and service layer logic.
4.  **Code Review**: All code changes MUST undergo a thorough code review by at least one other team member. Reviews will verify adherence to principles, code quality, and test coverage.
5.  **CI/CD Pipeline**: Automated builds, tests, and deployments will be managed through a CI/CD pipeline. All tests MUST pass for a build to be considered successful.
6.  **Database Integration**: The project supports multiple database integrations (MySQL, PostgreSQL) as evidenced by integration tests. Developers should ensure their changes are compatible with these configurations.

## Governance

This Constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this Constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a clear migration plan if existing practices need to be altered. All Pull Requests and code reviews MUST verify compliance with the principles outlined herein. Complexity in code MUST be justified and align with the project's goals.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31