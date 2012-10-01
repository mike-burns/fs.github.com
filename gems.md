---
layout: default
---

# Gem management

Instead of using RVM gemset for isolating gems for your new Rails application it's better to use bundler "path" option:

    bundle install --path vendor/bundle --binstubs

will install all gems into the vendor/bundle and all executables to bin/
