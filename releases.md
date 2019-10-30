# Releases

This document describes how OpenDevStack deals with releases.

## Release versioning

OpenDevStack uses one release version across several sub-repositories.
Specifically, `ods-core`, `ods-project-quickstarters`,
`ods-jenkins-shared-library`, `ods-provisioning-app` and
`ods-configuration-sample` are versioned as one unit. The versioning scheme
is a simple number, increasing every release (e.g. `2`, `3` and so on). The
reasoning behind this is:

* A simple number across all components is easy to understand and use for users
* SemVer (which we used originally) is tricky for complex projects like ODS - it is only suited well to libraries
* As the next version number is always known, code on `master` can already point to it

For more background on the versioning, see #16.

Next to the major versions there might be patch releases as needed.
For now, major versions are expected to happen roughly twice a year.

## Git

Development happens on the `master` branch. When a new major release is
made, a new branch is created, e.g. `2` or `3`. On this branch, a tag is
created which represents a specific version, such as `v1`,
`v2` or `v2.1` (for patch releases if needed). Tags are never updated, while branches such as `2` evolve as
patches are made. Changes on release branches are merged back into `master` as
appropriate, however usually patches are done on `master` and then applied into affected
release branches.

## Changelogs

Each repository keeps a separate changelog, in the format described by
[keepachangelog](https://keepachangelog.com/en/1.0.0/). Unreleased changes are
tracked when they are made (either in the pull request where the change is made
or shortly after merge). Once a release branch is created, the unreleased changes
are marked as being released in that branch (and this commit is then merged into
`master` as well). 

To make sure each changelog is complete, select the version to be released from the [projects overview](https://github.com/orgs/opendevstack/projects/) and filter for e.g. `repo:opendevstack/ods-provisioning-app`.
Then check that all completed issues are referenced (linked) from the changelog.

## Updating

Users must not be required to take any action between patch versions. Between
major versions, manual actions might need to be performed (such as
updating OpenShift resources). These actions have to be described in
`opendevstack.github.io/doc/update-guide.md`.

## Release process of major versions

* Ensure changelogs and update guides are up-to-date and complete.
* Create the appropriate branch as described in the [Git](#git) section.
* Tag the latest commit on the release branch with the specific version, e.g.
  `v3`.

After the release:
* In `ods-project-quickstarters@master`, set all pointers to the
  shared library and agent images in each `Jenkinsfile` to the next version (e.g. change the
  pointer from `2` to `3`).
* In `ods-provisioning-app@master`, set the pointer to the
  shared library and agent images in the `Jenkinsfile` to the next version (e.g. change the
  pointer from `2` to `3`).


## Release process of patch versions

* Ensure changelogs are up-to-date and complete.
* Tag the latest commit in each release branch with the specific version, e.g.
  `v3.1`.
