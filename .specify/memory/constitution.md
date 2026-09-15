# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations MUST be minimal and clearly justified, documented within their respective configuration classes.

### III. Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST include comprehensive unit and integration tests. Unit tests MUST cover business logic and controller interactions. Integration tests MUST verify data persistence and inter-layer communication. Existing tests MUST be maintained and updated.

### IV. Domain Model Integrity
The domain model (entities like `Owner`, `Pet`, `Vet`, `Visit`) MUST remain pure and free from presentation or persistence concerns. JPA annotations are acceptable within the model layer for persistence mapping.

### V. Observability and Logging
All significant operations, especially those involving data access or external interactions, MUST be logged with appropriate levels (INFO, WARN, ERROR). Structured logging is preferred for easier analysis.

## Additional Constraints

### Technology Stack
The project MUST utilize Spring Boot, Spring Data JPA, Thymeleaf for templating, and JUnit 5 for testing. Database interactions are primarily handled via JPA repositories.

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` enforces this by checking for untranslated strings and ensuring complete translations across all supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and architectural principles.

### Quality Gates
Automated checks, including static analysis, unit tests, and integration tests, MUST pass successfully before code can be merged. Any introduced failures in these checks will block the merge.

## Governance

All code changes MUST comply with this constitution. Amendments to this constitution require a formal proposal, review by the core development team, and a clear migration plan if existing practices are significantly altered. Compliance with this constitution is a mandatory part of all code reviews.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15