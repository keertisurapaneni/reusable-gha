## eks-deploy

Applies a standard workflow similar to what is defined for the Jenkinsfile in [Pipeline Spec v2](https://redventures.atlassian.net/wiki/spaces/LPDP/pages/18257936381/Pipeline+Spec+v2). This uses the standardized `make` targets to build a docker image, run tests, check that it properly responds to requests, and then deploys to the correct EKS cluster. As it stands right now, the workflow only works for deployments that do not require the use of helm.

## Inputs

| Name                  | Required | Description                      | Default                                      |
|-----------------------|----------|----------------------------------|----------------------------------------------|
| image                 | False    | Docker image name                | Repository name (e.g., lonelyplanet/actions) |
| aws-access-key-id     | True     | AWS access key id to be used     | N/A                                          |
| aws-secret-access-key | True     | AWS secret access key to be used | N/A                                          |
| aws-region            | False    | AWS region to be used            | us-east-1                                    |
| cluster               | True     | Name of the cluster              | N/A                                          |
| helm                  | False    | (bool) Does deployment use helm  | false                                        |
| directory             | False    | Directory of k8s application     | .                                            |
| namespace             | False    | Namespace of k8s application     | default                                      |
| policy-arns           | False    | policy ARNs if app uses AWS API  | N/A                                          |

## Usage:

```
name: cicd

on: push

jobs:
  test-and-deploy:
    uses: lonelyplanet/actions/.github/workflows/eks-deploy.yml@main
    secrets:
      aws-access-key-id: ${{ secrets.LPO_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.LPO_SECRET_ACCESS_KEY }}
    with:
      cluster: lonelyplanet-prod

```
## Note:
If your application uses the AWS API or SDK, you must supply the `policy-arns` input with the ARNs of the IAM policies that outline the permissions necessary for the service. These can be user-defined or AWS managed policies. In addition, include the field `serviceAccountName` at the appropriate level in your Kubernetes manifest. Typically, this field will go under 
```
spec:
  template:
    spec:
      serviceAccountName: default
```
It does not matter what value you include after `serviceAccountName: ` as this will be substituted with the appropriate service account name by the workflow using `sed`. This method of granting permissions allows users of the workflow to give their applications AWS permissions without writing any terraform or provisioning anything manual (assuming those policies already exist). In most cases, the necessary policies will already exist through AWS managed policies.
