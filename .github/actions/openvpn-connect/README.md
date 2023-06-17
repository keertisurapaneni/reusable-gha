# openvpn-connect

Creates a connection to the LP VPN, so a workflow can access internal LPO resources.

## Inputs

| Name                  | Required | Description                      | Default                                      |
|-----------------------|----------|----------------------------------|----------------------------------------------|
| openvpn-config        | True     | OpenVPN configuration file       | N/A                                          |
| openvpn-userpass      | True     | OpenVPN username/password file   | N/A                                          |


## Usage:

```
steps:
  - name: Connect to OpenVPN
    uses: lonelyplanet/actions/.github/actions/openvpn-connect@main
    with:
      openvpn-config: ${{ secrets.LPO_OPENVPN_CONFIG }}
      openvpn-userpass: ${{ secrets.LPO_OPENVPN_USERPASS }}
  - name: Kill VPN connection
    if: always()
    run: sudo killall openvpn | exit 0
```

**NOTE:** The `Kill VPN connection step` should always be used by the end of the job where this action is used
