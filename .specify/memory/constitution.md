# FlagDesk Constitution

## Core Principles

### I. Web-Based Flag Management

FlagDesk MUST provide a web-based UI for feature-flag management backed by an
OpenFeature-compatible evaluation backend. Flag evaluation MUST remain the responsibility of
the evaluation backend. Shared management workflows MUST expose backend capability limits and
unsupported operations explicitly; evaluation compatibility MUST NOT be treated as a guarantee
of a common management API.

### II. Reference Backend

FlagDesk MUST implement and verify flagd as its initial reference evaluation backend.
Backend-specific management behavior MUST remain behind an explicit integration boundary so
additional backends can be introduced without duplicating shared workflows. Additional backend
implementations MUST be driven by accepted requirements. A backend MUST NOT be advertised as
supported without documented configuration, capability limits, and integration verification.

### III. Standard Persistence

FlagDesk MUST use Entity Framework Core as its standard persistence layer and PostgreSQL as its
default, initially supported database. Persistence concerns MUST remain separate from business
logic. Database flexibility MUST be delivered through supported EF Core providers and
configuration; users MUST NOT need to implement database components to select a supported option.

Each supported database MUST have a maintained provider integration, appropriate schema
migrations, deployment documentation, and integration tests against that database system.
The existence of an EF Core provider alone MUST NOT qualify a database as supported by FlagDesk.
This establishes a concrete implementation while allowing deliberate expansion of database choice.

### IV. Simple Setup

FlagDesk MUST provide a setup script offering a working default configuration, including flagd
and PostgreSQL. Users MUST be able to accept sensible defaults or override individual supported
component choices, including the database, through configuration. Setup MUST validate supported
choices and report invalid or unsupported configuration with actionable errors.
Supported alternatives MUST NOT require users to write integration code. Setup documentation
MUST distinguish configuring existing services from any services the script provisions.

### V. Deployment Documentation

Deployment documentation MUST cover prerequisites, setup, configuration, secrets, startup,
persistence, upgrades, and troubleshooting as those capabilities are introduced. The default
setup MUST have a documented path from a fresh environment to a running application. Supported
alternatives MUST document their configuration and limitations. Changes affecting deployment or
operation MUST update the relevant instructions as part of the same change, so documentation
remains usable for the version being deployed.

### VI. Meaningful Automated Testing

FlagDesk MUST maintain comprehensive unit tests for business rules, edge cases, and relevant
failure paths, plus E2E tests based on expected user-visible behavior. Integration tests MUST
verify supported evaluation backends and database systems, including relevant schema migration
and failure scenarios. Test evidence MUST distinguish real integrations from substitutes;
substitute results MUST NOT be presented as proof of backend or database compatibility.

Tests MUST assert observable outcomes or meaningful contracts. Tests that merely mirror
implementation details, line-by-line source-file regression scripts, and arbitrary coverage
percentage targets MUST NOT be used as quality requirements. Each behavior change MUST include
proportionate verification of its acceptance criteria. Failures affecting the change MUST be
resolved before merge. This provides thorough coverage without maintaining redundant tests.

### VII. Simple, Explicit, Modular Architecture

Modules MUST have clear responsibilities and explicit dependencies. Implementation MUST use
the smallest design that satisfies accepted requirements, with interfaces at meaningful
integration and infrastructure boundaries. New abstractions, dependencies, and infrastructure
MUST have a documented purpose; speculative frameworks and unnecessary layers MUST be avoided.
Extensibility MUST preserve shared business behavior without requiring interchangeable
implementations of every internal component.

## Product Boundaries

FlagDesk manages feature flags; building an evaluation engine is outside the current scope.
PostgreSQL is the required initial database. Subsequent specifications MUST identify additional
databases or components before they are offered as supported setup choices. Database selection
configures a deployment; it does not imply transferring existing data between database engines.
Technology choices beyond the mandated persistence layer and reference defaults MUST be recorded
in implementation plans rather than inferred from examples.

Credentials MUST NOT appear in committed files, logs, or user-visible errors. Deployments with
access control MUST enforce authorization at the trusted operation boundary. Mutations MUST
identify the target flag and relevant backend or environment, and destructive actions MUST
require confirmation. The UI MUST distinguish pending, successful, and failed operations and
MUST NOT claim success without backend confirmation.

Core workflows MUST support keyboard operation, accessible control names, and status indicators
that do not rely on color alone. Loading, empty, error, and unsupported-operation states MUST be
clear; errors MUST provide a recovery action when one is available.

## Development Workflow

Feature specifications MUST state user outcomes, scope, acceptance criteria, and relevant
failure cases. Plans MUST identify module and integration boundaries, technology choices,
verification strategy, and constitution compliance. Review MUST check the implementation against
those criteria and its verification evidence, including relevant deployment documentation.

Exceptions MUST document the affected rule, justification, and scope and receive maintainer
approval. Permanent changes to governing principles MUST be handled through an amendment.
Breaking changes to supported behavior or configuration MUST document their impact and a
migration path.

## Governance

This constitution governs FlagDesk specifications, plans, implementation, and review. Compliance
MUST be checked during planning and before merge. Conflicts with other project guidance MUST be
surfaced and resolved explicitly.

Amendments MUST describe the proposed change, rationale, and impact on existing work and receive
project-maintainer approval. Approved amendments MUST update the version and last-amended date;
the original ratification date MUST remain unchanged. Affected specifications and plans MUST be
assessed when an amendment changes their obligations.

Versioning MUST follow semantic versioning: MAJOR for incompatible principle removals or
redefinitions, MINOR for new principles or materially expanded guidance, and PATCH for wording
clarifications that do not change obligations. This document is the initial adoption at version
1.0.0. The temporary Sync Impact Report MUST be removed before committing the reviewed constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-13 | **Last Amended**: 2026-09-13
