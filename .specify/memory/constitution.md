# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Test Coverage Mandate
All new features and bug fixes MUST include comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external APIs). Existing tests MUST be maintained and updated.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and component scanning. Auto-configuration SHOULD be leveraged where appropriate, and custom configurations MUST be clearly documented.

### IV. Data Integrity and Validation
All data persistence operations MUST be validated to ensure data integrity. Input validation MUST be performed at the controller or service layer, utilizing Jakarta Bean Validation constraints where applicable.

### V. Observability and Logging
Application behavior MUST be observable through structured logging. Critical events, errors, and significant state changes MUST be logged with sufficient detail to facilitate debugging and monitoring.

## Additional Constraints

The Spring Petclinic application is a web application built on the Spring Framework. It utilizes JPA for data persistence and Thymeleaf for templating. The project is designed to demonstrate core Spring Boot features and best practices.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs). Each PR MUST include:
- A clear description of the changes.
- Associated unit and integration tests.
- Successful execution of all automated checks (linting, testing, build).
- A review by at least one other team member.

Code reviews MUST focus on adherence to these principles, code quality, maintainability, and correctness.

## Governance
This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-08 | **Last Amended**: 2026-09-08