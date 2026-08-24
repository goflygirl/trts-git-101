# Git Cheat Sheet

The ~20 commands that cover almost everything you'll do day to day.

## Setup (once per machine)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@right-thing.solutions"
```

## Starting a repo

```bash
git init                    # turn the current folder into a repo (local only, no server needed)
git clone <url>              # copy a remote repo to your machine, remote already wired up as "origin"
```

## The daily loop: status → stage → commit

```bash
git status                   # what's changed, what's staged, what's not
git diff                     # line-by-line, what changed but is NOT staged yet
git diff --staged            # line-by-line, what IS staged and about to be committed
git add <file>                # stage a specific file
git add .                    # stage everything changed in this folder
git commit -m "message"       # save the staged snapshot to history, with a message
```

## Syncing with a remote (GitHub/GitLab)

```bash
git push                     # send your local commits to the remote
git push -u origin <branch>   # first push of a new branch — sets up the link
git pull                     # fetch + merge the remote's new commits into yours
git fetch                    # just download what's new, don't merge it yet
```

## Branches

```bash
git branch                   # list local branches
git switch -c my-feature      # create + switch to a new branch
git switch main               # switch back
git merge my-feature           # bring my-feature's commits into the branch you're on
```

## Pull request / merge request

Not a Git command — it's a feature of GitHub ("pull request") or GitLab
("merge request"). Same idea, different name: "here's a branch, please
review it, then merge it into main." Done on the website, not the terminal.

## Rebase

```bash
git rebase main               # replay your branch's commits on top of the latest main
git rebase --continue          # after fixing a conflict during a rebase
git rebase --abort             # bail out, back to how it was before the rebase started
```

Rebase vs. merge: merge adds a new "joining" commit and keeps both
histories exactly as they happened. Rebase rewrites your branch's commits
so it *looks like* you started from the latest main — cleaner history,
but never rebase commits someone else already pulled.

## Merge conflicts

```bash
git status                   # shows which files have conflict markers
# open the file, look for <<<<<<< ======= >>>>>>>, pick/edit the real content
git add <file>                 # mark it resolved
git commit                    # (merge) or: git rebase --continue (rebase)
```

## History

```bash
git log                      # full commit history
git log --oneline --graph --all   # the compact, branch-aware version — use this one
```

## Undoing things

```bash
git restore <file>            # discard unstaged changes to a file
git restore --staged <file>    # unstage a file (keeps the edit)
git revert <commit>            # make a NEW commit that undoes an old one — safe, keeps history
git reset --hard <commit>      # rewind and throw away history after it — only on your own local, unpushed work
```

`revert` is the one you reach for once something's pushed and shared —
it doesn't rewrite history, so it can't break anyone else's clone.

## Ignoring files

```bash
.gitignore    # one pattern per line, see this repo's own .gitignore for a real example
```
