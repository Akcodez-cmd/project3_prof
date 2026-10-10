Project-03: AWS Infrastructure Automation Using Terraform & GitHub Actions 
Objective
Provision AWS infrastructure using Terraform and automate infrastructure deployment through GitHub Actions.
Overall Workflow
GitHub → GitHub Actions → Format → Init → Validate → Plan → Plan Artifact → Approval → Apply → AWS Infrastructure → Outputs → Validation
Terraform Infrastructure
Provision the following AWS resources using Terraform:
VPC
Two Public Subnets
Internet Gateway
Route Table and Associations
Security Group
EC2 Instance
Elastic IP
S3 Bucket
IAM Role and Instance Profile
Expected / Proof: All required AWS resources are provisioned successfully through Terraform. Submit the Terraform configuration and AWS Console evidence of the created resources.
© 2026 GUVI GEEK NETWORK PVT LTD. All rights reserved. No part of this document may be reproduced or transmitted in any
form or by any means, electronic, mechanical, photocopying, recording, or otherwise, without prior permission from GUVI.


Terraform Variables & Outputs
Use Terraform variables for configurable values such as:
AWS Region
Environment
VPC CIDR
Subnet CIDRs
Instance Type
AMI ID
Define outputs for important information such as:
VPC ID
EC2 Instance ID
Elastic IP
Application URL
S3 Bucket Name
Expected / Proof: Infrastructure should be configurable through variables and deployment information should be available through Terraform outputs. Submit the variable/output files and GitHub Actions output evidence.

Reusable Terraform Modules
Create reusable Terraform modules for:
Networking
Compute
Use the modules from the root Terraform configuration.
Expected / Proof: Infrastructure should be provisioned through reusable modules. Submit the module structure and successful Terraform execution evidence.
Remote State & State Locking
Configure Terraform to use:
Amazon S3 for remote state
Terraform-supported state locking
Terraform state must not be committed to GitHub.
Expected / Proof: Terraform must use remote state and state locking successfully. Submit backend configuration, S3 state evidence, and .gitignore.
EC2 Web Server
Configure the EC2 instance using Terraform User Data to:
Install Nginx or Apache
Start the web server
Deploy a custom landing page
Serve the page through the Elastic IP
Expected / Proof: A newly provisioned EC2 instance should automatically become a working web server. Submit User Data configuration and browser evidence of the landing page.
S3 Configuration
Create an S3 bucket with:
Versioning enabled
Encryption enabled
Public access protection
Expected / Proof: The S3 bucket should be securely configured through Terraform. Submit Terraform configuration and AWS S3 Console evidence.
AWS Security
Implement:
IAM Role and Instance Profile for EC2
Least-privilege permissions
Required Security Group access only
No hardcoded AWS credentials
Protected Terraform state
Expected / Proof: AWS access should follow basic security and least-privilege practices without exposing credentials. Submit IAM, Security Group, and Terraform configuration evidence.
GitHub Actions CI/CD
Create a GitHub Actions workflow to automate Terraform deployment.
The workflow must include:
Checkout
Terraform Format
Terraform Init
Terraform Validate
Terraform Plan
Upload Plan as Artifact
Manual Approval
Terraform Apply
Terraform Outputs
Infrastructure Validation
Expected / Proof: A GitHub Actions workflow should successfully execute the Terraform lifecycle and require approval before applying infrastructure changes. Submit the workflow YAML and GitHub Actions run evidence.

Terraform Formatting
Run terraform fmt as part of the GitHub Actions workflow.
Expected / Proof: The workflow should verify that the Terraform configuration follows standard formatting. Submit GitHub Actions execution evidence.
Terraform Initialization & Validation
Run:
terraform init
terraform validate
through GitHub Actions.
Expected / Proof: Terraform should initialize successfully and invalid configurations should prevent the workflow from continuing. Submit GitHub Actions logs.
Terraform Plan & Artifact
Generate a Terraform plan and upload it as a GitHub Actions artifact.
Expected / Proof: A reviewable Terraform plan should be available as a workflow artifact before infrastructure changes are applied. Submit the workflow run and downloadable plan artifact evidence.
Approval Before Apply
Configure the workflow so that Terraform Apply requires manual approval.
Expected / Proof: The workflow must stop after the plan and require an authorized user to approve the deployment before infrastructure changes are applied. Submit GitHub Actions environment/approval evidence.
Terraform Apply
Apply the approved Terraform plan through GitHub Actions.
Expected / Proof: The approved plan should successfully provision the AWS infrastructure. Submit GitHub Actions logs and AWS Console evidence.
Terraform Outputs
Display important Terraform outputs after deployment.
Expected / Proof: The GitHub Actions workflow should display information such as EC2 Elastic IP, application URL, EC2 ID, and S3 bucket name. Submit workflow log evidence.
GitHub Actions Trigger
Configure the workflow to run automatically when changes are pushed to the Terraform repository.
Expected / Proof: A GitHub commit should automatically trigger the Terraform workflow. Submit the commit and corresponding GitHub Actions run evidence.
Infrastructure Validation
Verify:
AWS resources
EC2 instance
Elastic IP
Web server
S3 bucket
IAM Role
Security Group
Terraform outputs
Expected / Proof: The complete infrastructure must be operational and the web server must be accessible through the Elastic IP. Submit AWS Console evidence and the working application URL.
Submission Requirements
Submit:
GitHub Repository
Terraform configuration
Terraform modules
GitHub Actions workflow YAML
.gitignore
README.md
Remote state configuration
Terraform plan artifact
Application URL


