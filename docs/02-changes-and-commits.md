# Changes and commits

Git's staging area (also called the index) lets you choose exactly which
changes go into the next commit.

## Inspect changes

```bash
git diff                  # Unstaged changes
git diff --staged         # Staged changes
git diff <commit>         # Working tree compared with a commit
git show <commit>         # A commit and its changes
git log --oneline         # Compact commit history
git log --oneline --graph --decorate --all
```

Review the staged diff before committing: it is the content the next commit
will record.

## Stage changes

```bash
git add <file>            # Stage a file
git add <directory>       # Stage changes under a directory
git add -p                # Select changes interactively
git add -A                # Stage additions, modifications, and deletions
git restore --staged <file>  # Unstage a file, keeping its working-tree changes
```

`git add` stages the file's contents as they exist when the command runs. If
you edit the file again afterward, stage it again to include those later
changes.

## Commit

```bash
git commit -m "Add input validation"
git commit                # Open the configured editor for the message
git commit --amend        # Replace the most recent commit
```

Use a short, descriptive message. `--amend` creates a replacement commit; do
not amend commits that others may already have based work on.

## Ignore untracked files

Create a `.gitignore` file in the repository:

```gitignore
.env
node_modules/
*.log
```

Ignore rules do not affect files already tracked by Git. To stop tracking a
file but keep it on disk:

```bash
git rm --cached <file>
```

## Official references

- [`git-add`](https://git-scm.com/docs/git-add)
- [`git-diff`](https://git-scm.com/docs/git-diff)
- [`git-commit`](https://git-scm.com/docs/git-commit)
- [`git-log`](https://git-scm.com/docs/git-log)
- [`gitignore`](https://git-scm.com/docs/gitignore)
