---
title: "git worktree, no more stashing!"
layout: single
published: true
---
I recently discovered [`git-worktree`](https://git-scm.com/docs/git-worktree)
and it has been a game changer. I do not use these words lightly.

One of the silent pain points of using git for me which was agonizing at times, 
was when working on code locally in multiple branches simultaneously. 
Each branch usually has a small new feature under development which wishes to add 
on top of the main branch, or some branches have code that is specific to 
certain projects or new releases, which have deviated quite a bit from the main 
stable branch and live on a world of its own.

When switching between branches, it was always messy. I had to stash code or 
commit them with half-baked commit messages which don't fully describe the feature 
because hey! the feature isn't fully done yet.
Then, after I come back to that working branch, I've usually forgotten what I was doing.
Can you relate to this? No? You guys love stashing? In that case, you can skip 
the rest of this post.

Enter git worktree, it allows you to maintain independent copies of the repo, where
each copy is a working branch at the same time!

All you need to do to get started is, get rid of your old repo (ah ah ah not so fast!,
as much as you'd like to, don't `rm -rf <repo>` before you commit and push your local changes 
to your remote copy). So with a clean slate, let's start with

```bash
git clone --bare <https://github.com/you/your_repo.git> your_repo
```

Now when you change directory to your repo, you will notice that it doesn't 
look like your repo at all. There are all these files and folders like `HEAD`, `config`,
`refs`, `worktrees`, etc. Don't Panic! This is a bare worktree of your repo, and the files and other
stuff you see are what's needed in the local copy of the repo to enable you to use worktrees
and take advantage of the corresponding workflow.

First, lets get our one and only main branch back. Just do

```bash
git worktree add main
```

This now checks out the latest commit on the main branch and creates a folder with 
the copy of the repo at that commit. You can do a quick `ls` command and you will
notice the folder `main` with the contents of the repo after the latest commit.

Similarly, you can now add any number of copies of your repo checking out various
commits from different branches, and work on them all in the same parent directory!

To list each working tree you can do

```bash
git worktree list
```

You will notice all the different working trees along with the `(bare)` one which
represents the bare repo.

That's it! We are now ready to take advantage of git worktrees! I can't believe 
I didn't know about git worktree all these years (the feature was available since 2015!).

Sigh, never too late I guess 😒.

P.S. Another cool take away is that since each branch exists in different working folders,
depending on your development environment (workflow) and programming language in question, 
you can save the time needed to reinstall dependencies each time you want switch between 
branches, assuming they have a different set of dependencies. 

Furthermore imagine you are executing some program from inside a worktree. Since, you would never 
have to switch branches or stash code, if the program needs the state of the repo to be unchanged while 
it executes then the isolation provided by worktrees becomes quite convenient.
