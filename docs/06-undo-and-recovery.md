# Undo and recovery

Choose an undo command based on where the change is and whether it has been
shared. Inspect `git status` before changing or discarding work.

## Unstage or discard file changes

```bash
git restore --staged <file>  # Unstage; keep working-tree changes
git restore <file>           # Discard unstaged changes to the file
git restore --source=HEAD --staged --worktree <file>
```

The last command replaces both the staged and working-tree versions with the
version from `HEAD`. These restore operations can discard work; review the
file and status first.

## Undo a commit

```bash
git revert <commit>
```

`revert` creates a new commit that reverses the selected commit. It is usually
the appropriate choice for changes that have already been pushed or shared.

For a local commit that has not been shared, `reset` moves the current branch
backward:

```bash
git reset --soft HEAD~1   # Keep changes staged
git reset HEAD~1          # Keep changes, unstaged (default --mixed)
git reset --hard HEAD~1   # Discard commit and working-tree changes
```

`--hard` can permanently discard work. Do not use it as a routine undo command.

## Recover a commit reference

```bash
git reflog
git switch -c recovery <commit-id>
```

The reflog records recent local movements of `HEAD` and branch references.
Find the commit you need, then create a branch at it before doing further
cleanup. Reflogs are local and expire; they are not a substitute for backups.

## Remove untracked files

Preview first:

```bash
git clean -n
git clean -nd
```

Then, only if the preview is correct:

```bash
git clean -f
git clean -fd
```

`git clean` deletes untracked files (`-d` includes untracked directories).
Ignored files are not included unless additional options are supplied. Treat
clean commands as destructive and inspect their preview.

## Official references

- [`git-restore`](https://git-scm.com/docs/git-restore)
- [`git-reset`](https://git-scm.com/docs/git-reset)
- [`git-revert`](https://git-scm.com/docs/git-revert)
- [`git-reflog`](https://git-scm.com/docs/git-reflog)
- [`git-clean`](https://git-scm.com/docs/git-clean)
