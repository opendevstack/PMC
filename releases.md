# Releases

This document describes how OpenDevStack deals with releases.

## Release versioning

OpenDevStack uses one release version across several sub-repositories.
Specifically, `ods-core`, `ods-quickstarters`,
`ods-jenkins-shared-library`, `ods-provisioning-app` and
`ods-document-generation-svc` are versioned as one unit. Major releases are 
identified by a version such as 2, 3, 4.

A major update (e.g. 2.x to 3.x or 3.x to 4.x) is, from a user perspective, an explicit update. This means that even if admins update the ODS installation in the cluster, users still have to adopt that change (e.g. by updating their Jenkins image reference and so on). Therefore, a major version change is accompanied by an update guide. For admins, a major update might mean that configuration options have to be changed or migration steps to be taken, as well as rebuilding and rolling out all images etc.

A minor update (consuming changes/bugfixs on a release branch such as 3.x). From a user perspective, this is an implicit update. This means that only admins have to make a change to the ODS installation in the cluster. Users must get those changes automatically, without the need to explicitly adopt it. Therefore, there is no update guide for minor updates. For admins, a minor update should not require changing configuration options nor performing migration steps - only rebuilding and rolling out some (or all) images should be needed.

## Git

Development happens on the `master` branch. When a new major release is
made, a new branch is created, e.g. `3.x` or `4.x`. On this branch, a tag is
created which represents a specific version, such as `3.0` or
`4.0`. Tags are never updated, while branches such as `3.x` evolve as
patches are made. Changes on release branches are merged back into `master` as
appropriate, however usually patches are done on `master` and then applied into affected
release branches.

## Changelogs

Each repository keeps a separate changelog, in the format described by
[keepachangelog](https://keepachangelog.com/en/1.0.0/). Unreleased changes should be
tracked when they are made (either in the pull request where the change is made
or shortly after merge).

To make sure each changelog is complete, select the version to be released from the [projects overview](https://github.com/orgs/opendevstack/projects/) and filter for e.g. `repo:opendevstack/ods-provisioning-app`.
Then check that all completed issues/pull requests are referenced (linked) from the changelog.

## Release process of major versions

* Ensure changelogs and update guides are up-to-date and complete.
* Create a new section for the new version in the changelogs on master branch and move all unreleased entries to it.
* Create the appropriate branch as described in the [Git](#git) section.
* In each repository on the release branch, remove the `prerelease: Preview` from `docs/antora.yml`.
* Tag the latest commit in each release branch with the specific version, e.g. `3.0`.
* In each repository on the master branch, set `version` in `docs/antora.yml` to the next major version number (e.g. `3.x`).
* In each quickstarter inside `ods-quickstarters` on the master branch, set `version` to the next major version number (e.g. `3.x`) in the `files/metadata.yml` file.
* Update the roadmap section in file `docs/modules/getting-started/pages/index.adoc` in repository `ods-core` on master.

## Release process of minor versions

* Ensure changelogs are up-to-date and complete.
* Create a new section for the new version in the changelogs on release branch and move all unreleased entries to it.
* Cherry-pick the changelog update into master.
* Tag the latest commit in each release branch with the specific version, e.g.
  `3.1`.
