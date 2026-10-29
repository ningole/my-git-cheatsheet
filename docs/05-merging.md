# Merging branches

Merging integrates changes from another branch into the current branch. First
switch to the branch that should receive the changes:

```bash
git switch main
git merge <topic-branch>
```

## Common merge outcomes

- **Fast-forward:** If the current branch has no new commits of its own, Git
  can move its name forward to the incoming commit. No merge commit is created.
- **Three-way merge:** If both branches have new commits since they diverged,
  Git combines their changes and normally creates a merge commit.
- **Conflict:** If Git cannot combine some changes automatically, it pauses
  and asks you to resolve them.

Options for controlling the result:

```bash
git merge --ff-only <branch>  # Merge only if it can fast-forward
git merge --no-ff <branch>    # Create a merge commit, even if fast-forward is possible
git merge --no-commit <branch>  # Stop before committing a non-fast-forward merge
```

`--no-commit` cannot stop a fast-forward merge because a fast-forward does not
create a commit. Combine it with `--no-ff` if you need to inspect the result
before a merge commit:

```bash
git merge --no-ff --no-commit <branch>
```

## Update a topic branch and inspect history

To bring the latest `main` into a topic branch, fetch first, then merge the
remote-tracking branch while checked out on the topic branch:

```bash
git fetch origin
git switch <topic-branch>
git log --oneline --left-right --graph HEAD...origin/main
git merge origin/main
```

The log command shows commits unique to each side before integration. Review
the branch names and status before running the merge.

## Squash merge

```bash
git switch main
git merge --squash <topic-branch>
git diff --staged
git commit -m "Describe the combined change"
```

A squash merge stages the combined changes but does not create a merge commit
or record the merged branch as an ancestor. This can make later merges of that
branch behave differently from a normal merge.

## Unrelated histories

Git normally refuses to merge branches with no common ancestor. Only when
those repositories are intentionally being combined, use:

```bash
git merge --allow-unrelated-histories <branch>
```

Review the result carefully; this option is not a routine conflict fix.

## Resolve a merge conflict

1. Inspect the conflicted paths:

   ```bash
   git status
   ```

2. Open each conflicted file. Conflict markers look like this:

   ```text
   <<<<<<< HEAD
   current branch version
   =======
   incoming branch version
   >>>>>>> topic-branch
   ```

3. Edit the file to the intended final content and remove the conflict
   markers. The right resolution may combine both changes; it is not always
   one side or the other.

4. Mark resolved files and finish the merge:

   ```bash
   git add <resolved-file>
   git diff --staged
   git merge --continue
   ```

   If `git merge --continue` is unavailable in an older Git version, run
   `git commit` after staging all resolutions.

To cancel the merge:

```bash
git merge --abort
```

Start a merge with a clean working tree where possible. Git warns that aborting
may not fully reconstruct pre-existing uncommitted changes.

## Conflict-side terms

During a merge, `ours` means the checked-out branch (the current branch), and
`theirs` means the branch being merged in. During a rebase these labels can
feel counterintuitive because commits are replayed onto another base. Inspect
the operation and file before choosing either side.

## After the merge

```bash
git status
git log --oneline --graph --decorate -10
```

Run the project's tests after resolving conflicts. Git can combine text
changes, but it cannot determine whether the resulting program behaves
correctly.

## Official references

- [`git-merge`](https://git-scm.com/docs/git-merge)
- [Advanced merging in Pro Git](https://git-scm.com/book/en/v2/Git-Tools-Advanced-Merging)
- [`git-merge-base`](https://git-scm.com/docs/git-merge-base)
- [Git workflows](https://git-scm.com/docs/gitworkflows)
