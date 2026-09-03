# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). New components MUST be placed in the most appropriate layer.

### II. Spring Boot Convention Compliance
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and application bootstrapping. All Spring Boot annotations and auto-configurations MUST be used as intended.

### III. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Existing critical paths MUST have adequate test coverage. Unit tests MUST focus on individual component logic, while integration tests MUST verify interactions between layers and external systems.

### IV. JPA Repository Pattern Enforcement
Data access MUST be exclusively handled through Spring Data JPA repositories. Custom repository methods MUST be clearly defined and adhere to JPA naming conventions.

### V. RESTful API Design Principles
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Request and response payloads SHOULD be structured using appropriate data transfer objects.

## Additional Constraints

Technology Stack:
*   Java (version consistent with Spring Boot)
*   Spring Boot
*   Spring Data JPA
*   H2 Database (for development/testing)
*   PostgreSQL/MySQL (for production environments, as indicated by integration tests)
*   JUnit 5
*   AssertJ
*   Mockito

## Development Workflow

Code Review Process:
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.

Quality Gates:
*   All unit and integration tests MUST pass.
*   Code coverage metrics MUST meet or exceed defined thresholds (e.g., 80% for new code).
*   Static analysis tools (e.g., SonarQube, if integrated) MUST not report critical or major issues.

## Governance

This Constitution supersedes all other development practices for the Spring PetClinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and tests to comply with the changes. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03