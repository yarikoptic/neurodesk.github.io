---
title: "Create a pull request"
linkTitle: "Create a pull request"
weight: 5
description: >
  Creating pull requests and making contributions

---

When you're ready for feedback, submit a pull request. Pull requests
are a feature specific to GitHub. They provide a simple, web-based way
to submit your work (often called "patches") to a project. It's called
a _pull request_ because you're asking the project to _pull changes_
from your fork.

If you're unfamiliar with how to create a pull request, you can check
out GitHub's documentation on
[creating a pull request from a fork][github-help-create-pr-fork]. You
might also find GitHub's article
[about pull requests][github-help-about-pr] helpful. That all said,
the tutorial below will walk you through the process.


## Create a pull request

### Step 0: Make sure you're on a feature branch (not `master`)

It is important to [work on feature branch][feature-branch] when creating a pull
request. Your new pull request will be inextricably linked with your
branch while it is open, so you will need to reserve your branch only
for changes related to your issue, and avoid introducing extraneous
changes for other issues or from upstream.

If you are working on a branch named `master`, you need to create and
switch to a feature branch before proceeding.

### Step 1: Update your branch with git rebase

The best way to update your branch is with `git fetch` and `git rebase`. Do not
use `git pull` or `git merge` as this will create merge commits. See [keep your
fork up to date][keep-up-to-date] for details.

Here's an example (you would replace _issue-123_ with the name of your feature branch):

```console
$ git checkout issue-123
Switched to branch 'issue-123'

$ git fetch upstream
remote: Counting objects: 69, done.
remote: Compressing objects: 100% (23/23), done.
remote: Total 69 (delta 49), reused 39 (delta 39), pack-reused 7
Unpacking objects: 100% (69/69), done.
From https://github.com/NeuroDesk/neurocontainers/
   69fa600..43e21f6  master     -> upstream/master

$ git rebase upstream/master

First, rewinding head to replay your work on top of it...
Applying: troubleshooting tip about provisioning
```

### Step 2: Push your updated branch to your remote fork

Once you've updated your local feature branch, push the changes to GitHub:

```console
$ git push origin issue-123
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 658 bytes | 0 bytes/s, done.
Total 6 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 1 local objects.
To git@github.com:christi3k/neurocontainers.git
 + 2d49e2d...bfb2433 issue-123 -> issue-123
```

If your push is rejected with error **failed to push some refs** then you need
to prefix the name of your branch with a `+`:

```console
$ git push origin +issue-123
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 658 bytes | 0 bytes/s, done.
Total 6 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 1 local objects.
To git@github.com:christi3k/neurocontainers.git
 + 2d49e2d...bfb2433 issue-123 -> issue-123 (forced update)
```

This is perfectly okay to do on your own feature branches, especially if you're
the only one making changes to the branch. If others are working along with
you, they might run into complications when they retrieve your changes because
anyone who has based their changes off a branch you rebase will have to do a
complicated rebase.

### Step 3: Open the pull request

If you've never created a pull request or need a refresher, take a look at
GitHub's article [creating a pull request from a
fork][github-help-create-pr-fork]. 
Note: **Pull request titles are different from commit messages.** Commit
messages can be edited with `git commit --amend`, `git rebase -i`, etc., while
the title of a pull request can only be edited via GitHub.

## Update a pull request

As you make progress on your feature or bugfix, your pull request, once
submitted, will be updated each time you [push commits][self-push-commits] to
your remote branch. This means you can keep your pull request open as long as
you need, rather than closing and opening new ones for the same feature or
bugfix.

It's a good idea to keep your pull request mergeable with neurocontainer upstream by
frequently fetching, rebasing, and pushing changes. See [keep your fork up to
date][keep-up-to-date] for details. You might also find this excellent
article [How to Rebase a Pull Request][edx-howto-rebase-pr] helpful.

And, as you address review comments others have made, we recommend posting a
follow-up comment in which you: a) ask for any clarifications you need, b)
explain to the reviewer how you solved any problems they mentioned, and c) ask
for another review.

[edx-howto-rebase-pr]: https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request
[github-help-about-pr]: https://help.github.com/en/articles/about-pull-requests
[github-help-create-pr-fork]: https://help.github.com/en/articles/creating-a-pull-request-from-a-fork
[keep-up-to-date]: ../workflow#keep-your-fork-up-to-date
[self-push-commits]: ../workflow#push-your-commits-to-github
[feature-branch]: ../workflow#work-on-a-feature-branch