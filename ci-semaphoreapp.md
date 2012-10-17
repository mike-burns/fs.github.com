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
* `private-key-encoded-with-base64` - Content of the SSH private key which will be used during push to Heroku.
   The good practice is to setup separate Heroku collaborator (eg: `timur.vafin+rails3-base@flatstack.com`) for each application with different SSH keys.

## Campfire notifications

You can setup Campfire notification for each build:
* Project settings -> Nitifications -> Campfire
* Setup subdomain: `flatstack`
* Room: **room name**, not an id
* Token: we use special Campfire user [CI Bot](https://flatstack.basecamphq.com/W5050260). Insert token here.

**Note:** make sure it have access to specified campfire Room.
