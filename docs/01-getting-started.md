# Getting started

## Install and identify yourself

Install Git for your operating system, then configure the name and email that
will be recorded in new commits:

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global --list
```

`--global` applies to your user account. Run a config command without it from
inside a repository to set that repository's value instead. The commit name and
email are metadata; they do not prove a person's identity.

## Create or copy a repository

```bash
mkdir my-project
cd my-project
git init
```

`git init` creates a repository in the current directory. To work on an
existing project, clone it instead:

```bash
git clone <repository-url>
cd <repository-directory>
```

Cloning creates a working copy and normally configures the source repository
as the remote named `origin`.

## Check the working tree

```bash
git status
git status --short
```

Git tracks committed files and reports changes in the working tree and staging
area. New files are untracked until added. Short status uses compact codes:
the first column describes the staging area and the second describes the
working tree.

## Help

```bash
git help
git help <command>
git <command> --help
```

For example, `git help status` opens the manual page for `git status`. Online
reference pages are available at [git-scm.com/docs](https://git-scm.com/docs).

## Official references

- [`git-config`](https://git-scm.com/docs/git-config)
- [`git-init`](https://git-scm.com/docs/git-init)
- [`git-clone`](https://git-scm.com/docs/git-clone)
- [`git-status`](https://git-scm.com/docs/git-status)
- [Git tutorial](https://git-scm.com/docs/gittutorial)
