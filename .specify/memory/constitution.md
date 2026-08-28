# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers are prohibited.

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot's auto-configuration and conventions. Configuration MUST be managed via `@Configuration` classes and Spring Boot properties. Dependency Injection MUST be used extensively via `@Autowired` and constructor injection.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database). Test coverage MUST be maintained at a high level, with specific targets defined in the Quality Gates section.

### IV. JPA and Data Access Standards
Data access MUST be implemented using Spring Data JPA repositories. Entities MUST be annotated with Jakarta Persistence annotations. All database interactions MUST be performed through these repositories, ensuring consistency and testability.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. Request and response payloads SHOULD be designed for clarity and efficiency, leveraging JSON as the primary format.

## Development Workflow

### Code Review and Quality Gates
All code changes MUST undergo a mandatory code review process. Pull requests will only be merged after approval from at least one other team member. Automated checks, including static analysis and test execution, MUST pass before merging. Specific quality gates include:
*   Minimum 80% unit test coverage.
*   All integration tests passing.
*   No critical or major static analysis warnings.

### Versioning and Breaking Changes
The project will follow Semantic Versioning (MAJOR.MINOR.PATCH). Breaking changes MUST be clearly documented and require a MAJOR version increment. Any breaking change MUST include a migration plan if applicable.

## Governance
This constitution supersedes all other development practices for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. All pull requests and code reviews MUST verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28