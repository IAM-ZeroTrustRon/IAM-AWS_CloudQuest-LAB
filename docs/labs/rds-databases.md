# Databases in Practice Lab

Secure, available database design for an insurance-company client (MySQL) with
availability and efficiency concerns.

## Objective

Walk the client consultation, configure Amazon RDS for resilience, and plan a
read replica — while navigating account limits gracefully.

## Steps completed

1. **Client consultation** — Dr. Dee Tah, insurance company; MySQL workloads;
   availability and efficiency concerns. Started at 50% client satisfaction.
   ![Client consultation](../images/21-client-consultation.png)
2. **RDS concepts** — Amazon RDS overview; Multi-AZ, backups, storage autoscaling.
3. **Configured RDS resilience:** Multi-AZ "Create a standby instance" option and
   storage autoscaling (maximum 1000 GiB).
   ![Storage autoscaling and Multi-AZ](../images/26-multiaz-autoscaling.png)
4. **Hit an account limitation:** the Multi-AZ standby options were **grayed out**
   (free-tier/lab account limitation) — not a misconfiguration. Worked around it
   via the Practice Checklist / AccessDenied guidance and used Skip on validation.
   ![Grayed out Multi-AZ options](../images/27-multiaz-grayed-out.png)
5. **DIY:** plan a read replica of the primary DB on db.t3.xlarge; identifiers
   `my-database` → `my-database-read-replica`.
   ![DIY read replica](../images/28-diy-read-replica.png)
6. **Completion** — 95% overall client satisfaction.
   ![Completion screen](../images/22-completion-95-percent.png)

## Key takeaways

- Multi-AZ standby + read replicas = availability story for client-facing databases.
- Knowing the difference between "I misconfigured this" and "the account limits
  this" is a real operational skill — the grayed-out options were the latter,
  and the lab flow had a sanctioned workaround.
- Client-facing work counts: satisfaction went from 50% to 95% through clear
  communication of the plan.
