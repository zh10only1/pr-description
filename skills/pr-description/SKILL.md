---
name: pr-description
description: Write the title and description of a pull request so that every PR looks the same in any repo, whatever branch it targets. Use whenever you open or edit a PR (gh pr create, gh pr edit), or when the user asks for PR content to paste themselves ("give me the PR title and description", "write the PR"). Covers the title format, the four-section body (Summary, Behaviour, Deploy, Tests) and what never goes in a PR.
---

# PR title and description

Each PR is short, accurate and laid out the same way. A reviewer should learn what changed,
what to watch for and what to run, without opening the code.

## Before writing

Read the real diff against the base branch (`git diff <base>...HEAD`), not just the commit
messages or your memory of the work. Describe only what is in the diff. Leave out work
that was planned but not done. Mention a reverted experiment only if it leaves something
behind.

## Title

- A feature or fix: `type(scope): what it does, in plain words`. The type is `feat`, `fix`,
  `refactor`, `chore`, `docs` and so on, and the scope is the area touched.
  - `feat(meals): one request per meal over a date range`
  - `fix(availability): drop-offs let the helper pick a time`
- A release or promotion PR (one branch into another): `Release: <plain summary of what ships>`.
- Describe the behaviour, not the code: "users can reorder sessions", not "add sortIndex column".

## Body

Always use these four sections, in this order. Keep each one short.

```markdown
## Summary
One or two sentences: what this PR does and why.

## Behaviour
- What changed, in terms of what users or callers see. One bullet for each change.
- Contract changes: API shapes, payload fields, removed options, new errors.
- Anything a reviewer could trip over: visible side effects, things left untouched on purpose.

## Deploy
- Migrations to run, and on which environments.
- Scripts to run (dry run first if they write data), new env vars or config, and merge or
  deploy order between repos.
- If there's nothing: "Nothing to run."

## Tests
- What you actually ran and the result: test counts, typecheck, lint, build, manual or
  browser checks.
- State failures honestly ("2 failing, both already failing on the base branch").
```

For a release PR, the Behaviour section lists what ships, grouped by feature, with one line each.

## Rules

- **Accurate.** Every claim must be true of the diff. When unsure, check before you write.
- **To the point.** No filler, no repeating the title, no restating the obvious. Make every
  bullet short; when one grows long, split it or cut it.
- **Never list commits.** No "Commits" section and no commit-by-commit walkthrough. GitHub's
  Commits tab already shows them.
- **No file-by-file list.** Organise by behaviour and impact, not by file.
- **Write about behaviour, not implementation.** Name a function or file only when a
  reviewer needs it to find something.
- **No attribution.** No "Generated with Claude Code", no AI footer, no Co-Authored-By lines.
- **Don't write Deploy steps nobody needs.** "Nothing to run." is enough. Never make up a step.

## Delivering it

- When you open the PR yourself, pass the body through a file so the formatting survives:
  `gh pr create --title "..." --body-file <file>`. Do the same with `gh pr edit`.
- When the user asks for the content only (for example, someone else will open the PR),
  reply with the title on one line and the body in a single markdown block, ready to paste.

## Example

Title: `feat(export): download a workspace as CSV`

```markdown
## Summary
Admins can now export a workspace's records as a CSV file from the workspace settings page.

## Behaviour
- New "Export CSV" button in Settings → Data, shown only to admins.
- `GET /workspaces/:id/export` streams the file; non-admins get 403.
- Archived records are left out; the button's tooltip says so.

## Deploy
Nothing to run.

## Tests
- 14 new export tests pass; full suite 812/812.
- Typecheck and lint clean.
- Exported a 5,000-row workspace in the browser and opened it in a spreadsheet.
```
