# pipeline-spec-apply

This action modifies a kubernetes manifest and applies it to a cluster.

## Inputs

| Name                  | Required | Description                           | Default |
|-----------------------|----------|---------------------------------------|---------|
| kubeconfig            | True     | Kubernetes config for desired cluster | N/A     |

## Usage:

```
steps:
  - name: Apply manifest
    uses: lonelyplanet/actions/.github/actions/pipeline-spec-apply@main
    with:
      kubeconfig: ${{ secrets.LPO_STAGING_KUBECONFIG }}
      openvpn-config: ${{ secrets.LPO_OPENVPN_CONFIG }}
      openvpn-userpass: ${{ secrets.LPO_OPENVPN_USERPASS }}
```
