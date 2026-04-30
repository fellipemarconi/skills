---
name: pr-review-gh
description: Generates PR review comments using code-review-pro (and optionally another review skill) and posts them via gh. Use when user asks to review a PR, add review comments, or post feedback to a GitHub PR.
---

# PR Review via gh

## Quick start

When asked to review a PR, follow this flow:

1) Ask which PR to review (URL or number).
2) Fetch PR data and diff with gh.
3) Run a thorough review using code-review-pro (and a second review skill if requested).
4) Post comments via gh: general comment or inline comments with file+line.

## Workflow

1. Ask the user which PR to review.
   - Accept PR URL or number. If in a repo, default to current repo.
   - If user says "use both skills", run both review passes and merge findings.

2. Fetch PR context via gh:
   - `gh pr view <pr> --json title,body,files,commits,baseRefName,headRefName,author,url`
   - `gh pr diff <pr>`
   - If needed, `gh pr view <pr> --json reviewRequests,labels`

3. Analyze the diff:
   - Use code-review-pro to identify security, perf, correctness, and maintainability issues.
   - If using a second review skill, run it and merge results.
   - Prioritize issues; keep comments actionable with suggested fixes.

4. Post review comments:
   - General comment: `gh pr comment <pr> --body "..."`
   - Inline comment(s) with line mapping (prefer inline when possible):
     `gh pr review <pr> --comment -f <file> -L <line> -b "..."`

5. Summarize back to the user:
   - Provide the PR URL and a concise list of key findings.
   - Note any critical/high severity issues first.

## Notes

- Always ask for the PR before starting.
- Avoid posting if the user wants a dry run; in that case, summarize only.
- Use plain language and short, actionable comments.
