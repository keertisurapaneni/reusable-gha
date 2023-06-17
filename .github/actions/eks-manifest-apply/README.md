# eks-manifest-apply

Applies kubernetes manifest that do not necessitate helm to an EKS cluster

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
steps:
      - name: Apply manifest (without helm)
        if: ${{ !inputs.helm }}
        uses: lonelyplanet/actions/.github/actions/eks-manifest-apply@update-eks-deploy
        with:
          aws-region: ${{ inputs.aws-region }}
          image: ${{ inputs.image }}
          policy-arns: ${{ inputs.policy-arns }}
          directory: ${{ inputs.directory }}
          namespace: ${{ inputs.namespace }}
          aws-access-key-id: ${{ secrets.aws-access-key-id }}
          aws-secret-access-key: ${{ secrets.aws-secret-access-key }}
          cluster: ${{ inputs.cluster }}
```
