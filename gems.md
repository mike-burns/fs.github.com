---
layout: default
---

# Gem management

Instead of using RVM gemset for isolating gems for your new Rails application it's better to use bundler "path" option:

    bundle install --path vendor/bundle --binstubs

will install all gems into the vendor/bundle and all executables to bin/


Enable rvm integration with Bundler (the “bin” directory is added to your path each time you cd into a project directory with binstubs)

  chmod +x $rvm_path/hooks/after_cd_bundler

