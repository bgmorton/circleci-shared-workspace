# Sharing Data Between Local and Cloud Environments Using CircleCI Workspaces

This repository demonstrates how you can work on data stored locally in cloud CI/CD environments using CircleCI's shared workspaces functionality.

In the example CircleCI configuration, data is created on a self-hosted runner, persisted to a [workspace](https://circleci.com/docs/workspaces/), loaded in a cloud execution environment, and then checked to confirm that the transfer was successful.

### How to run this example

Everything in this example is done within the [CircleCI configuration file](https://circleci.com/docs/config-intro/). The data used to demonstrate persisting and loading data between jobs and environments is all generated using Bash commands defined in the configuration file.

To run this example, you'll need to fork this repository and [create a CircleCI project](https://circleci.com/docs/create-project/) from it.

Then, you will need to update the `RUNNER_NAMESPACE/RUNNER_RESOURCE_CLASS` in the included `.circleci/config.yml` to match the details provided after [setting up your own self-hosted runner](https://circleci.com/docs/runner-overview/). This file contains the complete job and workflow definitions.

### Notes on where persisted data should be stored

Because CircleCI isn't guaranteed control or access to directories outside of the configured [working directory](https://circleci.com/docs/runner-config-reference/#runner-working-directory) we recommend that workspaces be mounted and created within the working directory of the job. Workspaces are not intended for long term storage - only for persisting data between jobs - so make sure you store any data you want kept after your workflow ends outside of your CI/CD infrastructure.

You should also keep in mind potential [usage limits](https://circleci.com/docs/workspaces/#workspaces-and-self-hosted-runner) if you are moving large amounts of data, and [optimize the data](https://circleci.com/docs/workspaces/#workspace-usage-optimization) you are persisting.