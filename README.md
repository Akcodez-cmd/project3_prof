# Project-03: AWS Infrastructure Automation Using Terraform & GitHub Actions

## 📌 Project Overview

This project demonstrates the provisioning and automation of AWS infrastructure using **Terraform** and **GitHub Actions**. It follows Infrastructure as Code (IaC) principles to create secure, reusable, and configurable AWS resources through an automated CI/CD workflow.

The deployment process includes Terraform formatting, initialization, validation, planning, plan artifact generation, manual approval, infrastructure deployment, and post-deployment validation.

## 🎯 Objectives

- Automate AWS infrastructure provisioning using Terraform.
- Implement CI/CD automation using GitHub Actions.
- Create reusable Terraform modules for networking and compute.
- Configure remote Terraform state using Amazon S3 and state locking.
- Deploy a custom web page on an EC2 instance using User Data.
- Implement basic AWS security and least-privilege access.
- Require manual approval before applying infrastructure changes.
- Validate deployed resources and expose important Terraform outputs.

## 🏗️ Architecture & Workflow

```text
Developer
    |
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    v
Checkout Source Code
    |
    v
Terraform Format
    |
    v
Terraform Init
    |
    v
Terraform Validate
    |
    v
Terraform Plan
    |
    v
Upload Plan Artifact
    |
    v
Manual Approval
    |
    v
Terraform Apply
    |
    v
AWS Infrastructure
    |
    v
Terraform Outputs
    |
    v
Infrastructure Validation
```

## ☁️ AWS Resources

The following resources will be provisioned and managed through Terraform:

| Resource | Purpose |
|---|---|
| VPC | Isolated AWS network |
| Two Public Subnets | Host resources across two subnets |
| Internet Gateway | Provide internet connectivity for eligible public resources |
| Route Table & Associations | Route subnet traffic |
| Security Group | Control inbound and outbound traffic |
| EC2 Instance | Host the web application |
| Elastic IP | Provide a stable public IPv4 address |
| S3 Bucket | Store application-related data and Terraform remote state |
| IAM Role | Provide AWS permissions to EC2 |
| IAM Instance Profile | Attach the IAM role to EC2 |

## 🧰 Technology Stack

- **Cloud Provider:** Amazon Web Services (AWS)
- **Infrastructure as Code:** Terraform
- **CI/CD:** GitHub Actions
- **Version Control:** Git & GitHub
- **Web Server:** Nginx or Apache
- **Compute:** Amazon EC2
- **Networking:** Amazon VPC, Subnets, Internet Gateway, Route Tables
- **Storage:** Amazon S3
- **Security:** AWS IAM, Security Groups, S3 encryption and public access protection

## 📁 Project Structure

```text
project-03/
├── .github/
│   └── workflows/
│       └── terraform.yml
├── modules/
│   ├── networking/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── compute/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── bootstrap/
│   └── main.tf
├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── backend.tf
├── terraform.tfvars.example
├── .gitignore
└── README.md
```

*Note: This is the planned structure. Update it to match the actual files and folders in the repository. The `bootstrap/` directory is intended for creating the S3 backend resources before configuring remote state, if required.*

## ⚙️ Terraform Configuration

### Variables

Terraform variables will be used to configure:

- AWS Region
- Environment
- VPC CIDR
- Public Subnet CIDRs
- EC2 Instance Type
- AMI ID

Sensitive information must not be committed to the repository.

### Outputs

Terraform will expose important deployment information, including:

- VPC ID
- EC2 Instance ID
- Elastic IP
- Application URL
- S3 Bucket Name

## ♻️ Reusable Terraform Modules

The project will use reusable Terraform modules to organize infrastructure configuration.

- **Networking Module:** VPC, public subnets, Internet Gateway, route table, route associations, and security group.
- **Compute Module:** EC2 instance, Elastic IP, IAM role, and instance profile, where appropriate.

The root Terraform configuration will call these modules to provision the required infrastructure.

## 🗄️ Remote State & State Locking

Terraform remote state will be configured using Amazon S3.

The backend configuration will support:

- Centralized Terraform state storage.
- S3 bucket versioning for state recovery.
- Encryption at rest.
- Terraform-supported state locking.
- Restricted access to the state bucket.

The S3 backend must be created before Terraform can initialize against it. Backend resources should be bootstrapped separately when necessary.

**Important:** Terraform state files and sensitive plan files must not be committed to GitHub.

## 🌐 EC2 Web Server Deployment

The EC2 instance will use Terraform User Data to automate initial server configuration.

The initialization script will:

1. Install Nginx or Apache.
2. Enable and start the web server.
3. Deploy a custom HTML landing page.
4. Configure the server to serve the page over HTTP.
5. Make the application accessible through the Elastic IP.

The web server will be tested using the application URL after deployment.

## 🪣 S3 Bucket Security

The S3 bucket will be configured with:

- Versioning enabled.
- Server-side encryption enabled.
- All public access blocked.
- Restricted access through IAM policies.
- Remote state protection where the bucket is used for Terraform state.

## 🔐 AWS Security Best Practices

- Use IAM roles and instance profiles instead of static AWS credentials on EC2.
- Apply least-privilege IAM permissions.
- Restrict Security Group inbound rules to required ports and trusted sources where possible.
- Avoid hardcoding AWS credentials.
- Store GitHub Actions AWS credentials securely using GitHub Secrets or use GitHub OIDC with an appropriately restricted IAM role.
- Protect Terraform state and restrict access to backend resources.
- Require manual approval before production infrastructure changes.
- Avoid exposing sensitive Terraform outputs in workflow logs.

## 🚀 GitHub Actions CI/CD Pipeline

The GitHub Actions workflow will automate the Terraform deployment lifecycle.

| Stage | Description |
|---|---|
| Checkout | Retrieve repository code |
| Format | Verify Terraform formatting using `terraform fmt -check -recursive` |
| Init | Initialize Terraform and the configured backend |
| Validate | Check Terraform configuration |
| Plan | Generate an execution plan |
| Plan Artifact | Upload the plan for review |
| Approval | Require authorization through a protected GitHub Environment |
| Apply | Apply the approved plan |
| Outputs | Display important deployment outputs |
| Validation | Verify AWS resources and web application availability |

The workflow will run automatically when changes are pushed to the configured branch. The apply stage will require approval from an authorized reviewer.

The saved plan must be securely transferred to the apply job and applied using the reviewed plan file. The plan artifact should have restricted access and a limited retention period.

## 🧪 Infrastructure Validation

After deployment, verify the following:

- [ ] VPC and two public subnets are created.
- [ ] Internet Gateway and route table associations are configured.
- [ ] Security Group rules are correct.
- [ ] EC2 instance is running.
- [ ] Elastic IP is associated with the instance.
- [ ] Nginx or Apache is running.
- [ ] Custom landing page is accessible through the application URL.
- [ ] S3 bucket versioning and encryption are enabled.
- [ ] S3 public access is blocked.
- [ ] IAM role and instance profile are attached correctly.
- [ ] Terraform remote state and state locking work successfully.
- [ ] Terraform outputs are available in GitHub Actions logs.
- [ ] GitHub Actions runs automatically after a repository push.
- [ ] Manual approval is required before Terraform Apply.

## 🛠️ Local Terraform Commands

Run the following commands from the Terraform root directory.

```bash
terraform fmt -recursive
terraform init
terraform validate
terraform plan
```

To deploy manually, when authorized and appropriate:

```bash
terraform apply
```

To display deployment outputs:

```bash
terraform output
```

To inspect the deployed infrastructure:

```bash
terraform state list
```

Terraform commands that interact with remote state require the backend to be configured and accessible.

## 🧹 Resource Cleanup

To avoid unnecessary AWS charges, review and destroy resources when the project is no longer required.

```bash
terraform plan -destroy
terraform destroy
```

Run destruction only after confirming that the resources are no longer needed. Protect any resources containing important data, and handle the remote state backend separately if it must be retained.

## 📸 Evidence & Deliverables

The final submission will include:

- [ ] GitHub repository URL.
- [ ] Terraform root configuration.
- [ ] Networking and compute module files.
- [ ] GitHub Actions workflow YAML.
- [ ] `.gitignore` and `README.md`.
- [ ] Remote state backend configuration.
- [ ] Terraform plan artifact evidence.
- [ ] GitHub Environment manual approval evidence.
- [ ] Successful GitHub Actions execution logs.
- [ ] AWS Console screenshots of provisioned resources.
- [ ] Terraform outputs evidence.
- [ ] Browser screenshot of the working landing page.
- [ ] Application URL.

## 🔗 Project Links

- **GitHub Repository:** `Add your repository URL here`
- **Application URL:** `Add your Elastic IP or application URL here`

## 📌 Project Status

**Status:** In Progress

This project will be marked complete after successful infrastructure provisioning, approval-controlled CI/CD deployment, remote state verification, and post-deployment validation.

---

**Project:** AWS Infrastructure Automation Using Terraform & GitHub Actions  
**Purpose:** DevOps learning project demonstrating Infrastructure as Code, CI/CD automation, AWS infrastructure provisioning, and security best practices.
