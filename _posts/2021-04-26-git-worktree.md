---
title: "git worktree, no more stashing!"
layout: single
published: true
---
I recently discovered [`git-worktree`](https://git-scm.com/docs/git-worktree)
and it has been a game changer. I do not use these words lightly.

One of the silent pain points of using git for me has always been when working on
code in multiple branches. Each branch usually has a small new feature which adds 
on top of the main branch, or some branches have code that is specific to certain 
projects, which have deviated quite a bit from the main branch and live on a world  
its own.

When switching between branches, it was always messy. I had to stash code or 
commit them with half-baked commit messages which don't fully describe the feature.
Then, after I come back to that working branch, I've usually forgotten what I was doing.
Sound familiar?

Enter git worktree, it allows you maintain independent copies of the repo, where
each copy could be a working branch at the same time!

All you need to do to get started is, get rid of your old repo (ah ah not so fast!,
don't `rm -rf <repo>` before you commit everything to your remote).
