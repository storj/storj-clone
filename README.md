# storj-clone

`curl -sS https://gist.githubusercontent.com/zeebo/ecc0abd0aec09c9eff85b12d788dfc81/raw/storj-clone | sh -s`

## Quick start

You can run this script straight from curl, if you want. To clone drpc, you could run

```
$ curl -sS https://gist.githubusercontent.com/zeebo/ecc0abd0aec09c9eff85b12d788dfc81/raw/storj-clone | sh -s drpc
Cloning into 'drpc'...
remote: Counting objects: 147, done
remote: Finding sources: 100% (147/147)
remote: Total 461 (delta 44), reused 411 (delta 44)
Receiving objects: 100% (461/461), 148.30 KiB | 1019.00 KiB/s, done.
Resolving deltas: 100% (175/175), done.
Adding commit-msg hook...
Adding gerrit-support aliases...
```

## Installation

Download the `storj-clone` command, make sure it's executable, and place it into your `PATH`.

## Usage

### Cloning a repository

```
$ storj-clone drpc
Cloning into 'drpc'...
remote: Counting objects: 147, done
remote: Finding sources: 100% (147/147)
remote: Total 461 (delta 44), reused 411 (delta 44)
Receiving objects: 100% (461/461), 148.30 KiB | 1.07 MiB/s, done.
Resolving deltas: 100% (175/175), done.
Adding gerrit remote with ssh://zeebo@review.dev.storj.io:29418/storj/drpc...
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
Adding gerrit remote with ssh://zeebo@review.dev.storj.io:29418/storj/drpc...
Adding commit-msg hook...
Adding gerrit-support aliases...
```

### Setting up an existing repository

```
$ cd drpc

$ storj-clone drpc .
Updating commit-msg hook...
Updating gerrit-support aliases...
```

or

```
$ ls
storj

$ storj-clone storj
Adding gerrit remote with ssh://zeebo@review.dev.storj.io:29418/storj/storj...
Updating commit-msg hook...
Adding gerrit-support aliases...
```
