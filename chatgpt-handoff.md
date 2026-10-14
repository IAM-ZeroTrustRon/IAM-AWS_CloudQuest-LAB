# ChatGPT Handoff — Cybersecurity Portfolio Project Development

**Purpose:** This file continues an IAM / AWS Cloud Quest cybersecurity portfolio project
conversation that hit a usage limit. Read it, then pick up where the work left off.

---

## 1. Background

- **Who:** Ronald Richardson, a career pivoter into cybersecurity (professional background
  in healthcare and clinical workflows, no professional tech experience yet).
- **What:** A series of AWS Cloud Quest labs used to build a GitHub portfolio project
  demonstrating cybersecurity and IAM capabilities.
- **Source chat:** "Cybersecurity Portfolio Project Development" in Google Gemini
  (gemini.google.com), URL: https://gemini.google.com/app/7fd1c5fb851a7332
- **Current state:** All lab modules below were completed. The chat ended with a Gemini
  usage-limit notice — nothing is broken, the work just needs a continuation home
  (this file) and then packaging into a GitHub portfolio.

## 2. Lab modules completed (in order)

### Module A — EC2 / Instance work
- Completed "Instance ID Step 32": instance `i-00edd388f03a39ece`.

### Module B — Networking Concepts (VPC lab)
- Client consultation ("Step 36") — financial-company network segmentation Q&A.
- VPC lab Steps 37–44, Checkpoints 10–12.
- Resources created/configured:
  - VPC `vpc-0038a8ae943bb557c`
  - RouteTable2 `rtb-07f21772e33265c60` — added IGW routes
  - WebServerSecurityGroup `sg-0e7511947c03ce267` — inbound/outbound rules
    (HTTP/HTTPS/MYSQL outbound)
  - DbServerSecurityGroup `sg-09bdaa38352513e0b` — DIY task: allowed port 3306
    (MySQL/Aurora) inbound into the DB server
- A red-X architecture diagram showed blocked web→DB traffic before the fix; the fix
  connected it.

### Module C — Cloud Economics
- Steps 45–48, Checkpoints 13–14.
- AWS Pricing Calculator estimate id `ae09b8d9194a91000bd6c087538b933991862297`.
- Configured workload hours (Baseline 2, Peak 4, 8 hrs/day × 7 days); data transfer
  calculated at $9.00/mo.
- Initial estimate: $93.66/mo ($1,123.92/12 mo) → rightsized to t2.micro:
  **$35.26/mo ($423.12/12 mo)**.

### Module D — Databases in Practice
- Steps 53–54, Checkpoint 15.
- Client: Dr. Dee Tah (insurance company; MySQL; availability/efficiency concerns).
- 95% client satisfaction score.
- Amazon RDS work: Multi-AZ standby instance, storage autoscaling (1000 GiB max),
  read replicas. DB identifiers: `my-database`, `my-database-read-replica`.
- Problem: Multi-AZ/standby options were grayed out (account/free-tier limitation);
  worked around via the Practice Checklist / AccessDenied guidance and Skip.
  DIY: create a read replica on db.t3.xlarge.

### Module E — Core Security Concepts / IAM lab (the portfolio centerpiece)
- Overview + 7 Learn slides covering: least-privilege IAM groups, the
  `SupportEngineers` group, the `support-engineer-1` user, managed policies
  `AmazonEC2ReadOnlyAccess` then `AmazonRDSReadOnlyAccess`, the default-deny
  principle, and read-only vs. terminate denial.
- Step 55 + 6 Practice slides; reviewed the security-credentials tab (MFA, access keys).
- Step 56: signed in as `support-engineer-1` via the IAM user sign-in page.
  "Which do I choose?" moment on the session screen → clicked **Add session**.
- Step 57: attached `AmazonRDSReadOnlyAccess` to `SupportEngineers` (search-box
  Enter fix used).
- **Verification:** signed in as `support-engineer-1`, attempted an EC2 instance
  termination → correctly **denied with 403** (`ec2:TerminateInstances` not allowed).
  This was the expected proof of least privilege.
- DIY goal: grant the `SupportEngineers` group read-only access to Amazon RDS;
  validation tested that the group had both `AmazonEC2ReadOnlyAccess` and
  `AmazonRDSReadOnlyAccess`.

### Key identifiers (lab environment, ephemeral)
- IAM user: `support-engineer-1`
- IAM group: `SupportEngineers`
- Policies: `AmazonEC2ReadOnlyAccess`, `AmazonRDSReadOnlyAccess`
- IAM user sign-in URL: `https://302300604226.signin.aws.amazon.com/…`
- 403 verification: `ec2:TerminateInstances` denied for
  `arn:aws:iam::…:user/support-engineer-1`
- VPC `vpc-0038a8ae943bb557c`; RTB `rtb-07f21772e33265c60`;
  SGs `sg-0e7511947c03ce267`, `sg-09bdaa38352513e0b`; EC2 `i-00edd388f03a39ece`
- RDS identifiers: `my-database`, `my-database-read-replica`
- Pricing estimate id: `ae09b8d9194a91000bd6c087538b933991862297`

## 3. Problems encountered and how they were solved

1. **Blocked web→DB traffic (VPC lab):** The architecture diagram showed a red X between
   the web server and the database. Fixed by updating `DbServerSecurityGroup` to allow
   inbound MySQL/Aurora (port 3306) — the DIY goal — after which validation passed.
2. **"Which do I choose?" session screen (IAM lab):** When signing in as the IAM user
   `support-engineer-1`, the AWS session picker was confusing. Resolved by clicking
   "Add session" to start a fresh session as the IAM user.
3. **Policy-attachment UX friction (IAM lab, Step 57):** The IAM console policy search
   didn't behave as expected. Resolved by typing `AmazonRDSReadOnlyAccess` and pressing
   Enter to select it.
4. **Grayed-out RDS Multi-AZ standby options:** Account/free-tier limitation, not a
   config error. Worked around via the Practice Checklist / AccessDenied guidance and
   Skip on validation.
5. **The 403 termination error (IAM lab, Step 19/20):** Not a failure — this was the
   *expected* demonstration that least privilege was working (403, `ec2:TerminateInstances`
   not allowed for the read-only user).
6. **Rightsizing cost estimate (Cloud Economics):** Initial $93.66/mo estimate was cut
   to $35.26/mo by switching the instance family from t3 to t2 (t2.micro).

## 4. Suggested next steps

1. Turn the IAM lab into a standalone GitHub portfolio piece (a draft exists at
   `docs/labs/iam-least-privilege.md` in the accompanying folder).
2. Re-export the key screenshots from the Gemini chat and place them in
   `docs/images/` (see `docs/images/PLACEMENT-GUIDE.md` for the mapping).
3. Fill in the Architecture diagram section with a fresh diagram if possible.
4. Draft resume bullets from the "Problems solved" framing in this file.

---

## 5. Screenshot gallery (47 images, in chat order)

> Note: these are direct Google image URLs captured during extraction. They may expire
> over time. If a link breaks, re-export the image from the Gemini chat (see the
> description to identify it) or ask Ronald for a re-upload.

### Networking Concepts / VPC lab

**1. Cloud Quest "Welcome!" simulation intro** — client-consultation instructions, CONTINUE button.
![Cloud Quest Welcome simulation intro](https://lh3.googleusercontent.com/gg/AJWXcNd4WIl0X8Oi8EMkn2UKhi_xv2DuR3GH9cPqM3pMTniuIq5xJZ0_aAB5xEkFQga7TvZBCqnceSBdbe_wkRf0IBOVTqing432blRxP9xnpXsS61oEoVKlTKPGjWbaUGSl_zhQKU25lok_VEBEhuAq5gOyLF9AdNWwhOghbIJUHI_IJKKfbIF8iZPweQnvQrtxwcq4XUda-xTtb8oE073u-mxqtsecYm1LvtFqgIkKV4Fl1ctljx1q_Dd-NNckPEzAvswuLDfk-oG4nmNjzdGW92Z_-SE03deHB3E)

**2. Networking Concepts lab main screen** — VPC diagram: Internet → IGW → router → web server (public subnet) / DB server (private subnet).
![Networking Concepts lab main screen VPC diagram](https://lh3.googleusercontent.com/gg/AJWXcNfBuufjHLXqskskr1R2mfoSvLvZyQXRukAfFPwexagi8cubT6inEzMW3jI4yepWxgyhEptf5bGvF6MxKb87d0w1aoRF9EPmwfgRxdmPUYZ0fW0N0wyOB9MAv_XiWprjNSGSnWrwvLP0L26PR-JyKMuabOcTSjU0Sc20yb0tE6C9h4kjZD6-268o4Z3PKJXIXtA9PP3MukulaJGVyXvJg_Z65jmtNDDvxUYqrd0Vd_pBbY2uM0KXq0R7O_7DdDxFkDrQ-0931cVQcGXdi5Whl9eyTv5MQ-QGSg)

**3. Networking Concepts Practice tab, Step 1/23.**
![Networking Concepts Practice tab Step 1 of 23](https://lh3.googleusercontent.com/gg/AJWXcNe0cfdqBMIwYFC4szyMTNHyT4hwemNcD-3aqa9Rp9lCJ6yhZ9ElgoCJuwr86iVR2a1irOa4ln0yoiGr-CsSpFyif-N6DzRvKgjHOKokT6n3UqEraZp12W0YwWflkcOxh9oFOrnYOpe0VpLoc4NGbsNY2hE2yYXsxiYvLVhimwxySP3obRFLc7UVwe_6VIxp00l6fj6W5rTAxO6xOV387OIoY1VbCiNhrL7slNfuqHUPgk5ABt6wTwluvpV6U1wBZp0oxSi0vcMDcC1-jT8h-uutiEn6uPBZdiU)

**4. Networking Concepts DIY tab** — "DbServerSecurityGroup" typed in the validation field.
![Networking Concepts DIY tab with DbServerSecurityGroup in validation field](https://lh3.googleusercontent.com/gg/AJWXcNe8bc4KuO8zHcSKy-hmpFAxoQZeqMEV7YfEI8o8c3Tz5VeR-h1w3zp9FfyJIPhLcRxfuSSrX1O7GVyT19lDqinzOiUwzjNo5Mn07f5MChb63zSXJ8tIPmz438ExMUSKRUj-cASEhkg5gFpNTZeySafZaT1_7tFxH2j60zIrRO1DbMgQrAKiF-FrIrusBteTThDo5XTw7aa4xeQOrvE5LTEBSvmQnMydSuuySIgilUAgWJUtOo3cABvUQLdQNw7ZKd0Jr2TMypUeG2vDLmCLDkZmEWi6VueKFA)

**5. VPC Console Route Tables** — RouteTable2 with "Updated routes…successfully" banner.
![VPC Console Route Tables RouteTable2 updated routes banner](https://lh3.googleusercontent.com/gg/AJWXcNf19f_xAti1--o3emTDjo3KmTX6OYicLNJfAxVK_eyku09BksXFKYt2SUyvxCVBkvG5yUS5GMVQ42-i7k5pNB0hfzh-bAaQjLJZwICpFvQ8Jo-b3Q7BW-9dkopTWmlqSBdRgv2OVYr1TMBmEaeKYVuf-QqVDJLdZtwHUFhovjcwt4ZZAGQr2feQiusR41u-U5xyBwkOPW6s4lWT73C4mp8hHtcpvfHJ15TszZDeFY6X5CDKv0NgVww6YbZH4pnydbeOD37u6ZjIDW7a8f0Jo9KdvvyPxb2rQ9g)

**6. Networking Concepts Step 11/23** — route table with IGW route.
![Networking Concepts Step 11 route table with IGW route](https://lh3.googleusercontent.com/gg/AJWXcNdZu5nRyK0q2bNg2GHZ9sagTyKfmrVGNProMFpRY0IZLUv41HUgaZYpJ4ti8_V9VxRxbCSo5uKUg4SIsbQsgGysLKgOezOPbCyvOrgP3hlwM-81oOalrDPshqToW0dRUGDobtMDddhf8FsKAEAV9fqZQoVen7xwKGCi-tNXdrhyVPgiV15DnsEUt4x1NrwpTt6ykPdrrtheMcBy2XFVtipIQ6P9GfhGlzlqi_YXkQYVm_7dsKFPefh0vS0GLfod3L8Zb_JYCtvuIvJv2Mkzyl9m-Qx1WmLqEVU)

**7. EC2 Security Groups** — WebServerSecurityGroup (sg-0e7511947c03ce267), inbound-rules success banner.
![EC2 Security Groups WebServerSecurityGroup inbound rules success](https://lh3.googleusercontent.com/gg/AJWXcNcWUtyjf8cZTacZigQrpnGi2wowknIqNrfDJZhORfEfMhcZ8p0EgvFTW-B0Jqi6C4S4tgIIaVHJ7Gayrv4BoeJJC0hEzSabLZSKoTSphN8sgctg-1qfKnsSemVEDXUEhTW0tog5L4ZkffgQ69rKDDJpdtm-7_9h013-H3wTQaij--18WQAZTY0FAk4fGOfY4L3JYeftQNYAxQ8S_bjGsNJWBduG1-hnSt-ZoEwmgLmVjgNY91vE7WXVJWY91BNX4-ZTSq3bsMvWjfokDKbTi4Ug9MaG2mSTpQ)

**8. Same security group** — Outbound rules tab (HTTP/HTTPS/MYSQL outbound rules).
![WebServerSecurityGroup outbound rules tab](https://lh3.googleusercontent.com/gg/AJWXcNe-hOGbgElWFu5rYXpzZGnjWuHGqSTVpVrfmorVPBashNmkguEyfACyFXlwLPKmXijqArdXPH5LJa8YmwbGxlHwF5ygsZ6OtfZ8-JRwYEP6mH-r1y9rxb_tiocKiUvbFhzJzWkHzzD2PVxLhSy-pCoPR-QKDmKSI4zL2ahkHA2Z8zjABtAPpq_8KdFPtz7Wi69B3SRia-q3zOqcl9s9lZvj_aAu_3GKqJUy4VfUEzgukqfOleHurRA1o2ORNHNUfECkYbBX0IQr9T0D3Se8lEwhXiUs7FY2nxA)

**9. EC2 "Edit outbound rules"** — HTTP/HTTPS/MYSQL-Aurora/All-traffic rows; sg-09bdaa38352513e0b in dropdown.
![EC2 Edit outbound rules HTTP HTTPS MYSQL-Aurora rows](https://lh3.googleusercontent.com/gg/AJWXcNfb1xDuT_6pWGvQfSFCFQ_vZEkBDh9mDWzH6b5CKnNuP56Rnw-8fvC_UoNkuxqDGBO6DKsUpbXlAeOIsAEt143VAbo5VJAo8ryJi4345Gntr_ptfUPw4B1IZ0K3UzxVqkPAvhNyrnbnVXRee9P_u_KB9dCOs3lcMIPqxQYyxr_Z96KlJozYTooJfhq3mvYDtjSPLBd7DI8yAGbVmBhGZvseTTtk6NsxojhJze_FeKWbd1v4R3UBSU8AlDcTFYqIbyQo5JcuI5qcBCRx9K5Kj_O80Lqgvy4iKVQ)

**10. Architecture diagram with RED X between Web Server and Database** ("Checking!!!" label) — blocked traffic illustration.
![Architecture diagram with red X between web server and database](https://lh3.googleusercontent.com/gg/AJWXcNdHDCHCqMyWUyv11u3rIYbnDwS0NFDJC8CUrKkmYFkdiaChn2rW1RRE0IdFExmyfeAANe0oN6TcRsVilaiDMGi2gk-qa8FSuYlA9zgv97lLIwe56o_fHurUqXhsL2N-roha_boGomunPjDsKZpdUgxayzjQg86JdWSg3s_ZTOfqIRc2eBBp-Kqq5HARKTPWCJAhWSUweVgjXxLaXtLbtKdiARu9hBFro0WGMn0frxzzqxOYRlqrxM2R-2FCKMvXdt03DYMeUzVI-r4RTAQjk0iIiF_3KDkcg10)

**11. Networking Concepts DIY screen** — goal: change security group rules to allow port 3306 into DB server.
![Networking Concepts DIY screen allow port 3306 into DB server](https://lh3.googleusercontent.com/gg/AJWXcNcPDfJJry99n4RC3QN1LfQ1uVc9JhasJVZt83lw-AyivFVChOyVB344h7rqHKUCIYQcdNYZg3umKzm8d0-U1PaSTd0o2b4dnY59W-eeLE4eeqHYugu1uoYB1QfzsHRX-3O5NH_us3d6owVUv8ni-ac_kiaeML-YHoq4qeroKgt0D3nRw_WoVu7jiZRkQMf3dazaXYS-cwLhoLvt6ITnnwv1IsTZSP5RV-mhy4CVJY3KVcbLF-EF2PiZevbcb-EvIIR2DeZRSsQjfIBLGqAXmdKauXw02idoYrk)

**12. EC2 Security Groups** — DbServerSecurityGroup (sg-09bdaa38352513e0b), "Inbound security group rules successfully modified" banner.
![DbServerSecurityGroup inbound rules successfully modified banner](https://lh3.googleusercontent.com/gg/AJWXcNc5-ete9JD37yJoRU2Wbf8VWF2w0iaI2USfRP88iPohp-oR39Em9ZrsCyVb9iyyn_QVptvPWX0yl6t3EeR4QCVF2JN4ISZKVZAQFySWgKRZGefk8RNGb0ZTuBOWfiW9AwsJiydmxzgLxGWeUGZ8vkOpC1pWEmvbphdK3rIYNljDkDJIrJu3T4hBmheUBr7IKoteDGjdgQt0e5IQNNoMsLq9tu0VA2s_5bg9_Wznu3Y8or9BOvve1chMALbr-MeyYVwMmLtERNDPL2XaQcOym15Bmu6apVQ1VXc)

**13. Cloud Quest "You did it!" popup** — "Congratulations on completing this assignment."
![Cloud Quest You did it congratulations popup](https://lh3.googleusercontent.com/gg/AJWXcNfySooRqR8EZA7CMnD_kcJFa0QzuErZbedmTkKa7dhA3Iq_URJRkYF9hvKcnp1EewFKPoF823A1zHg6g6wH0HzruHINhnhROM1Jk5LvHcb25HxL-yeiXansamFC-XhevaZY5U4bJpDqsHkUNmxpM8_3UJSd0jGK5sb3XvI-XS5iAkAHpbmGb2LiKLTPcOg7dXitC_-m_xxaUPGlZhYcpCSw21WS22Fy-f_8fdb9jaW_K-ud-KrqAj-dyPuosUu9PArNEELG-fvDF3NuI6G4yORa0ZYLYkxiRPg)

**14. Networking Concepts completion screen** — Practice + DIY goals, green connected architecture, feedback stars.
![Networking Concepts completion screen green connected architecture](https://lh3.googleusercontent.com/gg/AJWXcNcsmv78KbmXqEQckrly0wjWO-wd1sti4-DFcWgFmAhRM8c340SQ1HM_I0ZJsCovTMYnPNV3a5ht95uSjKG_1iHJy7JxQjPa9QTygQmLf7Udu0zm1G1uoIo6QvAyBd3RuY3NiM9HcvjRh8LVnsWflyRlPCNws980UYc_dRnvaeMdTYLD4HgroDbgPsCoXaws_a9jUHOkgs4lB76ORVeInaV7rFq3C1ku11xmx_yUXdWt7vC2txFENY0LliZSvpDaRpe1qA-wjGcwytv770eyt3xZfWZlaX5qZaI)

### Cloud Economics

**15. AWS Pricing Calculator "Estimated workload hours" dialog** — Baseline 2, Peak 4, 8 hrs/day × 7 days.
![Pricing Calculator estimated workload hours dialog](https://lh3.googleusercontent.com/gg/AJWXcNfwacOpWuksDjkVu8klJ-FZV8RsbYUKbR9OC2sUEgcmRwipFthz6tIjAbVxikUXMuk9UtYiRJ-nv7gLOXj0Gi6vFfIhgRyuFQ4UITy0wYlLDnWMhsNV0t3k9JIrIMOQ4RErbRS9NOZqQ3Q5Qx6_8kcWIHj3oBU2QKxwCk8SJtmaf4zm6naqey5YIODYjc2z7W6jYPsULFZFwT_opFI1ZZiiQ_rifgeeoBZ2_A-16zhSfUzgEdV1TwQ6934WfB8HytATV0_QOFDyOXpN7EAs2TYLEtMebjBA4jg)

**16. Pricing Calculator "Show calculations"** — Inbound 1024 GB × $0 = $0; Outbound 100 GB × $0.09 = $9.00/mo data transfer.
![Pricing Calculator show calculations data transfer nine dollars](https://lh3.googleusercontent.com/gg/AJWXcNf58PllADqInY3T3wGbmy-jOuAeyIr_2nVU6rMLW-itjkgt1HalbQLb1QMnjfhUbnLMTvXYNENl3o4h_tm2nLNWB0dQJirVb0afqZwWoY1AZzVVcnDNywumMr4mmNX5n3k7Nv0MRScGdAEXIyW6RVC4eeM6ArDQCOmGROJjHxrDcwvgpArl3zr1FFlMkS8ZG7N-DhnQAe1X7F1zrhcAxxACtUqAp-qS1Jwy9P7isOW__FFVDm92iHWUd3HgxKvLPFmxZXgirEX4vOMLFcf5jX-zKVZDvlSs-wk)

**17. Cloud Economics DIY** — goal: change EC2 instance type to t2.micro; hint: family changes t3→t2.
![Cloud Economics DIY change EC2 instance type to t2 micro](https://lh3.googleusercontent.com/gg/AJWXcNfvUy8QhMcWLBCly7_HYB8uVPS3dNMGaCshhbbQ5SpIOlPSkUoZOHT_oELprKOOn0TRK5OnzS-le7LzZL6qMg4isQAUPOIgfhggqjkPH2Xy53qd6uhvCjKSJlzYONaek4EHMeN4BoBarpkme3Pg89yPZz8rpo04DaAu9B5dhfh5vw20cfdE1O7jzsAN7ZMOd0gvdSagXuydSLAxNuQ0XQFdYah944Hk9sof51yHFaRVZl__Q09L2V-vpbFvnWqntAAaZ5fOHNgih00VygQiQ5wUW0vDeMtsDw)

**18. Pricing Calculator estimate summary** — Oct 15, 2026; $0 upfront; $93.66/mo; $1,123.92/12 mo.
![Pricing Calculator estimate summary ninety three sixty six per month](https://lh3.googleusercontent.com/gg/AJWXcNfXr_P0m17cfFPsLqCCABs2TxdXzr3ZlSQzBtS6pC1yx0OS3zek817tGDqvSc9S-Y0iz4F77r7ZnGBkMqhVLdTicloMXhi6laiBCqizN_21Ex4U69oivP6ZOzrxRgPpNQ3hqBVJ-8JkgfdNu6P5sx2rMByKwdjtsGes18Bi8ijq_MsWSCCtb4PktJJLtal3xzwrygRZ2Ua6OSwzTMPNLsM9pzLgCsYortqGGE5Lr7RcTUW-9mHU_9zsje3B1J8kfTLV92V-uLkW2RNKYoufW8-r6hSt9BicwNo)

**19. Pricing Calculator** — "Successfully updated Amazon EC2 estimate." $0 upfront; $35.26/mo; $423.12/12 mo.
![Pricing Calculator successfully updated thirty five twenty six per month](https://lh3.googleusercontent.com/gg/AJWXcNcwt7ttQJrBwp35EdP3c4DFz7LLmBL8nGcUh9FOORqGFBWMo4rZdYdwl_NX73Su8S6WtsDm90zbleAQal1lVZ7X-hl5CxOr9Gzeyta1lfiTzjTRjYJGUHFX7NAHe6spe8jEqAlMlwXVHl3rmaSF7KQwsgq5KxMYoQIKvzrWfHhDBKoZ6R13t7cl1fh7Fyui3ATpwpE8Jr2rFwcG-0zmgJyvbx8PAHeTQwnJOdZyt2Vtyf1qAUKGre1Al-spIM-UUQM5PG7VWVm87dVFjX3Y7-_uliKFDrS580w)

**20. Cloud Quest city** — character facing Penny Singleton; CLOUD ECONOMICS assignment panel.
![Cloud Quest city Penny Singleton cloud economics assignment panel](https://lh3.googleusercontent.com/gg/AJWXcNcp53RY9ASzjOCVO-r7PPoNE9dJ21jed7vDwROE066ZTjwaEgkVGkT0IcxAnGQfySXezY1RH0wNNjQNM4-CONmsy9idl-40y4Ed8K0ecHcAhp8pdk5ZrNOH2BaQ7qH1RzhOFfgmJiVaqxy6QwSTNPvKzrIMos2_MIxKdtFFE8xKkXmL2V5sCeLNA2A9REEE_CkdcODVFL3UL5ls5sho533A6vyagZHw-WUEPBVirfKASQ_HDdi9DawU1CZZcQaUYNKe4rZtdcDiRI03PQJKdFeo71AJsWgcBCE)

### Databases in Practice

**21. Client consultation room** — Dr. Dee Tah (insurance company; MySQL; availability/efficiency concerns); Client Satisfaction 50%.
![Client consultation room Dr Dee Tah insurance MySQL concerns](https://lh3.googleusercontent.com/gg/AJWXcNc5CCVBma31hoRTcGEYJWdDROO97fXmlYWLo4jeRywWP67FfwRPjmLUHEPmd89mYPjeec8fj1WKR-hmDGEdNOUWIgQZL2qbcQtbZtJ574UkEM9lDkVlN3dQa7QROQKE6WX7Yq3UjubJEVbzwhJR3x4Bq72mNVURRCSyM0riizNapi5Pd-EmVTgPPEVBtS9upfaeQ5cZhhkk-81kJQ0IiBI9QeiC0_pNxDAF8X938b_P8ndbwjSFU__0YZsz8uurl-PpVFzDTB8BqGXS47ogUGbApfS0VlVyag)

**22. Completion screen** — 95% Overall Client Satisfaction; Amazon RDS multi-AZ/read-replica diagram.
![Completion screen 95 percent client satisfaction RDS diagram](https://lh3.googleusercontent.com/gg/AJWXcNdq_Dyd3xeDwZylvTxnqaESo8NS_sU5Kw6AqaLE2iljTCqFd6aK_BtXICMND4H37W_-iQurGh4mf0FAg5X2YrDaD4k1r57G3SsYRqso3JZaZH-Nby1h2ZW7N_vQh6UTLNZ4Rf8BtB9fcwl-1c1BrbpZh6fig-lRtAxu30sbB0AyKQk3Erjedkps6DVMSSr9PCivGNHdr0XDOIkig2EJhtEzL6_FpKpD67TKxIVFdNC0ALx8g0R_-lB7EqIXwRZYvEx4FTWKMXvXq1kR9rSptrEBvYXRPXDgUg)

**23. Learn tab — "Amazon RDS Overview" video (1/6); RDS architecture diagram.**
![Learn tab Amazon RDS Overview video RDS architecture diagram](https://lh3.googleusercontent.com/gg/AJWXcNfE0-FFg2Brn2ZAeTmxLV6AiAhAxA7Y7kxVxeR0d_UbncP4Oxevh3CJpjOZybEI-LMg9oAXhTrSEHRRfH-dhPqMACiBrJPtP-LapN07J39s7S-b0WTPwK26UKFaEMxttrzCmyvG1vyE0dgZ2w4RkUc91hP8kziu0aINZY2QP0kjkkRmzDdZX9UkKxY8p0HLPgDbd4bcOkXcllQM5s2hAQhvYpQRmZ5XSYCw48FgXMQuYRNdU-n1jbj824AqrdAshDUnvMU5NWBkEESCnA9vLj5w-hDBIUrHvw)

**24. Practice tab** — concept panel (DB offerings, launch RDS, Multi-AZ, backups); Practice Lab Goals.
![Practice tab concept panel DB offerings launch RDS](https://lh3.googleusercontent.com/gg/AJWXcNfiVEG4cWfFQuGmp_3B_vSKI9jC7esofUgilv2SesgEqRjmzmRfzikmO8HRj6TihgysoJKdfWkQeSJHrAXuWw8OwSpN5khlqnk95APZXxiqgMzbxhOHNx7Ctej1MGDckZ34iyUH9dbYRG38D8EjTjEnG2MJAGiM-j4_Mg-K1iZqcNqO9bkaOuUWtNQKiprdcauZSgtg_0CFW_LINzOlzk04boCnDNF-0NR9C-rRbF_AI3tiUU_mg_g1QLCnNhKDYrthaHllm9zmqWqgPisfhz698I-V4g-i9Fc)

**25. Practice tab Step 1/23** — lab instructions; Start Lab/Open AWS Console guidance.
![Practice tab Step 1 lab instructions start lab](https://lh3.googleusercontent.com/gg/AJWXcNf5Jt_LHFdiySsA_DkrNXYANkT97rlVk2Lhs1UNBNzKEl6-yFi7uTNiG5s90deIiSLB40G96Eur3-zy9FZulrZgQst-UIpeUhU8L9DE-0Y_7i7xYQHBfGH4fTHKvW0ix35gVKmnrSOnYNWdwurWNKijsbIbMihcHwQle5JTA884nVxmBQFrATihGDfXEEn85Va0RqehTYbXu4n5PlGrgTkvtIWHLTQQEdyerHecMwtbDd0SEb6z0EdMl5SaN98PIZozE6jeyescUxokskR538L7-dVL6EZEnDI)

**26. Practice tab Step 12/23** — Multi-AZ: "Create a standby instance"; storage autoscaling defaults.
![Practice tab Step 12 Multi-AZ create standby instance](https://lh3.googleusercontent.com/gg/AJWXcNcTkIUOPqzZv6rG1atY9hDRDPIp7p-gc-RrDGWWD0wdd083CNJhK2i6BKp48idgbErPNkkNXcYCo9Q8fNTEcDgutn-ZAQ-us3q3UlQZyvxsTrgwOjUk32deQyZoPz8pqLL6-tDPZyHiURmLP6gQ2D8wq8jyw8pJJ-QldHxNaFJDtpahcf6n3JIBg7XkQ0ASSK3ZcS_nRYGuGD_1aCBTsXviIRqS-geZMJJsSDcZOMO4QX3XCRPA4L3Tq-ZUDCtuHS14vP1CYtYUSTmLpEJQ-US5J0RrmerLtpE)

**27. RDS "Create database"** — Maximum storage threshold 1000 GiB; Multi-AZ options visibly grayed out/disabled.
![RDS Create database maximum storage 1000 GiB Multi-AZ grayed out](https://lh3.googleusercontent.com/gg/AJWXcNdMXb1OAPnRwFfksqtrME0LtI3Nc2RHeen1p9mdGiWuriXGBHJmVOkQCyTtqxhUmzJGz5mMnx63T9CQyJQhpkrVi1kedyLt3raMTscREhfPW0aHRVZvOT45VXHwPcSMjXfkBj2dr3BDcffiUvTgGW-7sqiK4KoXC1Ol8VCylmmEE_OUDRhg7BYaikkPpZ2dQCT4kgF6fX_S1Tlf0mgQnfxw9YwBk8g5Sas1imcI5Ypi1PHwN2cwBxxXE-vsfHc6Uoudx2D1hn9DiWm0oSyn8j54p-YgoJLQJHc)

**28. DIY screen** — goal: create read replica of primary DB using db.t3.xlarge; RDS read-replica architecture diagram.
![DIY screen create read replica primary DB db t3 xlarge](https://lh3.googleusercontent.com/gg/AJWXcNebXlTb3dRlh5GM0eM-YFB14bGhWImEdG9FBMh_w_MT46jL5A3rFzn4A7zSjYREs_pd5kvvCHWttlNsW6y67RP3rMbzQYfQIegmAqFwSwCHnBqugE794x2TloyLY1NamnstYt-La9m5FxwuQ4JGux6wqB1iiZYMpXCWli_pYavaJUzko8N9syESsRxnOOLK-p6ym8wmPmoPjPNZJWF2odwSrPPrjVL-_EUQnROj2de-OtcXIjo7gSYUINfSLbTvVnBxqQXg8zKLPWLqppCx9AcgMpbRPYEs1qo)

**29. DIY Validation Form** — "Your Amazon RDS DB identifier" and "Your read replica DB identifier" fields; Validate/Skip.
![DIY Validation Form RDS DB identifier read replica fields](https://lh3.googleusercontent.com/gg/AJWXcNeAE_IQV5l8EEYXN2rSFEmLKq9CplDy6THh5agEBmaP-bx9jj9PaLgl1WCLELCAzWaLQtQPIKXal-xDWtLNqgcKXtbC9KiSzvGXXRFs5ewwIfHj0OQw00MrIfOA2HD7_89qCmjdLOorBrDGXu1FicTGkKzMC53E6nJjYhGsqE9z1dMJf6fNiM4pcFjH63hDwb74wuAg1ChRF0AZqc7cLraNp0rwpbZU8Ot6sEu9b8zPDZtvF9fGi2Nuzv3Vl5aVO10D85IszOTdPejoePbVO2X2RGNi7QLV49Y)

### Core Security Concepts / IAM lab

**30. Learn slide 8/8** — diagram: SupportEngineers group + support-engineer-1 → EC2 (green check) + RDS; "Adding an RDS Read-only policy to the group allows SupportEngineers to view Amazon RDS information."
![Learn slide 8 of 8 SupportEngineers RDS read-only policy diagram](https://lh3.googleusercontent.com/gg/AJWXcNcDawnvgZ6573oaIJ5WgSpXi1_gKpJ3N1vwrPqVWieoed0vjqiNdEIebDvdUvXOxpDWESItOKBzYCvvi_8Y-utJKzeu-ep7YdCJkxWrizTmvvA3vzKh_5Y_B2XdzDiQ34xFRFCQKOs6__lw78BFaSpLyDhLbWtpx4pPiibNa5ySr6GQVfovNznSEgbzr-CbxLv4mMLf1jsTTzjxv1AylCFW6HiNpKYdaUxjYOuBzujJThtLs627JzjjQQO1Z_pHIZ3qQStvl3cVoYBnzdZFlT4e8CbcoVbZqv8)

**31. Learn slide 7/8** — same diagram with RED X on RDS; "Following AWS's default deny principle, the SupportEngineers group lacks Amazon RDS read access without explicit permissions."
![Learn slide 7 of 8 default deny principle red X on RDS](https://lh3.googleusercontent.com/gg/AJWXcNcUQAKgU7qsmSqixeYgYqhOF0xGQG8DwRlPbgsZXXgqGgWxVlz0lv0tPFigVLQWkbF7Z_Bi_apF2fC7OAOYafhQ9iGC7xsK6SH_0QkO7CNOccRhqYndqsf08yolW97OUPJcdszY9N0FcZo9AtkvG4XYMIaHJAjxmfeYc42BwHzmrsNdRre2LGC7OqMLkK0cVCDZzwvYOasCY4t_F8fzFZj-uocApjJFbfbhX2SedZVNhE99N3i5tuFYy2zIj1vIJ24BQUhEdeXSiELW8RcSEHYffMmVE3IhX_I)

**32. Learn slide 6/8** — RED X on EC2; "Instance termination attempts result in permission errors, as the policy restricts actions to read-only operations."
![Learn slide 6 of 8 red X on EC2 termination permission errors](https://lh3.googleusercontent.com/gg/AJWXcNdJQSsHI8NWiEKKp-gdtrlsps0zgWEF1157qa7zQ5dZh-gl1d_vJWYQo04GkqWMx5-TvGQbRl3AkAmR_pds30Td521KaUJEt9ljbaX4YS1TCk5sp407cYACo36K3PMC8_dlJqLMG4FPhfpcyfb-bBMAjSQeuWRjR861HQwIUzHNF0s-5Qc0APOdGC9hhIDCdhIBdKOV-NHkXnzGhQtAzEBfQTpCKpolSSdSZDIKwXvA3vjEXAiNUG39s4zUjrAKmcNSXp4zbG0UGLhcnwuIS-aQm1h8cuW2S8Q)

**33. Learn slide 4/8** — "Solution Request: Implement IAM groups with least-privilege permissions…"; "A new IAM user, support-engineer-1, is created and added to the SupportEngineers group, automatically receiving the group's read-only EC2 permissions."
![Learn slide 4 of 8 solution request IAM groups least privilege](https://lh3.googleusercontent.com/gg/AJWXcNey7UTyvR4VBGRimZZBG6lkzkIuNTN8crxHscyh4YNyFfLJmoxx4Gy2bEJ_or4lJrigHnLJn-LX-5bRCE_eqYq0SkRFDiEgzvi6yR0RCX6aUPCB5bkKWiYhSeEm3oHc3PL7eJ3o7oKb7ijkqeBYiyueDHIBEypKlI32sskNrxkxzDRNIIPVUTLoADjLcZBlJ30wlREb5ySFeNJhOgy15n61N6bxkdIGgsM4m9lbYo5tkEzkWIfOAO5QKmZC6F1IAWKTNDW-Ihdb-L_M4BcVz2VKL2lDEdZgu9g)

**34. Learn slide 3/8** — "A read-only access policy for Amazon EC2 is attached to the SupportEngineers group, limiting group members to read-only operations such as viewing instance information." AWS IAM - Manage Permissions button.
![Learn slide 3 of 8 read-only access policy Amazon EC2 attached](https://lh3.googleusercontent.com/gg/AJWXcNcF72pmW2vbzsGf_dR2xoXpjnSSFS9nm-Smr_zZvIdQ6pOnJd8BIBRtEhP_x1tDn610NsOSrNMgT23aWo8xPEdGSz7lUcNg4ZMBGSI0sdX5I_rtyFi8hLnCyIBskzj2-Uw1a-lzlurGCwBszNwQIR_BJGP2nSRKG2Bh7KSDtKkXfOUgMa0i_8F_41gseSj_SOpJHvwEi0sRnTcRhu7YIZQlNDoUFrqlZvH0cUyWQ4i6PFz0MFmzf0NKCFKdaMgSV81u_FZEd4A8cG3Otx5RbASwootlZMrq0XQ)

**35. AWS IAM Console — "IAM user groups"** — green banner "SupportEngineers group created."; table: SupportEngineers, 1 user, 1 permission.
![IAM Console IAM user groups SupportEngineers group created banner](https://lh3.googleusercontent.com/gg/AJWXcNcy1ic11FmXGdVn8lHLoGVeDV0RpfgTYX7xLOvCKdGMxlRFRcygWfKGUTIS7p19cr7NKmDSwKCSIH2ysX0DOLD1EbyJiDMVl3KH2fGHDNTb-dd4PRHZNEvgNglSQP61T7hsHYEF3afrAFxR01rCSdeLRUZcFiYt_eWqXnD3IAj9gmtfF0uQ3lTz29H1miHo2RqVuH4Ijf5uGssnd2RjVYT0WlHcMqfKZiw4h5nRzN9WOiAXZQIoAYHrAwZ3SFWxu-BhacLt8zl1uKfSomRbVQvFGirgcGSSzg)

**36. IAM Console "Create user" Step 3 (Set permissions)** — "Add user to group" selected; SupportEngineers (0 users, AmazonEC2ReadOnlyAccess, created 2026-10-14 14:47).
![IAM Console Create user Step 3 set permissions add user to group](https://lh3.googleusercontent.com/gg/AJWXcNdj6B9BVDhLkJ1BpwpCjddLsXwFgLQWtw0_ZiQ5S2lmtBHXYxxO_ABtHFLVcfxDpbrM5mlHD84EVYXYsSJE2hCbMPaBzNsfcXA5cZBZuPuhM4oGNflMYpOOFINfTBv0GBOyxBccIUJHo7FtuLPqaOQA2qq-myB4eYttc9MWT9_9tvnxHBhWAACYmNscoHCQSCYYfUYhYWF4LGjjeKE5-wOeSFGDz27Pilf-0RPfzyXDjtDupTXXCRBToxiuwMiNQzIF8B-PPCImNscmanVR3LHdI6PWYtOY5l8)

**37. Same "Create user" Step 3 screen** (second screenshot of the same step).
![IAM Console Create user Step 3 second screenshot](https://lh3.googleusercontent.com/gg/AJWXcNdzmb8g4MN4Igvw17phFFdqOCMOLNASgUITHT0o_OA0eZF5zyoaaYkYKPWYGS4FWFkOBjUGTEfAHSuUfY8NS2TsUPNd_niSPznDxE_wMXnVgz5Ltz1W6DQ2B0SlXd5IFaxTO_uc_G2XIwu0_URvy2MMy3I0d9ljg)

**38. IAM Console "Retrieve password"** — green banner "User created successfully"; console sign-in URL, user support-engineer-1, masked console password; "Email sign-in instructions" / "Download .csv file".
![IAM Console Retrieve password user created successfully](https://lh3.googleusercontent.com/gg/AJWXcNdGxa3F1RNkRAFMDNEUWnKQPBrmPvWHQac2xeEiKZbgQbyWw-t8tvqySmDamB3RWmYVHk3eqDhmGU4AhT9omEWz3GTHf5nYT3DF8bxV7VqCmZMpH_H0LNMwPg8lC20k7quUsCeabfAwbUl8Fq4COOKk97rCsmKjmWXg2TNwBp1VQ2Cdc7HGuvokOZqxSmsD_s4I_PCGxztmIgbiLOT1Hk6aBeaOR8BeLQSS1ZsQby_F_KI-yJBMINCoeN6SnjALGpBqsCAlLk21tOJkR0LGLk60EGaOW0jIyjE)

**39. IAM Console "IAM users"** — green "User created successfully" banner; support-engineer-1, Path /, 1 group, Password age "Now".
![IAM Console IAM users support-engineer-1 user created successfully](https://lh3.googleusercontent.com/gg/AJWXcNcFPeHnL_i_OtZqTBQBHwXVoVnfX5_56C2nYI11FK_t1fgdx-7sQIynfv5Hvqxeh1OkvcA8EfajlI7XUkfnCALNobSQl714lTEF6OyFOCYzIGwsapHRv8FYIRHKdIuPeOswOOaVCfHCODfqFygYEqePrIRguMf7HuzpNDp40bzl2HOSqzKZ75T6D92RcXLJpDtWL_lmH8MemxKqUUIh8yxgw6G50PeSrnF9efNcsu3fmIhxV1P6-KCpUZzfSzsT4TfbyJ0h25SqJ7lB528jz2xa_NTlAvLXZug)

**40. IAM Console "IAM users"** — support-engineer-1 selected; Password age "2 minutes" (later state).
![IAM Console IAM users support-engineer-1 password age two minutes](https://lh3.googleusercontent.com/gg/AJWXcNfXQqWR2xrEKCwdgCeWTUZvV_TodT45R_Mj1lyVwJDfDMc6qpFG8Yboce4cLesViGwhqVN-3JE05PYAtr-waxr8LZfwOOk7JRCma9uPvmN1nwjwBmixtcQgmHAEZwyEHjFPdBt989C1msxf4boM9Wv8IjAdS-tE_ZT5sgiRJ5g8mlqItWYeybA1MgF1IDJm0x1pqM3gx7FtNRrQL7S0FCM6zj_j_krTt2_CN1u86YvMsaAHU0MIa2bS1Z0SlXd5IFaxTO_uc_G2XIwu0_URvy2MMy3I0d9ljg)

**41. Practice Step 12/20** — support-engineer-1 "Security credentials" tab: console password last set 2026-10-14 15:48; MFA section (no devices); Access keys (0).
![Practice Step 12 of 20 support-engineer-1 security credentials tab](https://lh3.googleusercontent.com/gg/AJWXcNfDHalgcVlUQCO1lTcbD5m_BXoojCsCpWyqDTYPfhNSvjhDPZr6EtDApYFbKsZ4CkHVYGMS4p2X1VUes6v2Ry3Rhz61wgfbFdl5eq4Beu52zJrvC7RPFr8J-X_yH7r412gU9rnwEdvTdLUX1AzAU3rHjiscdIFTKFPw-aQpDp8cGhZjXpb7eLH7OjbQOp5BQ9vIN7_Hh9NzPlnUcFFiwQ072pODxwq1qu50Wvo-tWc1M3lNxKHf_maAEMF7pK5pYj4XO_uLCmkGsEOnTrcaN8f8J0vbG-303A)

**42. Practice Step 13/20** — AWS IAM user sign-in page: IAM user name "support-engineer-1" filled; instructions to use incognito window + Lab Files password.
![Practice Step 13 of 20 AWS IAM user sign-in page support-engineer-1](https://lh3.googleusercontent.com/gg/AJWXcNfJEAB_b2UHDRlPOYS5V8-iso1l3sTvCxLNExjw7wwdWRvzIX-4O4dYTZ9x422W9-I0Ipw-vN5v-CASO_zK23YWoLN7C-kcWXvnrWOyY9HEHBtHRvU4nqztd8TcOE7uvI5YFrxdxnV93pw6EIjZJMoO0gDq716tftjF9GjRMZzl4mRaznwpOkUDJc4JPrxP5SfdCScoX1VROhEjFSBLOxfvI8rrzmczrwH53qTQ_kmgDrcOQ0JXIkvKZQ95FXzuzmCctmzobSDNwlgmWxY91G2bbHwU7OgFJpA)

**43. AWS "Choose AWS sessions" dialog** — active sessions listed; "Add session" link ("Which do I choose?" moment).
![AWS Choose AWS sessions dialog add session link](https://lh3.googleusercontent.com/gg/AJWXcNcpYs5gh_TR0odlCt3IRvMx8pGIv_xn5FlpM06u_GbYtWCpl1L5jsFDG3GqFoW5uiWV0zsBYXdqh9ISZtPQ_P_c_jV2ghfyHw5137yq8jNgF4mxI_3B25KWrphDsZV-n9a-7R3352KoVNLUjBDQJYT-TAxrJI5wkOBrZ5xqbQ9h5FGXzz4XpNooITc9pQOUr0xHBCKT3Y_HLD5CJkXDrPrMue2huyxM6ZlwADoK0NgfF11xONfGIE12CRqPGjcU8SctcVg0HWE7XsAFCldJQ99mMI6gCmiK-pY)

**44. Practice Step 19/20** — RED error banner: "Failed to terminate EC2 instance. You are not authorized… User: arn:aws:iam::…:user/support-engineer-1 is not authorized to perform: ec2:TerminateInstances… Error code: 403."
![Practice Step 19 of 20 failed to terminate EC2 instance 403 error](https://lh3.googleusercontent.com/gg/AJWXcNeg_lgjITYahnL-mYkVyuOUQC1tiH1hLnvNQ7lp-KXKbY1bQpSIpCwCCPvb-zLceACBCHSvhKe27aYnG6C9UvSxEgE_QbrvaUFynZsfVapmMC0JHv5mXQvSFUYbQZKuvaDUqGlMqeuEeZt0-SGnzOtnDyp1-K0tIY839ln0Bd9l71MQEgxQJTpenpIAqlWd6puAI0rXN7DapxLl75t4wWPyQMDeGsQ361MQEiRbthJacrlLZJ8t65J-geYRjyGjRVzHbZDBYXQavsJ4fH1at37ySB3n5xwBBjM)

**45. DIY screen** — goal: "Grant the 'SupportEngineers' group read-only access to Amazon RDS."; validation: test server verifies SupportEngineers has EC2ReadOnlyAccess + RDSReadOnlyAccess.
![DIY screen grant SupportEngineers group read-only access to Amazon RDS](https://lh3.googleusercontent.com/gg/AJWXcNcIoYRpSUhybWiKT8-xJfjaChsm8uYT1Z5rkq15OEj-096kzecrBOUMi8QxREF_k4QMuGw-wpLXxmUshIEr7u6jlnSg6HWsFGVlvoVt3Q5pcf_4yid2NS41O2g6sLKhDQ5mSU8OBPNHi5cWT8ZmYpCez3eH3LVYrNblVJlWp8T92BGrQHVQXaEg5NXJcg68a-D1oEBkxEzJD09Z3hZTwtd9zwmsabVTZkYE4gcg2jHKqor6-OblQBG6y3W0Au5vrOIwR9tmCXSzNxR02VTZxUWYmUuFBPoRHg8)

**46. DIY Validation Form** — "IAM user group name" = "SupportEngineers"; Validate/Skip; architecture diagram shown.
![DIY Validation Form IAM user group name SupportEngineers](https://lh3.googleusercontent.com/gg/AJWXcNcPO_94mfJpEKrjnNHE1Xo5ay4D-9Y59SpSiTQiLzsQlb2mcE2y_MH9kb1U2MQZSDWFUnT24nSNp5dvG7qtzesEVvMJ55HP8qQrQEWDRGvFzbr39l8vs6e_MLx71a1oJMAlurt1qZHyu69KMreZp2NTx6K4CqoH3o2qilqeP_cexXztElkc4SVfsPSgP_d5AIec7IY3x8D7BDzqoEcWRywP1j4lE5UKyAV7XR35V4B-0DrURTrGW30innD_K8W4PNK2zYYPfARtc2GCuMwmCSR43g8daEndB1w)

**47. DIY Validation Form** — same form, diagram area empty.
![DIY Validation Form SupportEngineers diagram area empty](https://lh3.googleusercontent.com/gg/AJWXcNdNHIccGLPm_FDZR2vgXhE6ERSAjnoh-8zjcf75PPVwcc0Oyc241BJnBTCxccu4BJaj-ABh1EYAWfsTu-JJJresiu_93g4yKQ_iHS4ZKdtEMFDpZbyzqqZvkMjz36xsWhnOEnE0SFhLifH0050hB7mN8b9ffs9xYJWxd-eGU3sBf_4PwNKus_l0g3W8o6tK6b42nRrYZR8gVkCFGkOArhN-QhGoKCbZZW4a9iP8pBxKG1RPpNPB1GteAkxnWPHtUzkJVnTf1ghRYD8fOi63Pr6t8Dsipz-Yn4Q)
