# Workflow layer: GitHub Spec Kit

Skill pack: [GitHub Spec Kit](https://github.com/github/spec-kit), installed into this repo as `.claude/skills/speckit-*` and `.specify/` (by `specify init --here --integration claude`). The constitution is `.specify/memory/constitution.md`.

| Factory step (docs/dsf/workflows.md) | Mode | Spec Kit skill | Output goes to |
| --- | --- | --- | --- |
| Principles, once per app | design | `/speckit-constitution` | `.specify/memory/constitution.md` |
| PRD | design | interview the human, then write `specs/prd.md` as the list of features and product-level requirements | `specs/prd.md` |
| Feature spec | design | `/speckit-specify`, then `/speckit-clarify` | `specs/NNN-feature/spec.md` |
| UAT interview | design | `dsf-uat-interview`: start from the spec's acceptance scenarios and turn them into Gherkin | `uat/features/` |
| Architecture | design | `dsf-architect` for the module map and ADRs, then `/speckit-plan` per feature, which must follow `modules.json` and the ADRs | `docs/architecture/`, `specs/NNN-feature/plan.md` |
| Plan into tasks | design | `/speckit-tasks`, then `/speckit-analyze` (and `/speckit-checklist` when useful); with the `github` task backend also `/speckit-taskstoissues` | `specs/NNN-feature/tasks.md` |
| Build | build | `/speckit-implement`, then `/speckit-converge` until it reports converged | `src/`, tests, `uat/steps/` |
| Bugfix | build | the factory bugfix workflow (failing test first); the optional Spec Kit `bug` extension if installed | failing test first, then the fix |
| Review | build | `dsf-code-reviewer` | PR comments |
| Exploration | design | `/speckit-specify` a spike spec, prototype on a `spike/` branch | `docs/architecture/proposals/` |
| Factory | factory | `dsf-factory-improve`; upgrade Spec Kit with `specify` in the parent dsf-speckit repo | `.specify/`, `.claude/skills/speckit-*` |

Where Spec Kit and this factory differ, the factory wins:

- Work on a branch per feature (`feature/NNN-name`), created before `/speckit-specify`; that branch is the PR branch.
- Build mode may only tick off `specs/*/tasks.md`; the spec and plan stay read-only there (`.dsf/modes.workflow.json`).
- `/speckit-plan` may propose a project structure. Use the one in `docs/architecture/modules.json`; propose an ADR if it does not fit.
