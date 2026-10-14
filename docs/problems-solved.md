# Problems Solved — Troubleshooting Log

Real problems hit during the labs, and how each was resolved.

## 1. Blocked web→database traffic (Networking lab)

- **Symptom:** Architecture diagram showed a red X between the Web Server and the
  Database ("Checking!!!" label). Validation failing.
- **Diagnosis:** The DB tier's inbound rules didn't allow the web tier's traffic —
  a segmentation rule set too tight.
- **Fix:** Updated `DbServerSecurityGroup` (`sg-09bdaa38352513e0b`) inbound rules to
  allow MySQL/Aurora on **port 3306**. Console banner confirmed: "Inbound security
  group rules successfully modified." Validation passed.

## 2. "Which do I choose?" — AWS session picker confusion (IAM lab)

- **Symptom:** After signing in as the IAM user `support-engineer-1`, the "Choose
  AWS sessions" dialog listed multiple active sessions — unclear which one was the
  IAM user's.
- **Diagnosis:** The new IAM-user session needed to be created explicitly rather
  than reusing an existing one.
- **Fix:** Clicked **Add session** to start a fresh session as `support-engineer-1`.
  Lab continued normally.

## 3. Policy-attachment UX friction (IAM lab, Step 57)

- **Symptom:** The IAM console's policy search didn't select
  `AmazonRDSReadOnlyAccess` as expected.
- **Fix:** Typed the policy name in the search box and pressed **Enter** to select
  it. Policy attached to `SupportEngineers`.

## 4. Grayed-out RDS Multi-AZ standby options (Databases lab)

- **Symptom:** "Create a standby instance" / availability options disabled on the
  RDS Create database page (maximum storage threshold 1000 GiB visible, options
  grayed out).
- **Diagnosis:** Account/free-tier limitation, not a configuration error.
- **Fix:** Followed the Practice Checklist / AccessDenied guidance and used **Skip**
  on validation — the sanctioned path — without derailing the lab.

## 5. The 403 termination error (IAM lab, Step 19/20) — expected, not a failure

- **Symptom:** As `support-engineer-1`, terminating an EC2 instance returned:
  *"Failed to terminate EC2 instance. You are not authorized… is not authorized to
  perform: ec2:TerminateInstances… Error code: 403."*
- **Diagnosis:** This was the **proof** the least-privilege design was working —
  read-only policies attached, default-deny enforced, mutating calls fail closed.
- **Fix:** None needed. Documented as verification evidence.

## 6. Oversized cost estimate (Cloud Economics lab)

- **Symptom:** Pricing Calculator estimate of **$93.66/mo** ($1,123.92/yr).
- **Fix:** Rightsized the instance family from **t3 → t2.micro** (DIY goal).
  New estimate: **$35.26/mo** ($423.12/yr) — **62% cheaper**, same modeled workload.
