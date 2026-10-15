# AWS Cloud Quest Core Concepts LAB

Hands-on AWS work covering support-user access, network connectivity, cost estimation and database availability concepts. This repository uses original screenshots of console actions and visible outcomes; instructional slides and example screens are excluded.

## Selected lab results

| Lab | Work demonstrated | Evidence and write-up |
|---|---|---|
| Core Security Concepts | Created SupportEngineers, selected its EC2 read-only policy during user creation, and created support-engineer-1 | [IAM access configuration](docs/labs/iam-least-privilege.md) |
| Networking Concepts | Updated routing and security groups; passed the networking DIY validator | [Network segmentation](docs/labs/vpc-network-segmentation.md) |
| Cloud Economics | Revised a calculator estimate from $93.66 to $35.26 monthly | [Cost estimation](docs/labs/cloud-cost-estimation.md) |
| Databases in Practice | Encountered disabled Multi-AZ controls; earned 95% client satisfaction in the consultation | [Database availability review](docs/labs/rds-databases.md) |

## Evidence quality

[Evidence register](docs/evidence-register.md) lists the 15 original images, their scope and hashes. Images appear once in the relevant lab write-up. Console success banners, form selections, calculator estimates and simulation scores are distinct evidence types; none alone proves production effectiveness.

The IAM termination denial and RDS DIY implementation were previously described using instructional screenshots. Those images are removed: the supplied action-only evidence does not independently substantiate those outcomes. They remain evidence gaps, not verified test results.

## Skills and lessons

IAM group membership and managed policies; reading security-group directions and ports; tracing network reachability; calculator workload modeling; distinguishing estimated savings from realized savings; recognizing restricted options; and communicating outcomes without overstating evidence.

[Problems solved and limitations](docs/problems-solved.md) explains troubleshooting and remaining evidence needs. These are sandbox exercises, not a production healthcare audit or proof of HIPAA compliance. AWS managed policies satisfy a training requirement but do not establish the narrowest production access.

## About the author

Ronald Richardson brings behavioral-health and clinical-workflow experience to healthcare GRC and IAM. See the [GRC and IAM project overview](https://github.com/IAM-ZeroTrustRon/GRC-IAM-Portfolio).
