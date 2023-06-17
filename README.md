# Actions

This repo is a collection of Github actions and reusable workflows.

### Workflows

Reusable workflows exist in `.github/workflows`. The `README.md` there should contain more details about each workflow, but these are the available workflows:

| Name | Purpose |
|------|---------|
| kubernetes-deploy | This acts as a pipeline to deploy to LPO kubernetes clusters, replacing Jenkinsfile pipelines |
| eks-deploy | Deploy kubernetes application to an EKS cluster |
| ecs-deploy | Deploys application to ECS |

### Actions

Actions exist in `.github/actions` with each subdirectory containing an `action.yml` and a `README.md` giving detailed usage of each action. Here are brief descriptions of each action:

| Name | Purpose |
|------|---------|
| ecr-tag-and-push | Tags a docker image with standardized tags and pushes to ECR |
| openvpn-connect | Establishes a connection to the LPO VPN |
| pipeline-spec-apply | Modifies a kubernetes manifest and applies it to a cluster |
| login-anvil | Logs into anvil ECR in order to pull images from RV container image pipeline |
| eks-dependencies | Downloads VM dependencies necessary for an EKS deploy |
| eks-manifest-apply | Applies k8s manifests that do not require helm to an EKS cluster |
| wiz-scan-notify | Scans a Docker image for vulnerabilities and sends Slack notifications for high/critical vulnerabilities |
