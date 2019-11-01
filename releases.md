# Releases

This document describes how OpenDevStack deals with releases.

## Release versioning

OpenDevStack uses one release version across several sub-repositories.
Specifically, `ods-core`, `ods-project-quickstarters`,
`ods-jenkins-shared-library`, `ods-provisioning-app`,
`ods-configuration-sample` and `ods-document-generation-svc` are versioned as one unit.

The version number for aforementioned repositores
is in the format `MAJOR.MINOR.PATCH` and thus loosely (!) follows SemVer.

Repository `ods-mro-jenkins-shared-library` is not in sync regarding release version
number, but follows same version format.

Repository `ods-document-generation-templates` is not in sync either, and follows a
different version format: `release/vMAJOR.MINOR` for branches and `vMAJOR.MINOR` for tags.

## Git

Development happens on the `master` branch. When a new `MAJOR.MINOR` release is
made, a new branch is created, e.g. `0.1.x` or `1.0.x`. On this branch, a tag is
created which represents a specific `MAJOR.MINOR.PATCH` version, such as `v0.1.0`,
`v0.1.1` or `v1.0.0`. Tags are never updated, while branches such as `0.1.x` evolve as
patches are made. Changes on release branches are merged back into `master` as
appropriate, however usually patches are done on `master` and then applied into affected
release branches.

As mentioned in [Release versioning](#release-versioning), `ods-mro-jenkins-shared-library`
and `ods-document-generation-templates` are following a different release speed (and format
for the last), but same aforementioned git flow conventions apply, respectively.

## Changelogs

Each repository keeps a separate changelog, in the format described by
[keepachangelog](https://keepachangelog.com/en/1.0.0/). Unreleased changes are
tracked when they are made (either in the pull request where the change is made
or shortly after merge). Once a release branch is created, the unreleased changes
are marked as being released in that branch (and this commit is then merged into
`master` as well).

To make sure each changelog is complete, select the version to be released from the
[projects overview](https://github.com/orgs/opendevstack/projects/) and filter for
e.g. `repo:opendevstack/ods-provisioning-app`.
Then check that all completed issues are referenced (linked) from the changelog.

## Updating

Users must not be required to take any action between patch versions. Between
`MAJOR.MINOR` versions, manual actions might need to be performed (such as
updating OpenShift resources). These actions have to be described in the
[update-guide](https://www.opendevstack.org/ods-documentation/common/latest/update-guide.html).

## Release process of `MAJOR.MINOR` versions

* Ensure changelogs and update guides are up-to-date and complete.
* Create the appropriate branch as described in the [Git](#git) section.
* In `ods-project-quickstarters`, on the release branch, set all pointers to the
  shared library in each `Jenkinsfile` to the release branch (e.g. change the
  pointer from `production` to `1.2.x`).
* In `ods-provisioning-app`, on the release branch, set the pointer to the
  shared library in the `Jenkinsfile` to the release branch (e.g. change the
  pointer from `production` to `1.2.x`).
* Tag the latest commit in each release branch with the specific version, e.g.
  `v1.2.0`.
* For `release-manager` quickstarter, in its `Jenkinsfile`, set from `production` to
  each respective new released tag (e.g. to tag `v1.2.0` for `ods-jenkins-shared-library`
  library, and to tag `v0.1.0` for `ods-mro-jenkins-shared-library` library).

## Release process of `MAJOR.MINOR.PATCH` versions

* Ensure changelogs are up-to-date and complete.
* Tag the latest commit in each release branch with the specific version, e.g.
  `v1.2.0`.
