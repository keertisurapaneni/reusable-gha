# wiz-scan-notify

This action scans for Docker image vulnerabilities using Wiz and sends Slack notifications when it finds high/critical vulnerabilities.

## Inputs

| Name                  | Required | Description                           | Default                                         | Notes |
|-----------------------|----------|---------------------------------------|-------------------------------------------------|--------------|
| image                 | False    | Docker image name                     | Repository name (e.g., lonelyplanet/actions)    | |
| slack_notify          | False    | Boolean value or condition with boolean value which tells when to send a Slack notification | true |
| slack_channel         | False    | Slack channel to send Wiz failure notification to | N/A | To be used when `slack_notify` is true. |
| wiz_scan_fail         | False    | Fail the Wiz scan if there are vulnerabilities | false |
| SLACK_WEBHOOK         | False    | Slack webhook to use. | N/A | To be used when `slack_notify` is true. You can set it to org secret `${{ secrets.SLACK_WEBHOOK }}` in the workflow. |
| WIZCLI_ID             | True     | Wiz CLI ID for service account | N/A | You can set it to org secret `${{ secrets.WIZCLI_ID }}` in the workflow. |
| WIZCLI_SECRET         | True     | Wiz CLI secret for service account  | N/A | You can set it to org secret `${{ secrets.WIZCLI_SECRET }}` in the workflow. |

## Usage:

```
on:
  workflow_call:
    secrets:
      WIZCLI_ID:
        required: true
      WIZCLI_SECRET:
        required: true
      SLACK_WEBHOOK:
        required: false
steps:
  - name: Wiz scan and Slack notification
    uses: lonelyplanet/actions/.github/actions/wiz-scan-notify@main
    with:
      image: ${{ steps.build.outputs.image }}
      slack_notify: ${{ inputs.deploy }}
      slack_channel: ${{ inputs.slack_channel }}
      SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
      WIZCLI_ID: ${{ secrets.WIZCLI_ID }}
      WIZCLI_SECRET: ${{ secrets.WIZCLI_SECRET }}
```