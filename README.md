# Turbine deploy GitHub Action

This GitHub Action allow you to deploy your freshly built docker image to your Turbine environments.

## Use this action

### Use case 1: Redeploy your branch to any turbine environment currently on this branch

Add this in your workflow:

```yaml
- name: Turbine Deploy
  uses: adeo/turbine-deploy-action@main  ## Important: replace "main" branch with latest release commit hash
  with:
    token: ${{ env.TURBINE_TOKEN }}
```

When triggered, this step will run the `image_post_build` job with the version corresponding to the current git reference slugged, and the component corresponding to the current github repository name.

All these default variables can be overridden, check the [Inputs](#inputs) section to see all the available parameters.

### Use case 2: Deploy your branch to a specific turbine environment

Add this in your workflow:

```yaml
- name: Turbine Deploy
  uses: adeo/turbine-deploy-action@main  ## Important: replace "main" branch with latest release commit hash
  with:
    token: ${{ env.TURBINE_TOKEN }}
    environment: adeo-myapp-prod  ## replace with your Turbine environment name
```

When triggered, this step will run the `image_deploy` job with the version corresponding to the current git reference slugged, and the component corresponding to the current github repository name.

All these default variables can be overridden, check the [Inputs](#inputs) section to see all the available parameters.


## Inputs

| Input Parameter  | Required | Description |
|:----------------:|:--------:|-------------|
| token       | true   | Specify your Turbine team token |
| version     | false  | The image tag to deploy. Default value to the workflow build branch name slugified. |
| component   | false  | The Turbine component name to deploy. Default value to the repository name. |
| environment | false  | The Turbine environment to deploy. If not given or empty, this Action will redeploy the given component in every environment where it is currently deployed on the given tag. Default to empty. |


