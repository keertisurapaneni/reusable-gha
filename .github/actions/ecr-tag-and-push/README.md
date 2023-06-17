# ecr-tag-and-push

This action takes a docker image, and tags it with the branch name, and short (7 characters) commit SHA, then pushes the image with both tags to ECR.

## Inputs

| Name                  | Required | Description                      | Default                                      |
|-----------------------|----------|----------------------------------|----------------------------------------------|
| image                 | False    | Docker image name                | Repository name (e.g., lonelyplanet/actions) |
| aws-access-key-id     | True     | AWS access key id to be used     | N/A                                          |
| aws-secret-access-key | True     | AWS secret access key to be used | N/A                                          |
| aws-region            | False    | AWS region to be used            | us-east-1                                    |


## Usage:

```
steps:
  - name: build
    run: docker image build -t lonelyplanet/actions .
  - name: push
    uses: lonelyplanet/actions/.github/actions/ecr-tag-and-push@main
    with:
      aws-access-key-id: ${{ secrets.LPO_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.LPO_SECRET_ACCESS_KEY }}
```
