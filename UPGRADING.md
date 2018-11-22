# Upgrading

## 0.1.0 to 1.0.0

### Update configuration

See what has changed in `ods-configuration-sample` and update
`ods-configuration` accordingly.

### Update OCP templates

Go to `ods-project-quickstarters/ocp-templates/scripts` and run
`./upload-templates.sh`.

### Update `xyz-cd` projects

There is a new webhook proxy now, which proxies webhooks sent from BitBucket to
Jenkins. As well as proxying, this service creates and deletes pipelines on the
fly, allowing to have one pipeline per branch. To update:

* Setup the image in the `cd` project by running `tailor update` in
  `ods-core/jenkins/webhook-proxy/ocp-config`.
* Build the image.
* Setup the  webhook proxy next to each Jenkins instance. E.g., go to
  `ods-project-quickstarters/ocp-templates/templates` and run
  `oc process cd/cd-jenkins-webhook-proxy | oc create -f- -n xyz-cd`. Repeat for
  each project.

### Update components

For each component, follow the following steps:

In `Jenkinsfile`:
1. Set the shared library version to `1.0.x`.
2. Replace `stageUpdateOpenshiftBuild` with `stageStartOpenshiftBuild`.
3. Remove `stageCreateOpenshiftEnvironment` and `stageTriggerAllBuilds`.
4. Adapt the build logic to match the latest state of the quickstarter
   boilerplates.
5. Remove `verbose: true` config (replace with `debug: true` if you want debug
   output).
6. Configure `branchToEnvironmentMapping`, see README.md. If you used
   environment cloning, also apply the instructions for that.

In `docker/Dockerfile`:
Adapt the content to match the latest state of the quickstarter boilerplates.

In BitBucket, remove the existing "Post Webhooks" and create a new "Webhook",
pointing to the new webhook proxy. The URL has to be of the form
`https://webhook-proxy-$PROJECT_ID-cd.$DOMAIN?trigger_secret=$SECRET`. As
events, select "Repository Push" and "Pull request Merged + Declined".

### Update provisioning app

* Update the OCP resources using Tailor or manually by applying changes as
  appropriate.
* Trigger the build in Jenkins to deploy the latest version.
