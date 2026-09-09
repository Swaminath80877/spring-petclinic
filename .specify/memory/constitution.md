# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between components in the same layer are permissible only if they represent a clear, cohesive unit of functionality.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST verify individual component logic in isolation, while integration tests MUST validate interactions between components and external systems (e.g., database, external APIs). A minimum of 80% code coverage by automated tests is required for all production code.

### III. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST be the central focus of the application's design. Business logic MUST be encapsulated within these domain objects or their associated services. Data access MUST be abstracted through repository interfaces, ensuring that the domain model is not tightly coupled to the persistence mechanism.

### IV. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer between client and server MUST utilize JSON or other standard web formats. Endpoints MUST be designed for discoverability and statelessness.

### V. Observability and Logging
All significant application events, including errors, warnings, and key business transactions, MUST be logged using structured logging. Application health and performance metrics SHOULD be exposed to facilitate monitoring and debugging.

## Additional Constraints

**Technology Stack**: The project MUST primarily utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. External dependencies MUST be managed via Maven.

**Database**: The application is designed to work with relational databases. Integration tests SHOULD cover at least two different database systems (e.g., MySQL, PostgreSQL) to ensure portability.

**Containerization**: The project SHOULD support deployment via Docker, with a `Dockerfile` and Kubernetes manifests provided in the `k8s/` directory.

## Development Workflow

**Branching Strategy**: Feature development MUST occur on dedicated feature branches, branched from the `main` branch. All changes MUST be submitted for review via Pull Requests (PRs) targeting the `main` branch.

**Code Reviews**: All PRs MUST undergo at least one thorough code review by a team member familiar with the project. Reviews MUST verify adherence to the constitution, code quality, and test coverage.

**Continuous Integration**: A CI pipeline MUST be configured to automatically build, test, and analyze the code on every commit to a feature branch and on PR creation.

**Quality Gates**: The CI pipeline MUST enforce quality gates, including passing all automated tests, achieving the minimum code coverage, and passing static code analysis checks. Merging to `main` is blocked if any quality gate fails.

## Governance

This Constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this Constitution MUST be proposed via a formal PR, clearly documenting the proposed changes, the rationale, and a migration plan if necessary. Amendments require approval from at least two senior development team members. All Pull Requests and code reviews MUST verify compliance with the principles outlined in this document. Complexity introduced into the codebase MUST be justified and aligned with the core principles.

**Version**: 1.0.0 | **Ratified**: 2026-09-09 | **Last Amended**: 2026-09-09