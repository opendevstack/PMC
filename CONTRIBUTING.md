# Contributing to OpenDevStack

The following is a set of guidelines for contributing to [OpenDevStack](https://github.com/opendevstack) and its related packages and tools.  

#### Table Of Contents

[Prerequisites](#prerequisites)

[Notes](#notes)

[How to setup](#how-to-setup)

[How to update from github.com/opendevstack](#how-to-update-from-github.com/opendevstack)

[How to contribute](#how-to-contribute)




## Prerequisites
* All repos are created on your Bitbucket server (see [Getting Started](https://github.com/opendevstack) guide).


## Notes
Please note that all masters and all other from OpenDevStack derived tags need to stay clean at each point in time. OpenShift and Rundeck are configured to point to the production branch, where you can make changes.



## How to setup

* Clone the relevant repository from Bitbucket.

* Fork repo on OpenDevStack GitHub to namespace you own (following referred to as *<YOUR_GITHUB_ACCOUNT_NAME>*).

* Add the github/opendevstack master as a remote called '*github-opendevstack*', your fork as '*github-<YOUR_GITHUB_ACCOUNT_NAME>*' as well as the repo on Bitbucket as '*bitbucket-opendevstack*'.
  ```sh
  git remote add github-opendevstack https://github.com/opendevstack/<REPO_NAME>.git
  git remote add github-<YOUR_GITHUB_ACCOUNT_NAME> https://github.com/<YOUR_GITHUB_ACCOUNT_NAME>/<REPO_NAME>.git
  git remote add bitbucket-opendevstack <YOUR_BITBUCKET_REPO_URL>
  ```



## How to update from github.com/opendevstack

* Checkout master.
  ```sh
  git checkout master
  ```

* Fetch updates from '*github-opendevstack*' remote.
  ```sh
  git fetch github-opendevstack
  ```

* Merge '*github-opendevstack/master*' into your local master. Alternatively merge a certain tag into a local tag branch.
  ```sh
  git merge github-opendevstack
  ```

* Push the merged changes from your local master to '*github-<YOUR_GITHUB_ACCOUNT_NAME>/master*' remote. (Optional)
  ```sh
  git push github-<YOUR_GITHUB_ACCOUNT_NAME> master
  ```

* Push the merged changes from your local master to '*bitbucket-opendevstack/master*' remote.
  ```sh
  git push bitbucket-opendevstack master
  ```

* Create a Pull Request on Bitbucket master to production branch for the changes we pushed to master in the previous step. This serves as a gate to control changes coming in, and spread knowledge about what has changed exactly.

* Check the changelog for anything to update/reinstall via change-scripts, new ods-configuration properties etc. and do it.
  


## How to contribute

* Create a branch from master.
  ```sh
  git checkout master
  git checkout -b <BRANCH_NAME>
  ```

* Make your code changes in this branch.

* After finishing, push this branch to bitbucket-opendevstack.
  ```sh
  git push bitbucket-opendevstack <BRANCH_NAME>
  ```
  
* Test your changes by pointing OpenShift to this branch.
  
* Create a PR on Bitbucket targeting the production branch and wait until it gets approved and merge it.

* Push your branch to your forked repo on GitHub.
  ```sh
  git push github-<YOUR_GITHUB_ACCOUNT_NAME> <BRANCH_NAME>
  ```

* Create a PR from this github-<YOUR_GITHUB_ACCOUNT_NAME>/<BRANCH_NAME> branch on your GitHub repo to the OpenDevStack GitHub repo. 