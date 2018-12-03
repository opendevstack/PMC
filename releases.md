# Releases

This document describes how OpenDevStack deals with releases.

## Release versioning

OpenDevStack uses one release version across several sub-repositories.
Specifically, `ods-core`, `ods-project-quickstarters`,
`ods-jenkins-shared-library`, `ods-provisioning-app` and
`ods-configuration-sample` are versioned as one unit. The version number is in
the format `MAJOR.MINOR.PATCH` and thus loosely follows SemVer.

## Git

Development happens on the `master` branch. When a new `MAJOR.MINOR` release is
made, a new branch is created, e.g. `0.1.x` or `1.0.x`. On this branch, a tag is
created which represents a specific `MAJOR.MINOR.PATCH` version, such as v0.1.0,
v0.1.1 or v1.0.0. Tags are never updated, while branches such as `0.1.x` evolve as
patches are made.

## Changelogs

Each repository keeps a separate changelog, in the format described by
[keepachangelog](https://keepachangelog.com/en/1.0.0/).

## Updating

Users must not be required to take any action between patch versions. Between
`MAJOR.MINOR` versions, manual actions might need to be performed (such as
updating OpenShift resources). These actions have to be described in
`opendevstack.github.io/doc/update-guide.md`.

## Release process of `MAJOR.MINOR` versions

* Ensure changelogs and update guides are up-to-date and complete.
* Create the appropriate branch as described in the [Git](#git) section.
* In `ods-project-quickstarters`, on the release branch, set all pointers to the
  shared library in each `Jenkinsfile` to the release branch (e.g. change the
  pointer from `production` to `1.2.x`).
* Tag the latest commit in each release branch with the specific version, e.g.
  `v1.2.0`.

## Release process of `MAJOR.MINOR.PATCH` versions

* Ensure changelogs are up-to-date and complete.
* Tag the latest commit in each release branch with the specific version, e.g.
  `v1.2.0`.
