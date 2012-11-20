---
layout: default
---

# Deploy to Heroku.com

## Prepare

[Create an account on Heroku.com and install Heroku Toolbelt](https://devcenter.heroku.com/articles/quickstart).

Please use your `@flatstack.com` email account.

## Create an application

By default we use Heroku's [Cedar Stack](https://devcenter.heroku.com/articles/cedar).
Recommended app name should include it's environment name.

    $ heroku create --remote heroku-staging akmeapp-staging

## Procfile

Cedar stack runs Rails with Webrick by default. Include `thin` server in `Gemfile`, and add a `Procfile` with
command to run it:

    web: bundle exec rails server thin -p $PORT -e $RACK_ENV

[Rails3 Base example](https://github.com/fs/rails3-base/blob/master/Procfile)

## Optimize slug size

Make sure Heroku won't install `development` and `test` gems

    $ heroku config:set BUNDLE_WITHOUT="development:test"

## Environments

Normally, we have a staging and production environment for our application.
We can handle this with different git remotes:

    $ git remote add heroku-staging git@heroku.com:myapp-staging.git
    $ git remote add heroku-production git@heroku.com:myapp-production.git

Setup `RACK_ENV, RAILS_ENV` accordingly with you app environment

    $ heroku config:set RACK_ENV=staging RAILS_ENV=staging

## Add-ons

Make sure app owner have [validated account](https://devcenter.heroku.com/articles/account-verification)
You can transfer application ownership to developer with valid account with:

    $ heroku sharing:add <new owner email>

### Send Grid

Normally we need to send Email from the app.
Enable [Send Grid](https://devcenter.heroku.com/articles/sendgrid) add-on:

    $ heroku addons:add sendgrid:starter

The following settings are necessary to configure ActionMailer

    ActionMailer::Base.smtp_settings = {
      :address        => 'smtp.sendgrid.net',
      :port           => '587',
      :authentication => :plain,
      :user_name      => ENV['SENDGRID_USERNAME'],
      :password       => ENV['SENDGRID_PASSWORD'],
      :domain         => 'heroku.com'
    }
    ActionMailer::Base.delivery_method = :smtp

[Rails3 Base example](https://github.com/fs/rails3-base/blob/master/config/environments/production.rb#L55-65)

### Notifications

#### Campfire

It's good to know when app shipped to the world.
Enable Campfire notifications on deploy:

<script src="https://gist.github.com/3960067.js"> </script>

* URL: `flatstack`
* ROOM_NAME: Campfire room name, not an id
* APY_KEY: API token, we use special Campfire user [Deploy Bot](https://flatstack.basecamphq.com/W5050260).

**Note:** make sure Deply Bot have access to specified campfire Room.

#### Airbrake.io

If you use [Airbrake.io](https://www.airbrake.io) for tracking exceptions, you should notify it about deploy:

<script src="https://gist.github.com/3960086.js"> </script>

* RAILS_ENV: Application current environment
* API_KEY: Airbrake.io API key, uniq per project
* SCM_REPOSITORY: github repository URL, example: `git://github.com/fs/rails3-base.git`

[Access to Airbrake.io](https://flatstack.basecamphq.com/W5071773)

## Deply with Semaphoreapp.com

If you would like ship code to Heroku right after success build you can use please follow [these instructions](/dev/ci-semaphoreapp).

## Make sure everything's ok.

Check out Heroku's [Visibility & Introspection](http://blog.heroku.com/archives/2011/6/24/the_new_heroku_3_visibility_introspection/)

    watch heroku ps
