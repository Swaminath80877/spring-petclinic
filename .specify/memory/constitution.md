# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal, well-documented, and only introduced when explicit deviation from convention is required for specific functionality or performance needs.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), while integration tests MUST verify interactions between components and with external systems (e.g., database, external APIs). Test coverage metrics MUST be maintained and reviewed.

### IV. Domain Model Integrity
Domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be the single source of truth for business data. They MUST adhere to JPA entity standards and include necessary validation annotations. Changes to the domain model MUST be carefully considered for their impact on the entire application.

### V. Observability and Debuggability
The application MUST be designed with observability in mind. This includes structured logging, clear error handling, and the ability to trace requests through different layers. The `CrashController` serves as an example of explicit error simulation for testing observability.

## Development Workflow

### Code Review and Compliance
All pull requests MUST undergo a thorough code review process. Reviewers MUST verify adherence to the core principles, architectural layers, and testing requirements outlined in this constitution. Automated checks (e.g., static analysis, test execution) MUST pass before a pull request can be merged.

### Versioning and Breaking Changes
The application follows semantic versioning. Any changes that introduce backward-incompatible modifications to public APIs or core functionalities MUST be clearly documented and justified. Breaking changes require a higher level of review and approval.

### Technology Stack
The primary technology stack is Java with Spring Boot. Dependencies MUST be managed via Maven. Use of external libraries MUST be justified and reviewed for compatibility and security.

## Governance
This constitution supersedes all other development practices and guidelines for the Spring Petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. All approved amendments MUST include a plan for migrating existing code and tests to comply with the new rules. Compliance with this constitution is a mandatory requirement for all contributions.

**Version**: 1.0.0 | **Ratified**: 2026-08-28 | **Last Amended**: 2026-08-28