# Git Cheatsheet

A practical, command-by-command guide to Git, from your first repository to
merging branches and understanding Git's limitations. Commands use placeholders
such as `<branch>` and `<file>`; replace them with your own names.

## Pages

1. [Getting started](docs/01-getting-started.md) — setup, init, clone, and status
2. [Changes and commits](docs/02-changes-and-commits.md) — inspect, stage, and commit
3. [Branches and history](docs/03-branches-and-history.md) — branch, merge prep, and rebase
4. [Remotes and collaboration](docs/04-remotes-and-collaboration.md) — fetch, pull, and push
5. [Merging branches](docs/05-merging.md) — merge strategies and conflict resolution
6. [Undo and recovery](docs/06-undo-and-recovery.md) — restore, reset, revert, and reflog
7. [Git limitations](docs/07-limitations.md) — what Git does not do well and safer alternatives

## Daily workflow

```bash
git status
git switch -c <topic-branch>
git add -p
git diff --staged
git commit -m "Describe the change"
git push -u origin <topic-branch>
```

Check `git status` before destructive commands. Prefer `git revert` to undo
changes already shared with others; use `git reset --hard` only when you intend
to discard local work.

## Official references

- [Git documentation](https://git-scm.com/docs)
- [Git tutorial](https://git-scm.com/docs/gittutorial)
- [Git FAQ](https://git-scm.com/docs/gitfaq)
- [Pro Git book](https://git-scm.com/book/en/v2)
