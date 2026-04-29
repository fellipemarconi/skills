---
name: pull-request
description: Create a Pull Request following project standards — branch rules, file limit, template, and gh CLI
---

Create a Pull Request for the current branch. Follow every rule below exactly.

**Context:** $ARGUMENTS
(Auto-detect from branch name.)

---

## Step 1 — Pre-flight checks

Run these commands and evaluate the results before doing anything else:

```bash
git branch --show-current
git diff main...HEAD --stat
git log main...HEAD --oneline
git status
```

**File count check:**
Count the files changed. If the count exceeds **30 files**, stop and tell the user:
> "This PR contains X files, which exceeds the 30-file limit. Please split it into smaller PRs grouped by scope before continuing."

Do not proceed until the user confirms a split or reduces scope.

**Branch name check:**
The branch must follow the project naming convention: `{type}/{case-description}`

Valid types: `feat`, `feature`, `fix`, `refactor`, `chore`, `docs`, `test`

Examples: `feat/create-report`, `fix/header-layout`

If the branch name doesn't follow this pattern, warn the user but do not block.

**Push check:**
Check if the current branch has been pushed to remote:
```bash
git status -sb
```
If not pushed yet, push it:
```bash
git push -u origin $(git branch --show-current)
```

---

## Step 2 — Analyze the diff

Read the changed files as needed to understand what the PR actually does. Identify:
- PR type (Feature / Bug Fix / Optimization / Refactor / Docs / Tests) — can be multiple
- What changed technically (which layers, which entities, what behavior)
- Whether web files changed (needed for UI checklist)
- Whether translation files changed
- Whether test files are in the diff

---

## What type of PR is this? (check all applicable)

- [ ] Feature
- [ ] Bug Fix
- [ ] Optimization
- [ ] Refactor
- [ ] Documentation
- [ ] Tests
- [ ] Chore (build, ci, deps, etc)

## Description

{2–5 sentences. Explain what changed, why it was needed, and how it was implemented.
Mention affected modules, services, or components if applicable.}

## Related Issues

{Link issue/ticket if exists, or "N/A"}

## Changes Made

- {List key changes}
- {e.g. Added X}
- {Refactored Y}
- {Removed Z}

## How to Test

{Step-by-step to validate}

1. {Step 1}
2. {Step 2}
3. {Expected result}

## Checklist

- [ ] Code follows project standards
- [ ] Self-review done
- [ ] No unnecessary console logs / debug code
- [ ] Documentation updated (if needed)
- [ ] No breaking changes OR properly documented

## Tests

- [ ] Added tests
- [ ] Updated tests
- [ ] No tests needed (explain): {reason}

## Deployment Notes (optional)

{Migrations, env vars, feature flags, rollout steps}

## Additional Notes (optional)

{Anything reviewers should know}

## Step 4 — Determine the base branch

Check if a feature base branch exists (e.g. `use-case/header-layout` for `feature/header-layout-*`).
If no clear base branch is identifiable, default to `main`.

---

## Step 5 — Create the PR

Use `gh pr create` with the filled body via HEREDOC. Never use `--body-file` with the unfilled template.

```bash
gh pr create \
  --base {base-branch} \
  --head $(git branch --show-current) \
  --title "{type}: {concise description under 70 chars}" \
  --body "$(cat <<'EOF'
{filled template content here}
EOF
)"
```

Title format: `{type}: {description}` — e.g. `feat: add rotation report endpoint`, `fix: header layout`

---

## Step 6 — Confirm

After creation, output:
- The PR URL
- File count
- Base branch used
- A one-line summary of what was included

---

## Hard rules

- Never create PRs through the GitHub UI — always use `gh pr create`
- Never use `--body-file */pull-request/PULL_REQUEST_TEMPLATE.md` with the blank template
- Never exceed 30 files without user confirmation
- Never modify the template structure — only fill the fields
- The branch must not contain unrelated changes
- Do not mix feature + unrelated fixes + refactor in the same PR
