# Git Cheatsheet

A quick reference for common Git commands.

## Set up Git

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global --list
```

Use `--global` to apply a setting to all repositories for your user. Omit it to
configure only the current repository.

## Start a repository

```bash
git init
git clone <repository-url>
```

## Check repository status

```bash
git status
git status --short
git diff                 # Unstaged changes
git diff --staged        # Staged changes
git log --oneline --graph --decorate --all
```

## Stage and commit changes

```bash
git add <file>           # Stage one file
git add .                # Stage changes in the current directory
git add -p               # Interactively stage parts of changes
git commit -m "Describe the change"
git commit --amend       # Update the most recent commit
```

Amending changes a commit's history. Avoid amending commits that have already
been shared with others.

## Branches

```bash
git branch                         # List local branches
git switch -c <branch-name>        # Create and switch to a branch
git switch <branch-name>           # Switch branches
git branch -d <branch-name>        # Delete a merged branch
git branch -D <branch-name>        # Force-delete a branch
git merge <branch-name>            # Merge a branch into the current branch
```

## Remotes and synchronization

```bash
git remote -v
git remote add origin <repository-url>
git fetch origin
git pull --ff-only
git push -u origin <branch-name>   # Publish a branch and set its upstream
git push
```

`git fetch` downloads remote changes without merging them. `git pull` fetches
and integrates changes into the current branch.

## Undo or recover changes

```bash
git restore <file>                 # Discard unstaged changes to a file
git restore --staged <file>        # Unstage a file; keep its changes
git revert <commit>                # Create a commit that reverses a commit
git reflog                         # Find recent branch/HEAD positions
```

Use `git revert` to undo a commit that has been shared. `git reset` rewrites
local history; use it carefully:

```bash
git reset --soft HEAD~1            # Undo commit; keep changes staged
git reset HEAD~1                   # Undo commit; keep changes unstaged
git reset --hard HEAD~1            # Discard commit and its changes
```

`git reset --hard` permanently discards uncommitted changes. Check `git status`
before using it.

## Stash temporary changes

```bash
git stash push -m "Work in progress"
git stash list
git stash pop                      # Reapply and remove the latest stash
git stash apply                    # Reapply but keep the stash
```

## Tags

```bash
git tag                            # List tags
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin v1.0.0
git push origin --tags
```

## Ignore files

Add file patterns to `.gitignore`, for example:

```gitignore
.env
node_modules/
*.log
```

Git does not track empty directories. If a file is already tracked, adding it
to `.gitignore` will not untrack it; use `git rm --cached <file>` to stop
tracking it while keeping the local file.
