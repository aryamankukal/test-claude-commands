---
description: Sync work state at start of day — git, PRs, and standup notes
---

Run the steps below, then output a clean morning summary.

# 1. Sync git

Run these in order, narrating what each one returned:

- `git fetch origin` — pull down all remote state without touching your working tree
- `git status` — if there are uncommitted changes, stash them with `git stash` before continuing; restore with `git stash pop` after syncing
- Ask: "Which branch do you want to work on today?" — don't assume it's the same as yesterday
- Check out that branch if not already on it
- `git log HEAD..origin/<branch> --oneline` — check if a teammate pushed to your branch while you were away; if yes, run `git pull --rebase origin <branch>` to bring their changes in before rebasing onto main
- `git rebase origin/main` — sync your branch with latest main
- `git log --oneline -10` — confirm the state looks right

If the rebase produces conflicts, stop and flag them clearly. Don't try to resolve them automatically — list the conflicting files and tell me to resolve them.

# 2. Recent activity

- `git log --oneline -10` — last 10 commits on the current branch
- `git diff HEAD~5` — what's changed in the last 5 commits (skim, don't dump the whole diff in the output)

Briefly summarize what's been worked on recently in 2-3 lines.

# 3. My open PRs

- `gh pr list --state open --author @me` — my own open PRs
- For each, gather:
  - `gh pr view <number> --comments` — any new review comments since I last looked
  - `gh pr checks <number>` — CI status (flag any failures)
  - Mergeable state — any conflicts with main

Surface anything actionable: failing CI, unread review comments, merge conflicts. Don't tell me what to do about it — just flag the state.

# 4. Context from yesterday

- If `handoff.md` exists, read it and summarize where I left off, my blockers, and what I planned to do next
- If `lessons.md` exists, scan recent entries (last few) and surface anything relevant to what I'm currently working on

If neither file exists, just say so — don't fabricate context.

# 5. Standup notes

Generate standup bullets based on yesterday's git activity (commits since yesterday across all my branches, PRs opened/merged, review activity) plus `handoff.md` next steps for today if present. If nothing imn handoff then ask me.

Format: 1-3 bullets per section, max. Each bullet should be specific (mention the actual feature, ticket, or PR — not "worked on stuff"). Skip a section entirely with "—" if nothing fits. Reference ticket/PR numbers where relevant.

```
**Yesterday:**
- <specific thing shipped/worked on, with PR # or ticket ref>

**Today:**
- <specific thing planned, from handoff next steps or current branch>

**Blockers:**
- <specific blocker from handoff.md, or "none">
```

# Output format

Format the final output exactly like this, no filler:

```
## Morning sync

**Branch:** <current branch>
**Status:** <clean / N files modified / rebase conflicts>

**Recent work:**
- <2-3 line summary of recent commits>

**My open PRs:**
- #<num> <title> — <state: CI failing / N new comments / merge conflict / clean>

**Where I left off (from handoff.md):**
- <summary, or "no handoff.md found">

---

### Standup

**Yesterday:**
- <bullet>

**Today:**
- <bullet>

**Blockers:**
- <bullet, or "none">
```

If a section has nothing to report, write "—" rather than omitting it. Don't pad with commentary.