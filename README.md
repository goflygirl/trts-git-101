# TRTS Git 101 🧪

Welcome! This repo is the hands-on companion for our 1-hour Git session.
You don't need to know anything about Git going in — by the end you'll have
made commits, opened a pull request, hit a real merge conflict, resolved
it, rebased a branch, and reverted a mistake, all in this repo.

## Before the session

1. Make sure `git` is installed: run `git --version` in a terminal.
2. Make sure you have a GitHub (or GitLab) account and can sign in.
3. Clone this repo:

   ```bash
   git clone <the-url-you-were-given> trts-git-101
   cd trts-git-101
   ```

That's it. Everything else happens live.

## What's in here

| File | Why it's here |
|---|---|
| `EXERCISES.md` | The step-by-step walkthrough we'll follow together, in order |
| `CHEATSHEET.md` | The commands, one-line explanations — keep this open in a tab |
| `playlist.md` | Our shared "team Friday playlist" — the file we'll all edit, which is how we'll trigger a real merge conflict on purpose |
| `.gitignore` | A real example of what to tell Git to never track |

## The one-sentence version of Git

Git is a tool that runs **entirely on your own machine** and keeps a
history of every version of your files you've told it to remember. A
"repo" (repository) is just a folder Git is doing that for. GitHub/GitLab
only enter the picture the moment you want to **share** that history with
someone else — everything up to that point is 100% local.

See `EXERCISES.md` to start.

## Team norms

- Small commits, honest messages.
- If you're not sure whether to squash, don't.
- Green build before you open a PR/MR.
