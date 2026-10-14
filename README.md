# Claude Project Starter

A project template for working with [Claude Code](https://claude.com/claude-code).
It contains no app code. It gives you a lightweight workflow so you can go from
"new repo" to "building" in a few minutes:

| Skill | What it does |
|---|---|
| `/setup` | One-time: names the project, fills in its domain, resets the docs, creates GitHub labels. |
| `/backlog` | Ideas, bugs, debt and questions in `docs/backlog.md`, with acceptance criteria and a definition of done. Optionally mirrored to GitHub Issues. |
| `/arc` | Drives non-trivial work through six phases: ideate → brainstorm → prep → align → implement → reconcile. |
| `/decision` | Architecture Decision Records in `docs/adr/`. |
| `/rules` | Standing "always/never" guidance in `docs/rules/`, injected by hooks when a prompt mentions a rule's keywords. |
| `/state` | `docs/STATE.md`, a generated snapshot of what's in flight. A hook refreshes it at the end of every turn. |

## Quick start

1. On GitHub, click **Use this template** → **Create a new repository**, or
   fork the repo, or just copy the files.
2. Clone it and open it in Claude Code: `claude`
3. Run `/setup` and answer the questions. It fills in `CLAUDE.md`, rewrites
   this README for your project, and seeds `docs/`.
4. Start working: `/backlog add feature …`, then `/arc start <topic> from <id>`.

## Requirements

- [Claude Code](https://docs.claude.com/en/docs/claude-code)
- Node.js 18+ (the hooks run two small `.mjs` scripts and have no dependencies)
- Optional: the [GitHub CLI](https://cli.github.com/) (`gh auth login`), for the Issues mirror

## Layout

```
CLAUDE.md                     project instructions; /setup fills the placeholders
.claude/settings.json         hooks: rule injection + STATE.md refresh
.claude/scripts/              rules-match.mjs, refresh-state.mjs
.claude/skills/               setup, backlog, arc, decision, rules, state
docs/backlog.md               work items
docs/acceptance-criteria.md   per-item "User can…" outcomes
docs/definition-of-done.md    universal gates + per-item checklists
docs/phases/                  one folder per arc
docs/adr/                     decisions
docs/rules/                   rules
docs/STATE.md, activity.md    snapshot and event log
```

## Customising

All of it is plain Markdown and two short scripts, so edit anything you like.
The usual places to start:

- **`CLAUDE.md` → Domain**: the lenses `/arc` and `/backlog` apply (who else is
  affected, prior art, design axes, risks).
- **`docs/definition-of-done.md`**: your project's universal gates.
- **`docs/rules/README.md`**: the `scope` values rules can use.

## License

[MIT](LICENSE)
