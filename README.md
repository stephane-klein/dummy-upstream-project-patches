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

```sh
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
```

I can remove the patch, here's how:

```
$ stg pop
- devkit-patch.patch-1

$ git log --oneline
d0ab6c8 (HEAD -> main, origin/main, origin/HEAD) First import
```

## How to create a new patch for the dummy-upstream-project?

```sh
$ cd dummy-upstream-project-patches
$ stg import ../devkit-patch.patch
$ stg new mysuper-feature.patch -m "My super private feature"
> mysuper-feature.patch (new)

$ stg series
+ devkit-patch.patch
> mysuper-feature.patch

$ git log --oneline
6836ed4 (HEAD -> main) My super private feature
2f56dae Add devkit
d0ab6c8 (origin/main, origin/HEAD) First import
```

I make some changes in the project:

```sh
$ echo "Add to file1" >> file1.js
$ cat file1.js
$ echo "Add to README" >> README.md
$ cat README.md
$ echo "New file4" >> file4.js
```

I check the changes with *stg*:

```sh
$ stg status
 M README.md
 M file1.js
?? file4.js
```

I add the modified files in the patch and perform a refresh:

```sh
$ stg add file4.js
$ stg add README.md file1.js
$ stg refresh
```

I export the patches to the parent Git repository (`dummy-upstream-project-patches`):

```sh
$ stg export -d ../
```

I check which patches have been modified:

```sh
$ cd ..
$ git status -s
 M series
?? mysuper-feature.patch
$ cat series
# This series applies on Git commit d0ab6c8d4c56f71b63b13fc6aa3a965eaf1a6ebd
devkit-patch.patch
mysuper-feature.patch
```
