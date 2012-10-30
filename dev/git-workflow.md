---
layout: default
---

# Git Workflow.

## Prepare to work.

### Github account.

Sign up for the [free plan](https://github.com/signup/free):

* Username: use something like `firstnamelastname`, avoid some crappy nicknames.
* Email: use email `@flatstack.com`

#### SSH key.

Check out our guide to [generating SSH keys](https://help.github.com/articles/generating-ssh-keys).

User `@flatstack.com` in the key:

    $ ssh-keygen -t rsa -C "firstname.lastname@flatstack.com"

### Git config.

You could install [dotfiles](https://github.com/fs/dotfiles) based on `oh-my-zsh`
or create `.gitconfig` manually based on [template](https://github.com/fs/dotfiles/blob/master/gitconfig)

## Git Workflow.

The basic flow should tied as much as possible to [Github flow](http://scottchacon.com/2011/08/31/github-flow.html)

* Get your own copy
* To work on something new, create a descriptively named branch off of stable branch, usually `master` (ie: `new-oauth2-scopes`)
* Commit to that branch locally and regularly push your work to the same named branch on the server
* When you need feedback or help, or you think the branch is ready for merging, open a pull request
* After someone else has reviewed the feature, you can merge it into master
* Once it is merged and pushed to `master`, you can and should deploy immediately

### Get your own copy.

If your account added to repository directly you just clone the repo.
Try to organize projects into subfolders based on clients organisation name.

    $ mkdir -p ~/develop/clients-org-name
    $ cd ~/develop/clients-org-name
    $ git clone git://github.com/clients-org-name/project-name.git

###  Create a descriptively named branch.

When you want to start work on anything, you create a **descriptively named** branch off of the stable branch.

    $ git pull origin master
    $ git checkout -b new-feature

### Do your work.

#### Rebase frequently to incorporate upstream changes.

Rebase often enough to avoid massive conflicts - rebasing after every few commits in master is better than rebasing after 45 commits in master.

    $ git fetch origin
    $ git rebase origin/master
    <resolve conflicts>

**Note:** You should rebase before submitting your pull request. Don’t rebase in the middle of a pull request.

#### Push to named branches constantly.

Never have code that exists only on your local machine - if you’re out sick or something, other people should be able to pull down what you were working on from Github.

It also make sure that our work is always backed up in case of laptop loss or hard drive failure.

    $ git push origin new-feature

**Note:** Avoid force-pushing to the master branch. This will likely cause conflicts for other developers and may overwrite their work without warning.

#### Write a [good commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)

* Present-tense summary under 50 characters
* Make the commit message **USEFUL**. `FIX` or `WIP` doesn’t help. Even if it was something small, describing what or why makes a big difference.

### Submit a Github pull request.

When you finish you work on feature create a [pull request](https://help.github.com/articles/using-pull-requests/) and for a code review in Campfire.

### Review code

A team member other than the author reviews the pull request.
They make comments and ask questions directly on lines of code in the Github web interface or in Campfire.

For changes which they can make themselves, they:

    $ git checkout new-feature origin/new-feature
    $ script/bootstrap
    $ script/ci

    # make small changes right in the branch
    # test the feature in browser

    $ script/ci
    $ git add .
    $ git commit -m 'Good commit message'
    $ git push origin new-feature

When satisfied, they comment on the pull request `Ready to merge.` or `+1` or `:shipit:`

### Merge

If someone signoff pull request and CI is green on this branch it's OK to merge pull request to the stable branch.

It OK to merge using Github merge button or manually with interactive rebase, squash commits, etc.

    $ git rebase -i origin/master         # squash commits
    $ script/ci                           # make sure specs are green

    $ git log origin/master..new-feature  # view a list of new commits.
    $ git diff --stat origin/master       # view changed files

    $ git checkout master
    $ git merge new-feature --ff-only
    $ git push origin master

You should receive Campfire notification right after push to master:

    Github B. [project-name/master] Merge pull request #21 from project-name/new-feature - FirstName LastName ( https://github.com/org-name/project-name/commit/… )

Delete local and remote feature branches after merging.

    $ git push origin :new-feature
    $ git branch -d new-feature

### Deploy

If you use [autodeploy to Heroku](/dev/ci-semaphoreapp) right after build your code should be pushed to Heroku in case specs are green.

You should receive Campfire notifications one from CI and one from Heroku right after deploy:

    CI B. [project-name/new-feature] Passed: "Good commit message" - FirstName LastName (https://semaphoreapp.com/projects/867/bran…)

    CI B. firstname.lastname+project-name@flatstack.com deployed 6dc7b79 to project-name http://project-name.herokuapp.com

**Note**: Make sure featured deployed correctly and test it in browser.