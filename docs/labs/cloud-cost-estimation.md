# Cloud Cost Estimation Lab

Use the AWS Pricing Calculator to estimate and then rightsize a workload.

## Objective

Build a defensible monthly cost estimate for a web server workload, then find
the savings.

## Steps completed

1. **Modeled workload hours** in the Pricing Calculator: Baseline 2, Peak 4,
   8 hrs/day × 7 days.
   ![Estimated workload hours](../images/15-workload-hours.png)
2. **Calculated data transfer**: 1024 GB inbound × $0 = $0; 100 GB outbound ×
   $0.09 = **$9.00/mo**.
   ![Show calculations](../images/16-data-transfer-calc.png)
3. **Initial estimate:** **$93.66/mo** ($1,123.92/12 mo), $0 upfront.
   ![Initial estimate](../images/18-initial-estimate.png)
4. **Rightsized** the instance family from **t3 → t2.micro** (DIY goal).
   New estimate: **$35.26/mo** ($423.12/12 mo), $0 upfront — a **62% cost cut**.
   ![Rightsized estimate](../images/19-rightsized-estimate.png)

## Key takeaways

- Cost estimation is a security-adjacent skill: uncontrolled spend is a business
  risk, and rightsizing is the cheapest "optimization" available.
- The Pricing Calculator's workload-hour model forces you to quantify *usage*,
  not just pick instance types.
