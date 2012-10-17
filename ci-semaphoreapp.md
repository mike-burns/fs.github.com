---
layout: default
---

# Semaphoreapp.com


Runs test on push to github from different branches.

Please ask clients to add `fs-admin` user to repository collaborators with `Administration` permissions
if we would like to build application with semaphore.

[Access to Semaphoreapp account](https://flatstack.basecamphq.com/W5010754)

## Configuration

Good practice is to use [script/bootstrap](https://github.com/fs/rails3-base/blob/develop/script/bootstrap) and  [script/ci](https://github.com/fs/rails3-base/blob/develop/script/ci) for builds in CI:

    script/bootstrap ci # will run bundler setup and migrations if needed it
    script/ci # will run tests and code metrix checks

## Deploy to Heroku

If you would like ship code to Heroku right after success build you can use [script/ci_deploy](https://github.com/fs/rails3-base/blob/develop/script/ci_deploy)

    script/ci_deploy master your-heroku-app-name private-key-encoded-with-base64
    
* `master` - Branch which will deploy to Heroku after build, all other brunches will be ignored
* `your-heroku-app-name` - Name of you Heroku application, will used for generating right Heroku git remote repository name
* `private-key-encoded-with-base64` - Content of the SSH private key which will be used during push to Heroku. (see next section)

## Setup heroku account
The good practice is to setup separate Heroku collaborator for each application with different SSH keys.

Email should be like this: `your.email+project-name@flatstack.com` (e.g. `timur.vafin+rails3-base@flatstack.com` )

Then generate ssh keys for the new user: `ssh-keygen -t rsa -C "your.email+project-name@flatstack.com"`.

**WARNING**: do not rewrite your existing id_rsa key!

Add key to heroku https://devcenter.heroku.com/articles/keys. Make sure that you are adding keys for the newly created account (not your usual heroku account)

To encode key use base64: `base64 ~/.ssh/id_rsa_heroku_key`

## Campfire notifications

You can setup Campfire notification for each build:
* Project settings -> Nitifications -> Campfire
* Setup subdomain: `flatstack`
* Room: **room name**, not an id
* Token: we use special Campfire user [CI Bot](https://flatstack.basecamphq.com/W5050260). Insert token here.

**Note:** make sure it have access to specified campfire Room.
