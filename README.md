# GoIT DevOps CI/CD - Lesson 9

Terraform infrastructure for deploying a CI/CD pipeline on AWS with EKS, Jenkins, and ArgoCD.

## Architecture

- **VPC** — 3 public + 3 private subnets across `eu-central-1`
- **EKS** — Kubernetes cluster (`t2.micro`, 1-2 nodes)
- **ECR** — Container registry for Docker images
- **Jenkins** — CI server deployed via Helm
- **ArgoCD** — GitOps CD tool for automated deployments
- **S3 + DynamoDB** — Terraform remote state backend

## Project Structure

```
.
├── main.tf                 # Root module: providers, module calls
├── backend.tf              # S3 remote backend config
├── outputs.tf              # Root outputs
├── charts/
│   └── django-app/         # Helm chart for Django application
├── modules/
│   ├── s3-backend/         # S3 bucket + DynamoDB for state locking
│   ├── vpc/                # VPC, subnets, IGW, routes
│   ├── ecr/                # Elastic Container Registry
│   ├── eks/                # EKS cluster + node group + EBS CSI
│   ├── jenkins/            # Jenkins Helm deployment + IAM (IRSA)
│   └── argo_cd/            # ArgoCD Helm deployment + custom charts
```

## Usage

```bash
terraform init
terraform plan
terraform apply
```

## Requirements

- Terraform >= 1.0
- AWS CLI configured
- kubectl
