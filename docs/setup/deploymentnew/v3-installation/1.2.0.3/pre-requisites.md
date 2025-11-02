# Pre-requisites MOSIP Rapid Deployment
* Before initiating the MOSIP 1.2.0.3 **Rapid Deployment**, ensure that all of the following prerequisites are in place.
* These requirements are essential to guarantee successful and consistent deployment using the automated IaC and Helmsman workflows.
## Cloud Service Provider Account
* An active **cloud account** is required — currently, **AWS** is fully supported.
* Other providers (**Azure**, **GCP**) have placeholder structures defined and can be extended through community contributions.
## User Access & Permissions
* A valid **user** within the same cloud account, with sufficient **IAM privileges** to create and manage resources:
  * VPCs  
  * EC2 Instances  
  * IAM Roles & Policies  
  * Route53 Records
  * Security Groups
## Resource Quota Availability
Ensure your account has adequate resource quotas to provision all required components:
* **VPC and Subnets** (multi-AZ setup)
* **Compute Instances** (for Bastion, Cluster Nodes, NGINX)
* **Elastic IPs** (for public-facing components)
## RSA256 Key Pair
* Generate an **RSA256 key pair** in AWS for secure SSH access to instances.
* The **public key** should be shared within your Terraform variables for node creation.
* The **private key** must be securely stored for administrative or debugging access.
## GitHub Account and Repositories configurations
* A **GitHub account** is needed to fork the MOSIP Infra repositories and manage workflows.
* Access is required to configure **repository secrets** and trigger automated CI/CD actions.
* Fork the [MOSIP Infra Repository](https://github.com/mosip/infra) into your organization’s GitHub space.
* This serves as your base for customizing parameters, secrets, and Terraform variables specific to your deployment environment.
## DNS Mapping
* Domain for accessing MOSIP and external services.
* Ability to create DNA **TXT**, **A** and **CNAME** records for
  * MOSIP core internal services accesible only over wireguard channel.
  * MOSIP Admin & Developer Portals.
  * MOSIP Dashboards accessible over public channel.
  * Monitoring and external services over wireguard channel.
* Use **wildcard certificates** for HTTPS endpoints. (Created using Letsencrypt).
* Since using **Route53**, ensure proper hosted zone mapping and access permissions is already imported.
## Optional Tools (Recommended)
These tools improve visibility and management of the deployment and should be present in deployers PC:
* **git** : for local git repo management.
* **Helm / Helmsman CLI** – for manual overrides or checks.
* **Terraform CLI** – for validating IaC modules.
* **WireGuard Client** – for connecting securely to the private network.
* **kubectl** – for managing and verifying deployed Kubernetes resources.
* **Ansible** - for some optional debugging in case needed.
* **Istioctl** - for service Mesh related checks.
> **Note:** These pre-requisites are mandatory before triggering any pipeline under the Rapid Deployment flow.  
> Missing configurations or resource limits can result in failed deployments or partial infrastructure provisioning.
## Pre-deployment Validation Checklist ✅
Perform the following checks before starting the automated pipelines to ensure a smooth deployment:
| Check | Command / Action | Expected Output |
|-------|------------------|-----------------|
| **AWS CLI Installed** | `aws --version` | Displays AWS CLI version (v2.x recommended) |
| **Logged in to AWS** | `aws sts get-caller-identity` | Returns valid AWS account and user ARN |
| **VPC Quota Check** | `aws ec2 describe-account-attributes --attribute-names vpc-max-count` | Confirms available VPC quota |
| **Key Pair Exists** | `aws ec2 describe-key-pairs --key-names <your-key-name>` | Returns fingerprint of RSA256 key |
| **Route53 Hosted Zone** | `aws route53 list-hosted-zones` | Displays hosted zone ID and domain |

### Optional: Automate Quota Increase for EC2 Instances
* If your AWS account does not meet the required quota to run **7 × t3a.2xlarge** instances, you can automatically request an increase using the AWS CLI:
* Setup AWS credentials into your PC.
  ```
  aws configure
  ```
  * You will be prompted for:
  ```
  AWS Access Key ID [None]: <Your_Access_Key_ID>
  AWS Secret Access Key [None]: <Your_Secret_Access_Key>
  Default region name [None]: <e.g., ap-south-1>
  Default output format [None]: json
  ```
  ✅ Tip: Use the same region that your Terraform deployment will target (e.g., ap-south-1, us-east-1).
* Increase quota using aws cli
  ```bash
  aws service-quotas request-service-quota-increase \
    --service-code ec2 \
    --quota-code L-1216C47A \
    --desired-value 60
  ```
> ⚠️ Note: AWS typically approves quota increases within minutes to a few hours depending on the account’s trust level.
> Ensure the request is approved before running Terraform provisioning.
* You can verify the new limit using:
  ```
  aws service-quotas get-service-quota \
  --service-code ec2 \
  --quota-code L-1216C47A \
  --region <your-region>
  ```
  Look for
  ```
  "Value": 60.0
  ```
