# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories directly).

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database). Existing tests MUST NOT be broken.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application startup. Auto-configuration MUST be leveraged where appropriate, and custom configurations MUST be clearly documented.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by the Repository layer. Domain entities MUST be designed to be independent of the persistence mechanism, utilizing standard JPA annotations.

### V. Observability and Logging
Application behavior MUST be observable through structured logging. Critical operations and potential error conditions MUST be logged with appropriate severity levels.

## Additional Constraints

The project is built upon the Spring Framework and Spring Boot. It utilizes JPA for data persistence and Thymeleaf for templating. The primary database is H2, with support for integration testing against PostgreSQL and MySQL.

## Development Workflow

All code changes MUST be submitted via Pull Requests. Each Pull Request MUST undergo a thorough code review by at least one other team member. Automated checks, including compilation, unit tests, and integration tests, MUST pass before a Pull Request can be merged.

## Governance
This constitution supersedes all other development practices for the Spring Petclinic project. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02