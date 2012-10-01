---
layout: default
---

# Application configuration

Different application configurations could be stored in different places:

## Default settings for all environments

Should be stored in the `config/application.rb`

```ruby
# Application specific options
#
# Name used in the html titles and mailers
config.app_name = "Rails 3 Base example site"

# Default host for action mailer, initializers/mailer.rb
config.host = "localhost:5000"
```

## If need it overwrite settings for specified environments in the `config/environments/*.rb`

# Application specific options
#
config.host = "fs-rails3-base.heroku.com"


## Gem related settings

Should be stored in config/initializers/*.rb

```ruby
# config/initializers/mail_safe.rb

# allow send emails to the @example.com
#
if defined?(MailSafe::Config)
  MailSafe::Config.internal_address_definition = /^.*@example\.com$/i
end
```

```ruby
# config/initializers/mailer.rb

ActionMailer::Base.default_url_options[:host] = app_config.host
```

## Security sensitive config variables

Should not be stored in the git.
Better to set special environment variable in the `.env` file which will be loaded by `dotenv` gem from `config/initializers/01_config.rb`