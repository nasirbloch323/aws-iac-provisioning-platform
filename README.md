# AWS IaC Provisioning Platform

Infrastructure as Code & Automated Environment Provisioning Platform
CypherNex DevOps Internship, Project 2. Intern: Nasir Mehmood.

## Goal
Provision AWS infrastructure through code instead of manual configuration, configure the server automatically, and deploy a demo application. The whole setup must be reproducible from a clean checkout.

## Tool stack
| Tool | Role |
|---|---|
| Terraform | Provisions AWS resources (VPC, subnet, security group, EC2) |
| Ansible | Configures the server (packages, Docker, directories) |
| Docker | Containerizes and runs the demo app |
| Kubernetes | Deploys the app as a Deployment and Service (Weeks 7-8) |
| Bash / Python | Setup, checks and cleanup scripts |
| Git / GitHub | Version control and evidence |

## Workflow
Terraform apply -> Ansible playbook -> Docker build and run -> Kubernetes deploy -> health check -> cleanup (`terraform destroy`)

## Repository structure
```
terraform/   Terraform config, modules, variables, outputs
ansible/     inventory and playbooks
app/         demo application and Dockerfile
k8s/         Kubernetes manifests
scripts/     setup.sh, check.sh, cleanup.sh
docs/        architecture, cost and security, troubleshooting
evidence/    weekly reports, screenshots, test output
```

## Status
- Week 1: requirements, architecture and AWS planning (done)
- Week 2 onward: see docs/architecture.md

## Prerequisites (versions to be recorded in Week 2)
- Git, Terraform CLI, AWS CLI, Ansible, Docker
- An AWS account with a limited-permission IAM user

## Security rules
- Never commit passwords, private keys, access keys, `*.tfstate` or `*.tfvars`.
- Use `terraform.tfvars.example` for safe sample values.
- Destroy resources after each test session to avoid charges.

