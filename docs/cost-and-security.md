# Cost and Security Plan (Week 1)

## AWS environment plan
| Item | Choice | Note |
|---|---|---|
| Region | [fill in, e.g. ap-south-1 Mumbai] | Pick one region and use it everywhere |
| Instance type | [fill in, e.g. t3.micro or t2.micro] | Choose one eligible under my account's free plan (check Billing console) |
| OS | Ubuntu LTS | |
| Storage | Default small root volume | |
| Access | SSH key pair, SSH only from my IP | |

## Cost estimate
Exact prices must come from the AWS Pricing Calculator (calculator.aws). Fill the final numbers after checking it.

| Resource | Cost behavior | Plan |
|---|---|---|
| EC2 instance | Free-tier eligible or hourly | Stop or destroy after each session |
| EBS volume | Small monthly charge | Destroyed with the instance |
| Public IPv4 / Elastic IP | Can be billed | Do not leave unattached addresses |
| NAT Gateway | Billed hourly, not free | Avoid; use a public subnet instead |
| EKS control plane | Billed hourly, not free-tier | Do not leave running; use minikube or kind locally for Kubernetes practice where possible |

## Cost controls
1. Create an AWS Budget with an email alert at a low limit.
2. Run `terraform destroy` at the end of every work session.
3. Check the console for leftover resources (EC2, EBS, Elastic IPs) after destroy.
4. Tag every resource with `Project = aws-iac-platform` so cleanup is easy to verify.

## Security plan
1. Do not use the root account for work. Enable MFA on it.
2. Create an IAM user with limited permissions (EC2, VPC) for Terraform. No admin access.
3. Never commit access keys, `*.pem`, `*.tfstate` or `*.tfvars` (covered in `.gitignore`).
4. Store credentials with `aws configure` or environment variables, outside the repo.
5. Security group: SSH only from my IP, never 0.0.0.0/0.
6. Mark sensitive Terraform variables with `sensitive = true`, and never print them in logs.
7. Commit a `terraform.tfvars.example` with safe dummy values only.
