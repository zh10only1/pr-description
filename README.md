# pr-description

A [Claude Code](https://claude.com/claude-code) skill that makes every pull request look the same, in any repo and whatever branch it targets: short, accurate, and organised by what changed rather than by commit.

## What you get

**Title:** `type(scope): what it does, in plain words`, for example `feat(export): download a workspace as CSV`. A release PR (one branch into another) uses `Release: <what ships>`.

**Body:** always the same four short sections:

```markdown
## Summary
One or two sentences: what this PR does and why.

## Behaviour
- What changed, in terms of what users or callers see
- Contract changes and anything a reviewer could trip over

## Deploy
Migrations, scripts, env vars, deploy order, or "Nothing to run."

## Tests
What was actually run, and the real results.
```

**Never in a PR:**

- a list of commits (GitHub's Commits tab already shows them)
- a file-by-file walkthrough
- claims the diff doesn't back up
- a "Generated with Claude Code" footer or Co-Authored-By lines

Claude uses the skill on its own whenever it opens or edits a PR with `gh`. It also uses it when you ask for a title and description to paste yourself, for example "give me the PR title and description".

## Install

### As a plugin (recommended)

Inside Claude Code:

```
/plugin marketplace add zh10only1/pr-description
/plugin install pr-description@pr-description
```

Update later with `/plugin marketplace update pr-description`.

### As a plain skill file

For every project (user level):

```sh
mkdir -p ~/.claude/skills/pr-description
curl -fsSL https://raw.githubusercontent.com/zh10only1/pr-description/main/skills/pr-description/SKILL.md \
  -o ~/.claude/skills/pr-description/SKILL.md
```

For one repo only, so the whole team gets it, put the file at `.claude/skills/pr-description/SKILL.md` in that repo and commit it.

Pick one method. If the skill is installed both ways, Claude sees it twice.

## Use

Nothing to do. Open PRs as usual ("open a PR for this", "write the PR description") and Claude follows the skill. To call it directly, run `/pr-description`.

To change the rules, edit [`skills/pr-description/SKILL.md`](skills/pr-description/SKILL.md), or your installed copy.

## License

[MIT](LICENSE)
