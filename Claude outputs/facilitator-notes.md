# Facilitator notes — Git 101 (for you and Tilen only, not the team)

Don't hand this file to participants — it spoils the conflict/rebase/revert
answers. `trts-git-101.zip` is the file for them.

## 1. One-time setup, before the session

The zip contains a real local Git repo (with full history and branches
already built) — nothing has been pushed anywhere yet. You need to put it
somewhere participants can clone from:

```bash
unzip trts-git-101.zip && cd git-101-trts

# create a new EMPTY repo on GitHub/GitLab first (no README/gitignore
# auto-init — you already have those, and auto-init will conflict with
# this history)

git remote add origin <the-empty-repo-url>
git push -u origin main
git push origin exercise/conflict-a exercise/conflict-b exercise/rebase-me
```

Then invite the team to that repo (or make it public/internal), and give
them the clone URL for `README.md` → "Before the session".

If you want every participant to be able to push their own branch/PR
during Part 4, make sure everyone has write access (or fork it — up to
you and how your GitHub/GitLab org is set up).

## 2. What's already built into the repo, and why

- **`main`**: 6 commits telling a small story — includes one commit with
  a `Co-authored-by: Claude <noreply@anthropic.com>` trailer (the AI
  co-author demo in Part 8), and one deliberate "oops" commit
  (`Swap in a Daft Punk pick for #3`) that silently overwrites the
  "Dua Lipa — Levitating" line — that's the target for the Part 7 revert
  exercise.
- **`exercise/conflict-a`** and **`exercise/conflict-b`**: both branch
  from the tip of `main` and edit the *same line* of `playlist.md`
  differently. Merging `a` then `b` into `main` is guaranteed to conflict
  — verified live before packaging this.
- **`exercise/rebase-me`**: branches from `main` a few commits back (right
  after "Add workshop exercises") and adds a README edit. `main` then
  gets 2 more commits, so `exercise/rebase-me` is behind. `git rebase
  main` from that branch replays cleanly (no conflict) — verified.

## 3. Answer key

- **Part 5 conflict**: resolved file should end up with one line for
  "pick #1" — either "Daft Punk — Get Lucky", "Queen — Don't Stop Me
  Now", or something the group agrees on. There's no wrong answer as
  long as the `<<<<<<<`/`=======`/`>>>>>>>` markers are gone.
- **Part 6 rebase**: after `git rebase main`, `git log --oneline --graph`
  on `exercise/rebase-me` should show a straight line, Team Norms commit
  now sitting directly on top of the latest `main` commit.
- **Part 7 revert**: `git log --oneline` — the commit to revert is
  `Swap in a Daft Punk pick for #3`. After `git revert <hash>`,
  `playlist.md` line 3 goes back to "Dua Lipa — Levitating".

## 4. Timing (fits inside 60 minutes)

Part 0 (5) + Part 1 (5) + Part 2 (10) + Part 3 (5) + Part 4 (10) +
Part 5 (10) + Part 6 (5) + Part 7 (5) + Part 8 (5) = 60 min exactly.
Parts 2 and 4 are the ones most likely to run long (people get chatty
picking songs) — that's your buffer to cut if you're behind; Part 5
(the conflict) is the one people remember, don't cut that one.

## 5. Resetting between runs

If you ever want to reuse this repo for a second cohort, the cleanest
option is re-zipping a fresh copy of the original — once participants
push their own commits/branches to `main` and open PRs, the repo stops
being pristine (by design, that's the point of Part 2-4).
