
## kubernetes-deploy

Applies a standard workflow similar to what is defined for the Jenkinsfile in [Pipeline Spec v2](https://redventures.atlassian.net/wiki/spaces/LPDP/pages/18257936381/Pipeline+Spec+v2). This uses the standardized `make` targets to build a docker image, run tests, check that it properly responds to requests, and then deploys to the correct clusters (based on branch). This is intended to fully replace the Jenkinsfile when implemented.

## Inputs

| Name                  | Required | Description                                                                             | Default                                                          | Notes |
|-----------------------|----------|-----------------------------------------------------------------------------------------|------------------------------------------------------------------|----------|
| main_branch | False | Branch that deploys to prod | main | Deprecated (switch to prod_branch) |
| prod_branch | False | Branch that deploys to prod | master | |
| nonprod_branch | False | Branch that deploys to nonprod | master | |
| pre_deploy_target     | False    | Make target to run before deploying | N/A |
| envvar_name           | False    | Envvar name used to define the environment of the application | N/A |
| skip_nonprod | False | Set to `true` to prevent deploying to nonprod | false |
| skip_prod | False | Set to `true` to prevent deploying to prod | false |
| wiz_scan_fail         | False    | Fail the Wiz scan if there are vulnerabilities | true |
| anvil_fail         | False    | Fail the Wiz scan if there are vulnerabilities | true |


## Secrets
Note: You can just use `secrets: inherit` to inherit the org secrets in the destination repo.


## Usage:

 ```
name: cicd

on: push

jobs:
  test-and-deploy:
    uses: lonelyplanet/actions/.github/workflows/kubernetes-deploy.yml@main
    secrets: inherit
    with:
      main_branch: master
      pre_deploy_target: pre-deploy-assets
      envvar_name: RAILS_ENV
      skip_nonprod: true
```
