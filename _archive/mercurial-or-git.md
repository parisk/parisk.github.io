---
layout: post
title: A perpetual dilemma; Mercurial or Git?
permalink: /archive/hg-or-git
date: 2013-12-13
redirect_from:
  - /post/63969591909/a-perpetual-dilemma-mercurial-hg-or-git
---

[Mercurial](http://mercurial.selenic.com/) or [Git](http://git-scm.com/)? Many developers have to chose one of these two great [Source Control Managers](http://en.wikipedia.org/wiki/Revision_control), the differences of which may be really obscure, but they may be also critical to the development process of software.

In the first weeks of the existence of [sourceLair](https://www.sourcelair.com), we quickly found out that [SVN](http://subversion.tigris.org/) wasn't working for us. So, we had to choose a [Distributed Version Control System](http://en.wikipedia.org/wiki/Distributed_revision_control) and we were between [Git](http://git-scm.com/) and [Mercurial](http://mercurial.selenic.com/).

After a first failed attempt with [Git](http://git-scm.com/), I started using [Mercurial](http://mercurial.selenic.com/) (as a non-experienced developer using almost exclusively Windows), because of it being easier to use with [SVN](http://subversion.tigris.org/) in mind. More than a year later, while I was already familiar with UNIX, Mercurial, Git and SSH instead of HTTP for clone/pull/push, when I thought about replacing Mercurial with Git for the development of [sourceLair](https://www.sourcelair.com), the answer was fast and explicit; **no**. The main three reasons behind this decision are explained below.

## Sanity
This is the main win of Mercurial over Git for me. While both of them were built, almost at the same time, to solve the same problem, for me it seems like Git was built with performance in mind, while Mercurial was built with the human user in mind. Even the relative consistence, between server and client, that is imposed by Mercurial makes more sense to me, personally, for Source Control Management. Finally, the monolithic approach of Mercurial to itself makes more sense to me as a unified solid system aiming to solve a specific problem, compared to the 140+ different executables that compose Git, each one of those targets an individual problem.

## History is history
In Mercurial history is immutable. For me that translates to **safety**, since I am sure than no matter how many times I will do `hg push -f`, nothing is going to get lost, ever. In Git it is almost frequent seeing people changing the history of their repo by deleting commits, rebasing and stuff. This is some kind of freedom for sure, but there underlies the danger of doing the wrong thing the wrong time and wishing that this never happened. Humans are supposed to do mistakes, and I think the great thing with Mercurial is that gives you the freedom to do as many mistakes as you want, without endangering the future of your code.

## Branching system
Well here is another great win; in Mercurial branches are branches, they are not pointers. The branch of each commit, resides and will reside forever in the commit's metadata, no matter if you are merging or not, or if you add more commits in the branch, or even if you are *closing* the branch. This adds more semantics to your commits and make them branch-aware, something that consequently leads to having a consistent, organized and semantic code repository. If you 'd like though a branch in the same logic than the one of Git, you can chose Mercurial bookmarks, which work pretty much in the same way.

Obviously though, the two big wins of Git are its **performance** and **community** and this probably is not going to change in the immediate future.

Of course the selection of a Source Control Manager is something really personal, so there can be no general rule about that. So, this is not article trying to prove that Mercurial is better than Git. It is an article showcasing why Mercurial fit my personal needs compared to Git, when it comes to managing a code repository.

Written a lonely night in Cambridge, United Kingdom.