---
description: Wrap up the day — walk through what's done and unfinished, then write handoff.md
---

Leave a complete note for tomorrow-morning-me (read by `/daily-sync`). Capture both code state (committed, pushed, in progress) AND what's in my head (blockers, what didn't work, what's next).

Walk through this interactively. Don't write the file until we've gone through everything. For most sections, figure things out from git/MCP first, then ask me to confirm or add. Wait for my answer before moving to the next section.

# 1. Handle uncommitted work

Run `git status` and `git diff` silently. Ignore .DS_Store.

- If uncommitted changes exist: tell me what they are and ask "Want me to commit these? If so, what's the commit message?"
- If yes, stage relevant files, commit, and push.
- If there are unpushed commits: ask "Want me to push?"
- Then continue.

# 2. Load context

Run silently:
- `git status`, `git diff`, `git diff --staged`, `git stash list`
- `git log origin/<branch>..<branch> --oneline` — unpushed commits
- `git log --oneline --since=midnight` — today's commits
- Read `handoff.md` if it exists — use it as baseline for blockers and next steps
- Look up my open PRs via GitHub MCP, including CI status and review state

# 3. Walk through each section

**a. Shipped today**
Summarize today's commits and merged/closed PRs. Ask: "Anything else to note?"

**b. In progress**
List uncommitted, unpushed, or stashed work by file/feature. Ask: "Is anything here actually done, or all still WIP?"

**c. Open PRs**
Report each open PR with CI status and review state (from MCP). Ask: "Anything to add?"

**d. What's broken or didn't work**
Check for signals: reverted commits, WIP stashes, CI failures. Present what you found. Ask: "Anything else broken or that didn't work today?"

**e. Blockers**
For each blocker already in the previous handoff, ask: "Still blocking?" (group into one question). New blockers found from context today — just add, don't ask.

**f. Next steps**
Suggest 2-3 based on in-progress work, open PRs, and blockers. Ask: "Does this look right? Anything to add or change?"

**g. Notes for future-me**
Ask: "Anything you'd be annoyed about forgetting?" Don't infer or add anything yourself.

# 4. Write handoff.md

Overwrite `handoff.md` in the repo root:

```
# Handoff — <YYYY-MM-DD>

**Branch:** <current branch>

## Shipped today
- <commits/PRs done and pushed>

## In progress
- <uncommitted/unpushed/stashed — specific file/feature and state>

## Open PRs
- #<num> <title> — <CI status + review state>

## What's broken / didn't work
- <from git signals + my input>

## Blockers
- <confirmed old + any new>

## Next steps for tomorrow
1. <first>
2. <second>
3. ...

## Notes for future-me
- <only what I told you>
```

Use "—" for empty sections. Don't pad.

# 5. Confirm

```
Handoff written to handoff.md.

Tomorrow's sync picks up:
- Branch: <branch>
- <one-line summary of top in-progress item>
- <one-line summary of top blocker, if any>

Have a good evening.
```
