# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services/Repositories, but not vice-versa).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `application.yml`, and Spring Beans MUST be declared using standard annotations (`@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on isolated component logic, while integration tests MUST verify interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and extended as the codebase evolves.

### IV. JPA and Data Persistence Standards
Data access MUST be implemented using Spring Data JPA repositories. Entities MUST be clearly defined with appropriate JPA annotations. Database interactions MUST be encapsulated within repository interfaces, and business logic MUST not directly contain SQL queries.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. Request and response payloads SHOULD be designed for clarity and efficiency, leveraging JSON as the primary format.

## Development Workflow

The development workflow for the Spring Petclinic project is as follows:

1.  **Feature/Bug Identification**: A new feature request or bug is identified.
2.  **Task Breakdown**: The task is broken down into smaller, manageable units of work.
3.  **Branching**: A new feature branch is created from the main development branch (e.g., `develop`).
4.  **Development**:
    *   Code is written following the core principles outlined above.
    *   Unit tests are written and pass.
    *   Integration tests are written and pass.
    *   Code is formatted and adheres to project coding standards.
5.  **Code Review**: A Pull Request (PR) is created against the `develop` branch. The PR MUST include a clear description of changes, rationale, and any relevant context. At least one other developer MUST review the code for adherence to principles, correctness, and maintainability.
6.  **Testing**: Automated tests (unit and integration) MUST pass in the CI pipeline. Manual testing may be performed as needed.
7.  **Merging**: Once approved and all checks pass, the PR is merged into the `develop` branch.
8.  **Release**: Periodically, the `develop` branch is merged into the `main` branch for a release.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic project. Amendments to this Constitution require a formal proposal, a documented rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31