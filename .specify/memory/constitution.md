# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controller depending on Service, Service depending on Repository).

### II. Domain Model Integrity
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST be defined in the `org.springframework.samples.petclinic.model` and related sub-packages. These entities MUST be POJOs with appropriate JPA annotations for persistence and Jakarta Bean Validation annotations for data integrity.

### III. Test Coverage Mandate (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., Controllers, Services, Repositories) in isolation. Integration tests MUST verify the interaction between components and with the data store, as evidenced by the presence of `*IntegrationTests.java` files and their usage of test databases.

### IV. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application bootstrapping. This includes using `@SpringBootApplication`, `@Configuration`, `@Controller`, `@Repository`, and leveraging Spring's auto-configuration capabilities where appropriate.

### V. Internationalization (i18n) First
All user-facing strings MUST be externalized into resource bundles and managed via the internationalization framework. The `I18nPropertiesSyncTest.java` explicitly enforces this principle, ensuring no hardcoded strings and complete translations across supported locales.

## Additional Constraints

The project MUST utilize Spring Boot and Spring Data JPA for its core functionality. Database interactions MUST be managed through the defined repository interfaces. The project is designed to be runnable with various database backends, as indicated by the presence of `MySqlIntegrationTests.java` and `PostgresIntegrationTests.java`.

## Development Workflow

All code changes MUST be submitted via Pull Requests. Each Pull Request MUST include sufficient unit and integration tests to cover the changes. Code reviews MUST verify adherence to the core principles outlined in this constitution, focusing on architectural integrity, test coverage, and adherence to Spring Boot conventions.

## Governance

This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. Compliance with this Constitution is a mandatory requirement for all code merged into the main branch. Any deviation must be explicitly documented and justified.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09