# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Components MUST NOT cross layer boundaries inappropriately (e.g., a Controller directly accessing a Repository without service intervention).

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot's auto-configuration and conventions. Configuration MUST be managed via `@Configuration` classes and properties files. Dependency Injection MUST be used extensively via `@Autowired` and constructor injection.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external services). Test coverage MUST be maintained at a high level, with specific targets defined in the Quality Gates section.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be defined as Plain Old Java Objects (POJOs) with appropriate JPA annotations for persistence. Business logic related to these entities SHOULD be encapsulated within the domain or service layer, not directly in controllers or repositories.

### V. Observability and Configuration
Application behavior MUST be configurable through external properties. Logging MUST be used effectively for debugging and monitoring, adhering to standard Spring Boot logging practices. Internationalization (i18n) MUST be handled consistently using Spring's i18n mechanisms.

## Development Workflow

### Code Review Process
All code changes MUST undergo a peer review via Pull Requests (PRs). Reviewers MUST verify adherence to the core principles, coding standards, and test coverage requirements. PRs MUST not be merged without at least one approval.

### Quality Gates
- **Unit Test Coverage:** Minimum 80% coverage for all new code.
- **Integration Test Coverage:** All critical workflows and cross-layer interactions MUST be covered.
- **Static Analysis:** Code MUST pass all checks from configured static analysis tools (e.g., SonarQube, Checkstyle).
- **Build Success:** All CI/CD pipelines MUST pass before deployment.

## Governance
This Constitution supersedes all other development practices for the Spring PetClinic project. Amendments to this Constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All code reviews MUST explicitly check for compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28