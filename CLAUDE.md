# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

> **Not set up yet?** If any `{{…}}` placeholder is still in this file, run
> `/setup` before anything else.

**Stack: {{STACK}}.** Record each hard-to-reverse stack choice as an ADR
(`/decision new`) before building on it, then fill in *Commands* below.

## Start of session

Read `docs/STATE.md`: active arcs, open backlog, recent decisions and activity.
It's regenerated automatically; never hand-edit it.

## Commands

_To be filled in once the stack is chosen (install, dev server, test, lint, typecheck, build)._

## Domain

Project-specific lenses the workflow skills (`/arc`, `/backlog`) apply. Keep
each to a line or two.

- **Who's affected beyond the acting user:** {{DOMAIN_STAKEHOLDERS}}
- **Prior art to study:** {{DOMAIN_PRIOR_ART}}
- **Typical design axes:** {{DOMAIN_AXES}}
- **Prep artifacts that usually apply:** {{DOMAIN_PREP}}
- **Boundaries that bite:** {{DOMAIN_RISKS}}

## Workflow

| Need | Use | Lives in |
|---|---|---|
| Capture an idea, bug, debt, question | `/backlog` | `docs/backlog.md` (mirrored to GitHub Issues when enabled) |
| Drive non-trivial work | `/arc` | `docs/phases/<date>-<topic>/` |
| Record a hard-to-reverse choice | `/decision` | `docs/adr/` |
| Standing "always/never" guidance | `/rules` | `docs/rules/` |
| What's in flight | `/state` | `docs/STATE.md`, `docs/activity.md` |

- Acceptance criteria: `docs/acceptance-criteria.md`. Definition of done: `docs/definition-of-done.md`.
- Skip `/arc` for small work (typos, one-line fixes, small refactors).
- GitHub Issues mirror: **{{ISSUES_MIRROR}}** (`on` or `off`; see `.claude/skills/backlog/SKILL.md`).

## Conventions

- Branches: `<name>/<type>/<topic>`, e.g. `{{BRANCH_PREFIX}}/feat/<topic>`. PRs target `main`.
- Commits for a backlog item reference its issue (`… (#N)`); the finishing PR says `Closes #N`.
- {{REPO_VISIBILITY_NOTE}}
