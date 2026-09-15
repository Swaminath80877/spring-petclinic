# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories, Repositories interact with the data source). Direct dependencies between unrelated layers (e.g., Controller directly accessing Repository) are forbidden.

### II. Spring Boot Conventions and Best Practices
The project MUST leverage Spring Boot features and follow its established conventions. This includes, but is not limited to, using Spring Data JPA for data access, Spring MVC for web controllers, and standard Spring Boot auto-configuration mechanisms. Custom configurations MUST be clearly defined and documented.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by appropriate unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify the interaction between different layers and external systems (e.g., database). Test coverage MUST be maintained at a high level, with specific targets defined in the Quality Gates section.

### IV. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST accurately represent the business concepts. Relationships between entities MUST be clearly defined and managed through appropriate JPA annotations. Business logic SHOULD be encapsulated within the domain or service layers, not within controllers or repositories.

### V. Observability and Configuration Management
Application behavior MUST be observable through structured logging and appropriate metrics. Configuration MUST be externalized using Spring Boot's configuration properties mechanism, allowing for environment-specific adjustments without code changes.

## Development Workflow

### Code Review and Quality Gates
All code changes MUST undergo a mandatory code review process. Pull requests will only be merged after approval from at least one other team member. Automated checks, including static analysis and test execution, MUST pass before a pull request can be merged. Specific quality gates include:
*   **Test Coverage:** Minimum 80% unit test coverage for new code.
*   **Static Analysis:** No critical or major violations reported by the chosen static analysis tool (e.g., SonarQube, Checkstyle).
*   **Integration Test Pass Rate:** 100% of integration tests must pass.

### Versioning and Breaking Changes
The project follows Semantic Versioning (MAJOR.MINOR.PATCH). Breaking changes MUST be clearly communicated and require a MAJOR version increment. Backward-incompatible changes to public APIs or data schemas MUST be avoided where possible. If unavoidable, a migration strategy and deprecation period MUST be defined.

## Governance
This Constitution supersedes all other development practices for the Spring Petclinic project. Amendments to this Constitution require a formal proposal, a documented rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-15 | **Last Amended**: 2026-09-15