# Constitution

Starting principles from the Dark / gray Software Factory. Each application owns its copy: amend it with `/speckit-constitution` in design mode, and record why in an ADR.

## Core Principles

### I. The specification is the contract
`specs/` and `uat/features/` define the product; code is replaceable. Every requirement is testable, and every acceptance scenario in a feature spec is also written as Gherkin in `uat/features/`.

### II. Test-first (non-negotiable)
Write a failing test, make it pass, refactor. Unit, component and integration tests sit next to the code; acceptance scenarios run with `make uat`. Tests are never weakened, skipped or deleted to get green.

### III. Modules with high cohesion and low coupling
Code follows `docs/architecture/modules.json`: one responsibility per module, imports only through a module's public API and only along declared dependencies, no cycles. `make check` enforces this; changes to the module map need an ADR.

### IV. Decisions are recorded
Significant choices are ADRs in `docs/architecture/adr/`, naming the requirement they serve and the options rejected. Accepted ADRs are superseded, never edited.

### V. Small, verifiable increments
Each task is a vertical slice that leaves `make check` green. Work happens on branches and reaches `main` only through a reviewed pull request.

## Quality gates

`make check` (types, lint, tests, module rules, duplication) must pass before any task is done. The code review agent reviews every PR; the human approves changes to specs, acceptance scenarios, architecture and the factory.

## Governance

This constitution guides `/speckit-plan`, `/speckit-analyze` and `/speckit-implement`. Where it conflicts with the factory rules in `.dsf/CLAUDE.dsf.md`, the factory rules win until the human decides otherwise.

**Version**: 1.0.0 | **Ratified**: on app creation | **Last Amended**: on app creation
