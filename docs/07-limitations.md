# Git limitations

Git is a powerful version-control system, but it is not a complete backup,
collaboration-hosting, or project-management service. Knowing where it stops
helps avoid data loss and choose appropriate tools.

## Large files and generated data

Git stores file contents in repository history. Frequently changing large
binary files can make clones and repository storage grow quickly; text-oriented
diffs and merges may also be unhelpful for binary formats. Keep generated
builds, caches, and other reproducible output out of source history when
possible. For large assets that must be versioned, consider
[Git Large File Storage (Git LFS)](https://git-lfs.com/).

## Merges do not understand program meaning

Git can merge many text edits based on lines and history, but a conflict-free
merge is not proof that the combined code is correct. Git cannot generally
resolve semantic conflicts, such as two changes that compile but violate a
shared business rule. Review the result and run tests.

Binary files and generated files often need a human decision or a format-aware
tool rather than an automatic text merge.

## Git is not a backup by itself

A local repository can be lost with the device or damaged along with its
working copy. A remote adds another copy, but important work still deserves
backups and a recovery plan. Do not treat unpushed commits, reflogs, or stashes
as durable backups.

## Do not cloud-sync an active repository directory

The Git FAQ warns that syncing a working repository file-by-file through a
cloud-sync service can corrupt repository metadata or lose data, especially
when synchronization happens during a Git operation. Use `git push` and
`git fetch` between repositories instead. Keep backups for important work.

## No empty directories or automatic tracking of ignored files

Git records files, not empty directories. Add a placeholder file if a directory
must exist in a checkout. `.gitignore` prevents matching untracked files from
being added by default; it does not stop tracking files that are already in the
repository.

## Git is not a hosting or access-control service

Git handles version history and repository transport. Pull requests, issue
tracking, permissions, protected branches, and hosted CI are generally
provided by a server or hosting platform. A commit's author name and email are
metadata, not proof of identity.

## Official references

- [Git FAQ: sharing a working tree across systems](https://git-scm.com/docs/gitfaq)
- [`gitignore`](https://git-scm.com/docs/gitignore)
- [`gitattributes`](https://git-scm.com/docs/gitattributes)
- [Git Large File Storage](https://git-lfs.com/)
- [Distributed workflows in Pro Git](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows)
