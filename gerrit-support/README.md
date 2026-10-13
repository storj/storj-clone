# Gerrit Support

## Installation

Use [storj-clone](../README.md).

---

## Usage

### push-review

`git push-review` is used to create and update changes.

```
$ git push-review
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 283 bytes | 283.00 KiB/s, done.
Total 2 (delta 0), reused 0 (delta 0)
remote: Processing changes: refs: 1, new: 1, done
remote:
remote: SUCCESS
remote:
remote:   https://review.dev.storj.tools/c/storj/gerrit-testing/+/163 add foo [NEW]
remote:
To ssh://review.dev.storj.tools:29418/storj/gerrit-testing
 * [new branch]      HEAD -> refs/for/master
```

### push-it

`git push-it` is exactly like `git push-review` except it doesn't mark the change ready or work in progress. An existing change keeps its state and a new change gets your Gerrit default.

```
$ git push-it
```

### reset-to

`git reset-to` is used to "reset --hard" to some gerrit changeset or to the most recent upstream ref.

To check out the most recent patchset for change number 147

```
$ git reset-to 147
From ssh://review.dev.storj.tools:29418/storj/storj
 * branch              4467c023e340d4bf799b829a387a6ed7b08d8139 -> FETCH_HEAD
HEAD is now at 4467c023 storagenode/trust: list implementation
```

To check out the most recent master

```
$ git reset-to
From ssh://review.dev.storj.tools:29418/storj/storj
 * branch              master     -> FETCH_HEAD
HEAD is now at 756b9b9e satellite/payments: coupons and coupon usage (#3648)
```

If you have an unclean status, `git reset-to` will error

```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git reset-to
It is unsafe to reset --hard with a dirty status. Please commit/stash and try again.
```

### pick

`git pick` is used to cherry-pick the lastest version of some change.

```
$ git pick 147
```

### push-draft

`git push-draft` is exactly like `git push-review` except it pushes a draft. It may not work yet.

```
$ git push-draft
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 283 bytes | 283.00 KiB/s, done.
Total 2 (delta 0), reused 0 (delta 0)
remote: error: branch refs/heads/master:
remote: You need 'Push' rights to upload code review requests.
remote: Verify that you are pushing to the right branch.
remote: User: zeebo
remote: Contact an administrator to fix the permissions
remote: Processing changes: refs: 1, done
To ssh://review.dev.storj.tools:29418/storj/gerrit-testing
 ! [remote rejected] HEAD -> refs/drafts/master (draft workflow is disabled)
error: failed to push some refs to 'ssh://zeebo@review.dev.storj.tools:29418/storj/gerrit-testing'
```

---

## Troubleshooting

If you're running into any problems, run the commands with `TEST=1` set. This will have the commands output a bunch of debug logging and not execute any state changing commands. Hopefully that will either let you figure out what's wrong, or you can paste it into #gerrit and get some help. For example,

```
$ TEST=1 git reset-to
--- caching REMOTE_PUSH...
---     caching REMOTE_NAME...
---         attempting to cache address when REMOTE_NAME=gerrit...
---         caching ADDRESS...
---             caching RAW_PUSH...
---                 remote for REMOTE_NAME=gerrit not found...
---             RAW_PUSH=INVALID
---             caching HOSTNAME...
---                 using default hostname...
---             HOSTNAME=review.dev.storj.tools
---             using default port with HOSTNAME=review.dev.storj.tools...
---         ADDRESS=review.dev.storj.tools:29418
---         found based on ADDRESS=review.dev.storj.tools:29418...
---     REMOTE_NAME=origin
---     using push url from REMOTE_NAME=origin...
--- REMOTE_PUSH=ssh://zeebo@review.dev.storj.tools:29418/storj/gerrit-testing
--- caching REMOTE_BRANCH...
---     using remote tracking branch of master...
--- REMOTE_BRANCH=master
git fetch ssh://zeebo@review.dev.storj.tools:29418/storj/gerrit-testing master
git reset --hard FETCH_HEAD
```

---

## Advanced

The tools attempt to figure out what your intent is without having to configure a lot. By default, if your computer's username matches your gerrit username, everything should just work. Here's how:

First, it tries to figure out the remote to push to. If there's a remote with `review.dev.storj.tools` in the name, it uses that. Otherwise, if there's a remote named `gerrit`, it uses that.

Second, it ensures that the remote name exists. If it doesn't, it constructs a remote by looking at your username, your project configuration, and the directory name of the git repository. You can override the username by setting the `gerrit.user` or `github.user` git config (in that priority order), and the project name by setting the `gerrit.project` git config. The name of the repo is always taken from the git directory.

Finally, it will push to whatever the remote tracking branch is for the current branch you're on. If there's no remote tracking branch, it uses `main`.
