---
layout: default
---

Semaphoreapp.com
================

Runs test on push to github from different branches.

Please ask clients to add `fs-admin` user to repository colloborators with `Administration` permissions
if we would like to build application with semaphore.

Good practice use [`script/bootstrap`](https://github.com/fs/rails3-base/blob/develop/script/bootstrap)
and [`script/ci`](https://github.com/fs/rails3-base/blob/develop/script/ci) for builds in CI:

    script/bootstrap ci
    script/ci

[Access](https://flatstack.basecamphq.com/W5010754)
