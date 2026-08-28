# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST be strictly unidirectional, flowing downwards (e.g., Controller depends on Service, Service depends on Repository).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `application.yml`, and Spring Beans MUST be declared using standard annotations (`@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify interactions between components and with external systems (e.g., database). The existing test suite structure (e.g., `OwnerControllerTests`, `ClinicServiceTests`, `MySqlIntegrationTests`) MUST be maintained and expanded.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST be POJOs with clear responsibilities. Persistence logic MUST be encapsulated within Repository interfaces, and domain entities MUST NOT contain direct database access code. Validation MUST be applied using Jakarta Bean Validation annotations.

### V. Observability and Configuration
Application behavior MUST be configurable through external properties. Logging MUST be used judiciously to provide insights into application flow and potential issues. Internationalization (i18n) MUST be handled via properties files, as evidenced by `I18nPropertiesSyncTest`.

## Development Workflow

### Code Reviews and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage. Automated checks, including static analysis and test execution, MUST pass before merging.

### Dependency Management
Dependencies MUST be managed using Maven (as indicated by `pom.xml` structure). New dependencies MUST be carefully evaluated for necessity and potential impact on the project.

### Database Integration
The application supports multiple database integrations (MySQL, PostgreSQL). Integration tests MUST be written to cover the specific database being used in the testing environment. Database schema changes MUST be managed through appropriate migration strategies.

## Governance
This constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a clear migration plan if they impact existing code or processes. Compliance with this constitution is a mandatory requirement for all code merged into the main branch.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28