---
title: Git reflog to the rescue
layout: post
categories: [git, programming]
---
Git reflog provides an audit trail of all the actions you have taken in git. The magical thing about it is that we can use it to recover from catastrophic failures, like when you accidentally do a git reset with the -hard flag when you didn’t mean to and hadn’t pushed it to remote - yep, been there!

Let’s do a little example where we just have some plain text files.

```
#make a wee folder
mkdir example
cd example
git init

#first commit
touch first.txt
git add .
git commit -m 'first file'

#second commit
touch second.txt
git add .
git commit -m 'second file'
```
Cool so our log should look something like this

```
commit ca57fc46e1c57b2947c458d42f9b98d5d3fb9921
Author: Valerie Dryden <outragedpinkracoon@gmail.com>
Date:   Tue Mar 28 09:15:40 2017 +0100

    second file

commit 407f489e5b73f473b89e2f4bd73df3172d47f61a
Author: Valerie Dryden <outragedpinkracoon@gmail.com>
Date:   Tue Mar 28 09:15:26 2017 +0100

    first file
```
We haven’t pushed anything to a remote branch, so if we were do to this:

git reset --hard head~1
The last commit is seemingly gone forever - not an issue if it’s one empty text file, but a huge problem if you a complex commit or have been rolling smaller commits into the head commit to keep your history tidy.

All is not lost! If we do:

```
git reflog
```
we should see something like this:

```
407f489 HEAD@{0}: reset: moving to head~1
ca57fc4 HEAD@{1}: commit: second file
407f489 HEAD@{2}: commit (initial): first file
```
This is a special audit trail of what we have been up to. One way we can sort our dilemma is to cherry pick back the commit we deleted:

```
git cherry-pick ca57fc4
```
Hurray! Catastophe averted. Make friends with reflog, it’s got your back when you have forgetten to push to remote…
