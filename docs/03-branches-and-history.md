# Branches and history

A branch is a movable name for a line of development. Branches make it
possible to work on changes separately and integrate them later.

## Create, list, and switch branches

```bash
git branch                         # List local branches
git branch --all                   # List local and remote-tracking branches
git switch -c <topic-branch>       # Create and switch to a branch
git switch <branch>                # Switch to an existing branch
git switch -                        # Switch to the previous branch
git branch -d <topic-branch>       # Delete a merged local branch
```

Git normally prevents switching when doing so would overwrite uncommitted
changes. Commit or stash work before switching if necessary. `git branch -D`
force-deletes a branch; use it only when you are sure its work is no longer
needed.

## Compare branches

```bash
git log --oneline main..HEAD
git diff main...HEAD
```

`main..HEAD` lists commits reachable from `HEAD` but not `main`. For `git diff`,
`main...HEAD` compares the current branch with the merge base it shares with
`main`, which is often useful when reviewing a topic branch.

## Rebase local work

Rebase replays commits on a new base, producing new commit IDs:

```bash
git fetch origin
git switch <topic-branch>
git rebase origin/main
```

If conflicts occur, resolve them, stage the resolved files, then continue:

```bash
git add <resolved-file>
git rebase --continue
```

Or cancel the rebase:

```bash
git rebase --abort
```

Because rebase rewrites commit history, avoid rebasing commits that are already
shared unless your team explicitly coordinates that workflow.

## Official references

- [`git-branch`](https://git-scm.com/docs/git-branch)
- [`git-switch`](https://git-scm.com/docs/git-switch)
- [`git-diff`](https://git-scm.com/docs/git-diff)
- [`git-rebase`](https://git-scm.com/docs/git-rebase)
- [Git workflows](https://git-scm.com/docs/gitworkflows)
