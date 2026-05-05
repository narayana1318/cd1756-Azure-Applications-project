# Deployment Write-up: VM vs App Service

This CMS app uses Flask + Azure SQL + Blob Storage + Microsoft login.

| Analysis Point | Azure VM | Azure App Service |
|---|---|---|
| Cost | Compute + disk + network + ops are paid continuously; HA adds more cost. | Plan-based pricing is simpler and usually lower ops cost for web apps. |
| Scalability | Scale up by larger VM; scale out needs multiple VMs + load balancer. | Built-in scale up/out and autoscale with less setup effort. |
| Availability | Needs manual HA design (zones/sets, LB, failover, patching). | Platform-managed availability features reduce downtime risk. |
| Workflow | Team manages OS patches, security, runtime, and deployments. | Team focuses on app code and CI/CD, with less server maintenance. |

Example cost (approx): VM B1ms ~$10–$25 (+extras), App Service B1 ~$10–$20.
Prices vary by region; use Azure Pricing Calculator for exact values.

**Chosen option: Azure App Service**

I choose App Service for this project.
It fits a standard Flask web app, is easier to scale, and reduces infrastructure work.
It gives a better balance of cost, reliability, and delivery speed for a small team.

**When I would choose VM instead**

I would switch to VM if we need full OS/server control.
Examples: custom system software, strict enterprise network controls, or legacy runtime constraints.
In those cases, VM flexibility can justify higher operations effort and cost.