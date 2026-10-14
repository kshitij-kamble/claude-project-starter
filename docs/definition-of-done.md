# Definition of done

`/backlog done <id>` and `/arc reconcile` check the universal gates below **plus**
the item's own section. An unmet gate blocks `done`.

## Universal gates

- [ ] Every acceptance criterion for the item is met (`docs/acceptance-criteria.md`).
- [ ] Tests for the change exist and pass; build, lint and typecheck are clean.
- [ ] Linked arc's `reconcile.md` is filled in; punted work is in the backlog.
<!-- setup:domain-gates — /setup adds project-specific gates here. -->

<!-- Per-item sections go below this line: ## <id> — <slug>  (`<tag>`) -->
