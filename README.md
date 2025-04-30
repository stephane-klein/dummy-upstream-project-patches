# sklein patches for dummy-upstream-project

This repository contains personal patches that are not intended to be directly integrated into the [`dummy-upstream-project`](https://github.com/stephane-klein/dummy-upstream-project).

For more information on this subject, you can consult the following note (in French): https://notes.sklein.xyz/2025-04-29_2236/zen/

These patches are managed by [Stacked Git](https://stacked-git.github.io/).

Here's how to install *Stacked Git* on *Fedora*:

```sh
$ sudo dnf install stgit
$ stg --version
Stacked Git 2.5.1
Copyright (C) 2005-2024 StGit authors
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
SPDX-License-Identifier: GPL-2.0-only
git version 2.49.0
```

## How to setup this repository and import patches?

```
$ git clone git@github.com:stephane-klein/dummy-upstream-project-patches.git
$ cd dummy-upstream-project-patches
$ git clone git@github.com:stephane-klein/dummy-upstream-project.git upstream/
$ cd upstream/
$ git log --oneline
d0ab6c8 (HEAD -> main, origin/main, origin/HEAD) First import

$ stg import ../devkit-patch.patch
> devkit-patch.patch (new)

$ git log --oneline
6bdd3aa (HEAD -> main) Add devkit
d0ab6c8 (origin/main, origin/HEAD) First import

$ stg pop
- devkit-patch.patch-1

$ git log --oneline
d0ab6c8 (HEAD -> main, origin/main, origin/HEAD) First import
```
