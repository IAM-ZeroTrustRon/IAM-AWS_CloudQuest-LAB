# Database availability and consultation

## Problem

The Databases in Practice exercise explores database availability and operational choices. Only the supplied non-instructional outcome and console screenshots are used here.

## Encountered disabled configuration

The actual RDS form shows disabled Multi-AZ standby choices and a maximum storage threshold of 1000 GiB. The screenshot does not establish the reason for the disabled choices or prove that a configuration was deployed. Account eligibility or configuration prerequisites require separate verification.

![Disabled Multi-AZ standby options](../images/27-multiaz-grayed-out.png)

## Consultation outcome

The simulation reports 95% overall client satisfaction. Its architecture diagram describes the proposed solution; it is not proof that standby or replica resources were created.

![Databases consultation outcome](../images/22-completion-95-percent.png)

## Lessons and remaining evidence

Multi-AZ standby and read replicas address different availability/read-scaling needs. Disabled controls should trigger prerequisite review, not an unsupported assumption about the cause. A learning objective, empty DIY form or architecture diagram is not implementation evidence. Deployment details, running resource state and successful validation are still needed before claiming a completed Multi-AZ or read-replica configuration.
