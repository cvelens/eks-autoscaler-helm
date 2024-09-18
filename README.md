# Helm Chart for Cluster Autoscaler on Amazon EKS!

This Helm chart deploys EKS Cluster Autoscaler on an Amazon EKS cluster. The Cluster Autoscaler automatically adjusts the number of nodes in a Kubernetes cluster when pods fail to launch due to resource constraints. The cluster autoscaler is bootstrapped and created while creating the EKS cluster using terraform. 

## Prerequisites

Before deploying this Helm chart, ensure you have the following:

- Kubernetes cluster (version 1.25+)
- Helm (version 3.0+) installed

## CI/CD Pipeline
This repository follows a CI/CD process that integrates GitHub and Jenkins using webhooks to trigger automated workflows. The CI/CD process ensures that code quality, chart validation, and versioning are handled automatically before code can be merged and released.

### CI/CD Workflow Overview
#### GitHub -> Jenkins Integration
- GitHub Webhook: A webhook is configured on this repository to trigger Jenkins jobs on specific GitHub events (e.g., pull requests).
- Jenkins Pipelines: There are two Jenkins pipelines (Jenkinsfile1 and Jenkinsfile2) that handle validation, linting, and publishing Helm charts.

#### CI/CD Pipeline Flow
##### Code Validation and Linting (Jenkinsfile1)

- Trigger: Pull requests to the main branch
- This pipeline performs several checks to ensure the quality and validity of the Helm chart and that the commit messages adhere to the Conventional Commits standard before allowing a merge.

##### Helm Chart Publishing (Jenkinsfile2)
- Trigger: Merging a pull request into the main branch
- Once the code passes all validations, and a pull request is merged, this pipeline automatically versions and publishes the Helm chart to GitHub releases.

## Troubleshooting

If you encounter issues:

Check the status of the pods:

```bash
kubectl get pods -n kube-system
```

View the logs of the consumer application:

```bash
kubectl logs -f <autoscaler-pod-name> -n kube-system
```

Check the PostgreSQL logs:

```bash
kubectl logs -f <autoscaler-pod-name> -n kube-system
```