# Spring PetClinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., Controllers, Services, Models) in isolation. Integration tests MUST verify interactions between components and with external systems (e.g., database, external APIs). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Compliance
The project MUST adhere to Spring Boot conventions for configuration, dependency injection, and application bootstrapping. Auto-configuration SHOULD be leveraged where appropriate, and custom configurations MUST be clearly documented and placed in dedicated configuration classes.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by components within the Repository layer. Domain entities MUST be designed to be POJOs with appropriate JPA annotations. Data access logic MUST be separated from business logic.

### V. RESTful API Design
Controller layer components MUST implement RESTful APIs following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Request and response payloads SHOULD be in JSON format.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. External dependencies MUST be managed via Maven.

**Database**: The primary database is relational (e.g., MySQL, PostgreSQL). Integration tests MUST validate functionality against at least one supported relational database.

**Containerization**: The project MUST be containerizable using Docker, with a `Dockerfile` and potentially Kubernetes manifests provided in the `k8s/` directory.

## Development Workflow

**Branching Strategy**: Feature development MUST occur on dedicated feature branches. Pull Requests (PRs) MUST be created from feature branches to the main development branch.

**Code Reviews**: All PRs MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

**CI/CD**: Continuous Integration (CI) MUST be configured to automatically build, test, and analyze code on every commit to feature branches and on merges to the main development branch. Continuous Deployment (CD) SHOULD be implemented for stable releases.

**Issue Tracking**: All development tasks, bugs, and feature requests MUST be tracked using an issue tracking system.

## Governance

This constitution supersedes all other development practices and guidelines for the Spring PetClinic project. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All Pull Requests and code reviews MUST explicitly verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-27 | **Last Amended**: 2026-08-27