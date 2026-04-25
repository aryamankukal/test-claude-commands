---
description: Wrap up the day — walk through what's done and unfinished, then write handoff.md
---

The point: leave a complete note for tomorrow-morning-me (read by `/daily-sync`) so I never lose context between sessions. The handoff should capture both the code state (committed, pushed, in progress) AND the stuff in my head (blockers, things that didn't work, what I want to tackle next).

Walk through this interactively with me. Don't write the file until we've gone through everything together.

# 1. Handle uncommitted work

Run `git status` and `git diff` silently. If there are uncommitted changes or untracked files (ignoring .DS_Store):

- Tell me what's uncommitted and ask: "Want me to commit these before we wrap up? If so, what should the commit message be?"
- If yes, stage the relevant files and commit with the message I give. Then push.
- If there are already-committed but unpushed commits, ask: "You have unpushed commits — want me to push now?"
- Once any commits/pushes are done (or skipped), continue.

# 2. Look at the state of my code

Run these silently to gather context:
- `git status` — what's uncommitted/staged
- `git diff` — what's in the working tree
- `git diff --staged` — what's staged but not committed
- `git stash list` — anything stashed
- `git log origin/HEAD..HEAD --oneline` — commits I made locally that aren't pushed yet
- `git log --oneline --since=midnight` — commits I made today
- `git branch --show-current` — current branch
- `gh pr list --state open --author @me` — my open PRs

Don't dump all this output to me — synthesize it.

# 3. Walk through each category with me, one at a time

For each of the categories below, summarize what you found, then ask me if I have anything to add or correct. Wait for my answer before moving to the next one. Keep it conversational — I'm tired.

**a. What I shipped today**
Summarize today's commits and any merged/closed PRs. Then ask: "Anything else you finished today that I should note?"

**b. What's in progress (committed but unpushed, or uncommitted)**
Tell me what's sitting on my laptop that isn't on the remote yet — unpushed commits, uncommitted changes, staged work, stashes. For each, say which file/feature it relates to. Then ask: "What state is each of these in? Anything I should know about why it's not pushed?"

**c. Open PRs**
Summarize each open PR I authored and its state (CI failing, comments to address, waiting on review). Then ask: "Anything to add about these — review feedback to address tomorrow, things you're waiting on?"

**d. What's broken or didn't work**
Ask directly: "Anything you tried today that didn't work, or anything currently broken in your branch I should flag for tomorrow?"

**e. Blockers**
Ask: "Anything blocking you that you need to deal with tomorrow? Could be technical, could be waiting on someone."

**f. Next steps**
Ask: "What's the first thing you want to pick up tomorrow? And after that?"

**g. Anything else**
Ask: "Anything else you'd be annoyed about forgetting — a weird gotcha, a TODO, a decision you made, a hack?"

# 4. Write handoff.md

Once we've gone through everything, overwrite `handoff.md` in the repo root with this structure. Use the git findings + my answers to fill it in.

```
# Handoff — <YYYY-MM-DD>

**Branch:** <current branch>

## Shipped today
- <commits/PRs that are done and pushed>

## In progress
- <unpushed commits, uncommitted work, staged changes, stashes — be specific about what file/feature and what state>

## Open PRs
- #<num> <title> — <state + anything I need to address tomorrow>

## What's broken / didn't work
- <from my answers>

## Blockers
- <from my answers, or "none">

## Next steps for tomorrow
1. <first thing>
2. <second thing>
3. ...

## Notes for future-me
- <gotchas, decisions, things I almost forgot>
```

Use "—" for any section with nothing to put in it. Don't pad.

# 5. Confirm

After writing:

```
Handoff written to handoff.md.

Tomorrow's sync picks up:
- Branch: <branch>
- <one-line summary of top in-progress item>
- <one-line summary of top blocker, if any>

Have a good evening.
```

