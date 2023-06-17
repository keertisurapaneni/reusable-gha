# eks-dependencies

Downloads VM dependencies necessary for deploying to EKS


## Usage:

```
      - name: install dependencies
        uses: lonelyplanet/actions/.github/actions/eks-dependencies@main
```

## Note:

This action installs `kubectl` due to a versioning issue with the `kubectl` that is already existent on the `ubuntu-latest` runners
