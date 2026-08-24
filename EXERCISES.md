# Git 101 — Live Exercises

Follow along at your own pace — nobody has to keep up with anyone else.
Each part says roughly how long we'll spend on it. Keep `CHEATSHEET.md`
open in another tab.

---

## Part 0 — Git with no repo, no server, no internet (5 min)

Before we touch this repo at all: Git needs **none** of that to work.

```bash
mkdir ~/scratch-git-demo && cd ~/scratch-git-demo
git init
echo "hello" > note.txt
git add note.txt
git commit -m "my first commit, completely offline"
git log
```

That's a fully working repo with real history, no GitHub/GitLab involved
at any point. **This is the thing to remember**: Git tracks changes on
your machine the moment you run `git init`. A remote (GitHub/GitLab) only
enters the picture the moment you choose to push somewhere.

You can `rm -rf ~/scratch-git-demo` when done — we won't need it again.

---

## Part 1 — Clone, and what "local vs. remote" actually means (5 min)

```bash
git clone <the-url-you-were-given> trts-git-101
cd trts-git-101
git remote -v
```

`origin` is just a nickname for "the URL this came from." Everything you
do next (edits, `git add`, `git commit`) stays 100% on your machine —
right up until you type `git push`.

---

## Part 2 — Stage and commit a change (10 min)

Open `playlist.md`, add a song of your choice at the bottom.

```bash
git status                # see it listed as "modified"
git diff                  # see the exact line you changed
git add playlist.md       # stage it
git status                # now it's "staged", not committed yet
git commit -m "Add <your song> to the playlist"
git log --oneline         # your commit is now part of history
```

Staging is the "which changes go into the *next* commit" step — you can
`git add` half a file's changes and leave the rest for later.

---

## Part 3 — Push and pull (5 min)

```bash
git push
```

Now everyone's commit is visible to everyone else on the remote. Pull
whoever went before you:

```bash
git pull
git log --oneline --graph --all
```

---

## Part 4 — Branch for a feature (10 min)

```bash
git switch -c my-name/add-song
# edit playlist.md again
git add playlist.md
git commit -m "Add another song"
git push -u origin my-name/add-song
```

Go to GitHub (or GitLab) in the browser → open a **pull request** (GitHub)
/ **merge request** (GitLab) from your branch into `main`. Same concept,
different vendor name. Someone reviews it, then merges it — that's the
whole point of doing it as a branch instead of committing straight to
`main`.

---

## Part 5 — A real merge conflict, on purpose (10 min)

We'll do this one together as a group using two prepared branches:
`exercise/conflict-a` and `exercise/conflict-b`. Both change the exact
same line of `playlist.md`, differently.

```bash
git switch main
git merge exercise/conflict-a      # merges cleanly
git merge exercise/conflict-b      # <-- conflict!
```

Git stops and marks the file:

```
<<<<<<< HEAD
1. Daft Punk — Get Lucky
=======
1. Queen — Don't Stop Me Now
>>>>>>> exercise/conflict-b
```

Open `playlist.md`, decide what the line should actually say (keep one,
keep both, write something new), delete the `<<<<<<<` / `=======` /
`>>>>>>>` markers, then:

```bash
git add playlist.md
git commit
```

That's it — a conflict is just Git asking a human to make a call it
can't make for you.

---

## Part 6 — Rebase (5 min)

`exercise/rebase-me` branched off `main` a few commits ago and has fallen
behind. Instead of merging main into it (which adds a merge commit),
we'll replay its commit on top of the latest main:

```bash
git switch exercise/rebase-me
git rebase main
git log --oneline --graph
```

Compare that history to what `git merge` would have produced — rebase
keeps the line straight.

---

## Part 7 — Revert a mistake (5 min)

Somewhere in this repo's history is a commit that broke the playlist by
mistake. Find it, then undo *just that commit* without touching anything
that came after it:

```bash
git log --oneline
git revert <the-bad-commit-hash>
```

Note this makes a **new** commit that undoes the old one — it doesn't
rewrite history, so it's safe to do even after you've pushed and other
people have already pulled.

---

## Part 8 — AI-assisted commits and attribution (5 min)

If you ask an AI assistant (Claude, Copilot, etc.) to write or fix code
and it drafts the change, you can credit it in the commit itself:

```bash
git commit -m "Fix playlist formatting

Co-authored-by: Claude <noreply@anthropic.com>"
```

Look at `git log -1` on the commit that added `playlist.md` in this repo
— it already has one. On GitHub, a `Co-authored-by:` trailer makes that
author show up as a contributor on the repo (and, if it's a real GitHub
account, on their profile's contribution graph — there's even an
achievement badge, "Pair Extraordinaire," for it). It's the honest way to
say "I didn't write 100% of this alone."

---

## Done

You've now done everything in `CHEATSHEET.md` at least once for real.
Keep the cheat sheet — that's the part meant to outlive today.
