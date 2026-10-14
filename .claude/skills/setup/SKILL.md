---
name: setup
description: One-time bootstrap for a project created from this starter — fills the {{…}} placeholders in CLAUDE.md, writes the project README, adds domain gates to the definition of done, resets the docs and creates GitHub labels. Use for /setup, or suggest it when CLAUDE.md still contains {{…}} placeholders.
---

# /setup

Turns the starter into *this* project. Run it once, right after creating the
repo. It's safe to re-run: it only touches what's still a placeholder unless
the user asks to redo something.

## 1. Check where we are

- `grep -rn '{{' CLAUDE.md docs/` — if nothing is left, setup has been done;
  say so and ask what the user wants to change instead.
- Note `git remote get-url origin` (may be absent) and whether `gh auth status`
  succeeds. Both decide the Issues-mirror default.

## 2. Ask

Ask in one round with `AskUserQuestion` where options make sense, plain
questions otherwise. Infer what you can (e.g. the repo name from `origin`) and
offer it as the default. Don't invent domain answers — propose a draft from
the description and let the user correct it.

| Placeholder | Ask for |
|---|---|
| `{{PROJECT_NAME}}` | Project name. |
| `{{PROJECT_DESCRIPTION}}` | One or two sentences: what it is and who it's for. |
| `{{STACK}}` | The stack if chosen, else `not chosen yet` (leave the ADR reminder). For each piece already chosen, offer to write an ADR with `/decision new` afterwards. |
| `{{DOMAIN_STAKEHOLDERS}}` | Who besides the acting user sees the effect of a change (other collaborators, admins, API consumers, downstream jobs…). `none` is a valid answer. |
| `{{DOMAIN_PRIOR_ART}}` | Products, libraries or papers worth studying in brainstorm. |
| `{{DOMAIN_AXES}}` | The recurring design trade-offs in this domain. |
| `{{DOMAIN_PREP}}` | Prep artifacts specific to this domain, beyond the generic list in `/arc`. |
| `{{DOMAIN_RISKS}}` | Boundaries that usually bite (concurrency, offline, scale, permissions, migrations…). |
| `{{ISSUES_MIRROR}}` | `on` or `off`. Default `on` only if there's a GitHub `origin` and `gh` is authenticated. |
| `{{BRANCH_PREFIX}}` | Short name for branch prefixes (default: lowercase first name from `git config user.name`, or ask). |
| `{{REPO_VISIBILITY_NOTE}}` | Public → `The GitHub repo is public. Put nothing secret in issues, commits or docs.` Private → `The GitHub repo is private, but treat issues and docs as shareable: no secrets.` |

Also ask:

- **Domain gates** for `docs/definition-of-done.md`: 0–5 checks every change
  must clear in this project. Propose some from the answers above.
- **Rule scopes:** keep the defaults in `docs/rules/README.md`
  (`global · ui · api · data · infra · process`) or replace them.
- **License:** keep MIT (update the copyright holder and year), change it, or
  remove it.

## 3. Write

1. Replace every placeholder in `CLAUDE.md`. Delete the *Not set up yet?*
   blockquote.
2. Rewrite `README.md` for the project: name, description, status ("early
   setup" + links to `docs/STATE.md` and `docs/adr/`), *Getting started*
   (placeholder until the stack exists), *Project docs* links, license. Drop
   everything about the starter itself except one line at the bottom:
   `Bootstrapped from claude-project-starter.`
3. Insert the domain gates as `- [ ]` lines in place of the
   `<!-- setup:domain-gates … -->` comment in `docs/definition-of-done.md`.
4. Update scopes in `docs/rules/README.md` if changed, and `LICENSE`.
5. If `.gitignore` doesn't fit the stack (it ships Node-flavoured), adjust it.
6. Reset the logs: `docs/backlog.md` keeps only its header; then
   `node .claude/scripts/refresh-state.mjs log "Project bootstrapped from claude-project-starter"`.

## 4. GitHub (only if the mirror is `on`)

Show the user the commands first — labels are visible on the remote repo.

```sh
gh label create feature   --color 1D76DB --force
gh label create bug       --color D73A4A --force
gh label create tech-debt --color FBCA04 --force
gh label create spike     --color C5DEF5 --force
gh label create question  --color D876E3 --force
gh label create arc       --color 0E8A16 --force
```

A failure here doesn't block setup; report it and move on.

## 5. Finish

- `grep -rn '{{' CLAUDE.md README.md docs/` must come back empty.
- Show a short summary of what changed and suggest a first commit (don't
  commit unless asked).
- Ask whether to delete this skill (`.claude/skills/setup/`) now that it's done.
  Keeping it is harmless.
- Suggest next steps: ADRs for any stack choices, then `/backlog add`.

## Example: a filled-in Domain section

From a real-time collaborative whiteboard:

```md
- **Who's affected beyond the acting user:** other people on the same board, live.
- **Prior art to study:** Excalidraw, tldraw, Miro, Figma.
- **Typical design axes:** rendering (Canvas 2D / SVG / WebGL); sync model (CRDT / OT / server-authoritative / last-write-wins); persisted vs ephemeral state (presence, cursors).
- **Prep artifacts that usually apply:** board model with schema version + migration; per-user undo/redo for each operation; sync message shapes and conflict rule; tool state machines and hit-testing; a two-client test for anything that syncs.
- **Boundaries that bite:** concurrent edits, reconnect/offline, large boards, undo across users.
```

…with domain gates such as "verified with two clients at once, and after a
reload" and "existing boards still load after a format change".
