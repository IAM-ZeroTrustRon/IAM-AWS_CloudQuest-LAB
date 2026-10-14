# AWS Cloud Quest Core Concepts LAB

Hands-on labs in identity & access management, network segmentation, cloud cost
estimation, and database security — documenting real IAM configurations,
troubleshooting, and the problems solved along the way.

> **Note:** All resource identifiers below come from ephemeral AWS lab environments
> (AWS Cloud Quest). They no longer exist, but the steps and outcomes are real.

## The highlight: IAM least-privilege in action

**[Core Security Concepts — IAM lab](./docs/labs/iam-least-privilege.md)**

- Created IAM group **`SupportEngineers`** with the AWS managed policy
  **`AmazonEC2ReadOnlyAccess`** attached (least privilege).
- Created IAM user **`support-engineer-1`**, added it to the group.
- Signed in as the IAM user and verified read-only access works.
- **Proved the control:** attempted an EC2 instance termination as the IAM user →
  denied with **403** (`ec2:TerminateInstances` not allowed). Default-deny working
  exactly as designed.
- DIY extension: attached **`AmazonRDSReadOnlyAccess`** to the group so support
  engineers can view RDS info — validated programmatically.

![IAM 403 denial](./docs/images/44-iam-403-denial.png)
![SupportEngineers group created](./docs/images/35-iam-group-created.png)
![SupportEngineer-1 user created](./docs/images/39-iam-user-created.png)

## Labs

| Lab | What I did | Write-up |
|---|---|---|
| IAM & least privilege | IAM groups, users, managed policies, 403 verification | [iam-least-privilege.md](./docs/labs/iam-least-privilege.md) |
| VPC network segmentation | Route tables, IGW routes, security groups, port 3306 DIY fix | [vpc-network-segmentation.md](./docs/labs/vpc-network-segmentation.md) |
| Cloud cost estimation | Pricing Calculator workload modeling, rightsizing t3 → t2 | [cloud-cost-estimation.md](./docs/labs/cloud-cost-estimation.md) |
| RDS databases in practice | Multi-AZ concepts, storage autoscaling, read replicas | [rds-databases.md](./docs/labs/rds-databases.md) |

## Problems solved

Full troubleshooting log: [problems-solved.md](./docs/problems-solved.md)

- Diagnosed blocked web→DB traffic from an architecture diagram and opened port 3306
  in the DB security group.
- Resolved a confusing AWS session-picker screen when signing in as an IAM user.
- Worked around grayed-out RDS Multi-AZ options (account limitation) without
  breaking the lab flow.
- Used the search-box Enter fix to attach a managed policy in the IAM console.
- Cut a $93.66/mo estimate to $35.26/mo through instance rightsizing.

## Skills demonstrated

- **IAM:** users, groups, managed policies, least privilege, default deny, 403 analysis
- **Networking:** VPCs, route tables, internet gateways, security groups (stateful
  inbound/outbound rules), subnet design (public web / private DB)
- **Cost optimization:** AWS Pricing Calculator, workload-hour modeling, rightsizing
- **Databases:** RDS Multi-AZ, storage autoscaling, read replicas
- **Troubleshooting:** reading error codes, architecture diagrams, and console
  validation states; adapting when lab accounts impose limits

## About me

Career pivoter into cybersecurity — professional background in **healthcare and
clinical workflows**, targeting healthcare-sector security roles where HIPAA-grade
data handling and clinical operations experience is an asset.
