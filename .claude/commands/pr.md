---
description: Write a PR description from the current branch's diff
---

Run these to gather context:
- `git diff main...HEAD` — see what changed
- `git log main..HEAD --oneline` — see commit messages
- `git diff main...HEAD --stat` — see which files/types changed (use this to decide if it's a UI change)

Write a PR description following the structure below. The description is a permanent part of version control history and may be read by hundreds of people over the years — future engineers searching for it should understand *why* the change was made, since source code already shows *what*. Take it seriously even for small PRs.

# Title

- **Short summary of what is being done**, written as a complete sentence in the imperative ("Truncate long agent names in Kanban card" — not "Truncating..." or "Fix bug").
- Must stand alone — someone skimming `git log` should understand what the PR did without opening it.
- Bad: "Fix bug", "Fix build", "Add patch", "Phase 1". These are real bad descriptions — don't write them.

# Body sections (in this order)

## Why
The motivation and reasoning. Briefly set the context (what part of the system this is, how it currently behaves), then explain what problem, gap, or goal triggered this change. Why this approach over alternatives? Any decisions or tradeoffs that aren't visible in the diff?

This is the most important section — source code shows *what*, this shows *why*. Don't just point at a ticket; expand on it.

## Changes
Short bullets listing the concrete file-level changes. Which files, which functions, what was added/removed/modified. Lets reviewers scan what to expect in the diff.

## Verification
**Only include this section if the PR changes UI or user-visible behavior.** Skip entirely for backend-only / refactor / test-only changes.

When included:
- "Before:" — leave a placeholder for me to drop in a screenshot/recording
- "After:" — leave a placeholder for me to drop in a screenshot/recording
- Bullet list of behaviors verified manually (e.g. "Long names truncate with ellipsis", "Hover shows full name via tooltip", "Short names render unchanged")
- One line on test results: "Existing tests pass (N passed)"

## Risks
1-3 sentences. What could break? What should reviewers pay extra attention to? "Low risk — only adds standard utility classes, no behavioral changes" is a valid answer for small PRs. Don't pad.

# Footer

End with the ticket link on its own line:
- `Fixes #N` or `Closes JIRA-N` if there's a ticket in commit messages
- Ask me if there isn't one — don't invent one. I'll tell you.

# Asking me questions

Before writing Why, check if the diff and commits give enough context. If they don't — especially for the motivation, root cause, or design decisions behind the change — ask me what's missing before drafting. Don't guess and don't ask about things already obvious from the code.

# Style rules

- Reviewers skim. No filler. No AI-flavored phrases like "comprehensive", "robust", "leverages", "facilitates", "seamlessly".
- After drafting, re-read the title alone — does it stand on its own in `git log`? If not, rewrite it.
- Do not use em dashes (—) or en dashes (–). Use a hyphen or rewrite the sentence.

# Opening the PR

After drafting the description, push the branch if not already pushed, then run:

```
gh pr create --title "<title>" --body "<description>" --web
```

The `--web` flag opens the GitHub PR editor in the browser with the title and description pre-filled. The user can review and submit from there.