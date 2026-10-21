# Architecture (Week 1 design)

## Purpose
A reusable automation solution that provisions AWS resources through code, configures the server, and deploys a demo application.

## Flow
```
Developer (Git / GitHub)
        |
        v
Terraform ----> AWS: VPC + Subnet + Internet Gateway + Security Group + EC2
        |
        v   (EC2 public IP from Terraform output)
Ansible  ----> configures EC2: updates packages, installs Docker, creates directories
        |
        v
Docker   ----> builds and runs the demo app container on EC2
        |
        v
Kubernetes --> Deployment + Service for the demo app (Weeks 7-8)
        |
        v
Bash check script ----> health check, then cleanup with terraform destroy
```

## Responsibilities
| Tool | Responsible for | Not responsible for |
|---|---|---|
| Terraform | Creating and destroying AWS infrastructure | Installing software inside the server |
| Ansible | Server configuration, Docker install | Creating AWS resources |
| Docker | Packaging and running the app | Provisioning |
| Kubernetes | Deploying and exposing the app | Server setup |
| Bash | Ordering the steps, health checks, cleanup | Business logic |

## Planned AWS resources
- 1 VPC with 1 public subnet
- Internet Gateway and route table
- Security group: SSH (22) only from my IP, HTTP (80) for the app
- 1 EC2 instance (Ubuntu, small free-tier eligible type)
- Key pair kept outside Git

## Planned Terraform layout
```
terraform/
  main.tf  variables.tf  outputs.tf  terraform.tfvars.example
  modules/vpc  modules/security-group  modules/ec2
```

## 10-week plan
| Weeks | Focus |
|---|---|
| 1-2 | Requirements, architecture diagram, AWS plan, security and cost estimate |
| 3-4 | Terraform infrastructure, variables, outputs, modules |
| 5-6 | Ansible server setup, Docker app deployment |
| 7-8 | Kubernetes deployment and service, failure and config-error tests |
| 9-10 | Security, cleanup routines, documentation, final demo |

## Diagram
Draw the final diagram in draw.io (diagrams.net), export as PNG, and save it as `docs/architecture.png`.
