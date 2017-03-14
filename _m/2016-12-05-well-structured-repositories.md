---
layout: post
title: Well-structured repositories
medium_url: https://stateofprogress.blog/well-structured-repositories-db63864a9a14
---

Anyone who has ever contributed code in a collaborative software project, had hard time doing so at some point.

Usually there were various reasons for this; you didn’t know where to start, you could not get things working, you had to review illegible code and so on.

You also use some sort of version control software like Git that tracks the history of the code base (who did what and when) in a repository and collaborate within this framework.

While it’s not in the direct concerns of a repository though, it’s own structure can be catalytic in resolving the most important issues that people face when contributing to a software project.

**Now let’s get to the point.**

A well-structured repository should facilitate collaboration with the least friction possible among its contributors by taking care of:

1. **Explaining “How things work here”**
2. **Ensuring consistent code execution across all environments**
3. **Ensuring readability via code style uniformity**

At this point let’s clarify that these are not the only issues that a well-structured repository should take care of, but they are the most important and universal (valid across any programming language / technology).

Next, let’s get into details about why and how you should tackle these issues in your repositories.

### How things work here

There are few things more motivating for a developer, than feeling autonomous when working; knowing how to act inside given boundaries.

**The best place to start explaining how things work is a README file** in the root directory of the repository. While you can’t cover all topics in a README file, it’s a great place to talk about the basics (What is this project? How do I get started? How do I install this?) and also point the reader to complimentary helpful documentation of the repository.

An example of a repository that does just excellent work in explaining how things work is the [Linux kernel](https://www.kernel.org/). Just [take a look at its README file](https://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/about/)! It covers everything from What is Linux? to hardware and software requirements, documentation, and troubleshooting. It’s stunning.

It’s one of the most complex software projects on the planet, with [**more than 15 million lines of code**](http://arstechnica.com/business/2012/04/linux-kernel-in-2011-15-million-total-lines-of-code-and-microsoft-is-a-top-contributor/) and reading its README file makes you feel like you can get started almost right now!

In addition to README files, there are a few more elements that you should include in your directory to help contributors, like the following:

- a [LICENSE file](https://help.github.com/articles/open-source-licensing/): Let contributors know what are the terms of using and redestributing your software, especially if we are talking about an open-source project.
- a [CONTRIBUTING file](https://help.github.com/articles/setting-guidelines-for-repository-contributors/): Set the guidelines for contributions in the code base. How should someone send their patches (commits)? How should they file a bug?
- a docs directory: Self-explanatory. This is the place where everyone should look for the full documentation, so just make sure it is there and include the documentation of your code base

### Consistent code execution across all environments

Developers demand rightfully to stay in scope and deal only with what they have taken over at a given time.

Misconfigured builds and runs of an application are more than often a wet blanket. They either put developers into solving a different problem than the one they were thinking about a few seconds ago or have them delegate the task of *“fixing this”* to the sysadmin or devops person.

The repository should help the contributors focus on what they have to by letting them build and run their application in an almost infallible way. This should be done by:

1. **reducing the [Degrees of Freedom](https://en.wikipedia.org/wiki/Degrees_of_freedom_%28mechanics%29) of the contributor**: consequently reducing the possibilities of doing things the wrong way
2. **using industry-accepted descriptor files**: learn once, use anywhere

Such descriptor files can be:

- a [Makefile](https://www.gnu.org/software/make/manual/make.html#Introduction): running `make` should build your app properly
- a [Procfile](https://devcenter.heroku.com/articles/procfile): running `foreman start` should start all processes of your web app and should work on Heroku out of the box
- a [Dockerfile](https://docs.docker.com/engine/reference/builder/): running `docker build .` should build a self-contained image of your application to be run with Docker anywhere

Each one of the above examples has different Degrees of Freedom, but all of them have few enough to prevent developers from misconfiguring how their application will be built or run.

### Readability via code style uniformity

A code base with multiple code formatting patterns is pure terror for people that read through it.

A readable code base helps people contribute higher quality code by assisting code reviews and code reuse.

**The repository should include configuration files that will impose a uniform code style on behalf of the developers.**

At the moment of writing this article this can be accomplished by tools like:

- [EditorConfig](http://editorconfig.org/): maintain the same code styling between different editors and IDEs via an `.editorconfig` configuration file. IDEs from [SourceLair](https://www.sourcelair.com/features/editorconfig) to [WebStorm](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig) ship with built-in support for EditorConfig, while editors from [Vim](https://github.com/editorconfig/editorconfig-vim#readme) to [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig) offer available plugins.
- [ESLint](http://eslint.org/) (or any other linter): analyse the code base and let developers know about divergences from the desired code style via `.eslintrc.*` configuration files. These tools can be either [used in the command line](http://eslint.org/docs/user-guide/command-line-interface) or [integrated into the editor of choice](http://eslint.org/docs/user-guide/integrations). While such tools do not format the code on behalf of the developer, they let them know what they have to fix and lead to the same result with little more effort.

Now it’s time to ask yourself; *“Is my repository well-structured?”*.

The answer to this question is **Yes** only if the answer to all following questions is **Yes** as well:

1. Does my repository make crystal clear how things work here?
2. Does my repository allow consistent code execution across all environments?
3. Does my repository impose it’s own readability?

If the answer to the initial question is still **No**, then move on with taking care of these issues and you will find out you will get more work done with happier and more productive contributors.

If you enjoyed this article, please share your love by hitting the heart ❤️ on the left or sharing this on Twitter!

---

**P.S.:** To help everyone (including me) create better repositories from now on, I opened a public repository at GitHub to act as a well-structured skeleton for future projects: 🆓 [**https://github.com/parisk/skel**](https://github.com/parisk/skel) 🆓. Feel free to re-use as you wish.

If you do not want my initial commit laying in your project’s Git history, feel free to squash it right after your first commit with the following command:

```
git rebase -i --root HEAD
```

---

### References
- [**Readme Driven Development**](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html), by [Tom Preston-Werner](https://twitter.com/mojombo)
- [**Unsucking your team’s development environments**](https://zachholman.com/talk/unsucking-your-teams-development-environment/), by [Zach Holman](https://twitter.com/holman)