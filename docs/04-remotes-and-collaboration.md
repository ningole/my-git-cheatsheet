# Remotes and collaboration

A remote is a named reference to another repository, usually hosted on a
service or server. Git itself is distributed; a hosting service is optional
but commonly used to share work.

## Inspect and configure remotes

```bash
git remote -v
git remote add origin <repository-url>
git remote show origin
git remote rename origin upstream
git remote remove <remote-name>
```

`origin` is only a conventional name; it has no special behavior.

## Fetch changes

```bash
git fetch origin
git log --oneline HEAD..origin/main
```

Fetch downloads commits and updates remote-tracking branches such as
`origin/main`. It does not merge them into your current branch.

## Pull changes

```bash
git pull --ff-only
git pull --rebase
```

Pull fetches and then integrates changes into the current branch. `--ff-only`
allows an update only when it can move the branch forward without making a
merge commit; it stops if the histories have diverged. `--rebase` rebases
local commits on top of the fetched branch. Choose a policy that matches your
team's workflow.

## Push changes

```bash
git push -u origin <branch>
git push
```

The first command publishes the branch and sets its upstream, so later pushes
can usually use `git push`. A push can be rejected if the remote has commits
you do not have; fetch and integrate those commits before retrying.

Avoid `git push --force` on shared branches. If rewriting a branch is
necessary and your team agrees, `git push --force-with-lease` is safer than
plain `--force`, but it can still replace remote history.

## Typical team workflow

```bash
git switch main
git pull --ff-only
git switch -c <topic-branch>
# Edit, inspect, stage, and commit changes.
git push -u origin <topic-branch>
```

Then open a pull/merge request on your hosting service or coordinate with your
team to integrate the branch.

## Official references

- [`git-remote`](https://git-scm.com/docs/git-remote)
- [`git-fetch`](https://git-scm.com/docs/git-fetch)
- [`git-pull`](https://git-scm.com/docs/git-pull)
- [`git-push`](https://git-scm.com/docs/git-push)
- [Distributed workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows)
