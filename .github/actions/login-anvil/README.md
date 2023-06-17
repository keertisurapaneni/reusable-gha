# login-anvil

Logs into ECR Anvil, so a workflow can access RV approved container images

## Inputs

| Name                  | Required | Description                      | Default                                      |
|-----------------------|----------|----------------------------------|----------------------------------------------|
| aws-access-key-id     | True     | AWS access key id to be used     | N/A                                          |
| aws-secret-access-key | True     | AWS secret access key to be used | N/A                                          |


## Usage:

```
steps:
  - name: login anvil ecr
    uses: lonelyplanet/actions/.github/actions/login-anvil@main
    with:
      aws-access-key-id: ${{ secrets.aws-access-key-id }}
      aws-secret-access-key: ${{ secrets.aws-secret-access-key }}

  - name: build
    run: make build
```
