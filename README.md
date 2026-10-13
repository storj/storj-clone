# storj-clone

## Quick start

You can run this script straight from curl, if you want. You can use it to set up an existing repository with the correct remote and gerrit support aliases, or clone a new repository.

### Set up an existing repository

`curl -sSL storj.io/clone | sh`

### Clone a new repository

`curl -sSL storj.io/clone | sh -s <repo>`

## Installation

Download the `storj-clone` command, make sure it's executable, and place it into your `PATH`.

## Usage

### Setting up an existing repository

```
$ ls
storj

$ storj-clone
Adding gerrit remote with ssh://user@review.dev.storj.tools:29418/storj/storj...
Updating commit-msg hook...
Adding gerrit-support aliases...
```

### Cloning a repository

```
$ storj-clone drpc
Cloning into 'drpc'...
remote: Counting objects: 147, done
remote: Finding sources: 100% (147/147)
remote: Total 461 (delta 44), reused 411 (delta 44)
Receiving objects: 100% (461/461), 148.30 KiB | 1.07 MiB/s, done.
Resolving deltas: 100% (175/175), done.
Adding gerrit remote with ssh://user@review.dev.storj.tools:29418/storj/drpc...
Adding commit-msg hook...
Adding gerrit-support aliases...
```

### Cloning to a specific location

```
$ storj-clone drpc my-other-drpc
Cloning into 'my-other-drpc'...
remote: Counting objects: 147, done
remote: Finding sources: 100% (147/147)
remote: Total 461 (delta 44), reused 411 (delta 44)
Receiving objects: 100% (461/461), 148.30 KiB | 1.01 MiB/s, done.
Resolving deltas: 100% (175/175), done.
Adding gerrit remote with ssh://user@review.dev.storj.tools:29418/storj/drpc...
Adding commit-msg hook...
Adding gerrit-support aliases...
```

## Added commands

See [gerrit-support](gerrit-support/README.md) for documentation on some aliases storj-clone adds to the repository.

## Hosting

`storj.io/clone` serves `storj-clone` from the `main` branch of this
repository; the website build fetches it. The script downloads the
`gerrit-support` files from `main` too, so set `SUPPORT_REV` to a branch or
commit to try changes before merging.

This repository was imported from zeebo's gists, history included:
[storj-clone](https://gist.github.com/zeebo/ecc0abd0aec09c9eff85b12d788dfc81) and
[gerrit-support](https://gist.github.com/zeebo/108b15abab91cc3d9cfbf367090d6fa5).
