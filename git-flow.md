---
layout: default
---

Git Flow
========

We are going to use [git-flow branching stategy](http://nvie.com/posts/a-successful-git-branching-model)
So now we have 2 branches: `develop` &` master`.

All new features are being started from `develop` branch
--------------------------------------------------------

    git flow feature start new-feature-name


* Once developer has finished working on a task, a pull-request is being issued
* Pull-request passes internal code-review phase 
* Once a task has passed internal code review it's being merged into `develop`, pull-request is closed, branch is deleted
* Developer makes sure all tests pass and deploys it to staging
* After staging has passed client review it's being merged with master and deployed to production


