# Deployment Write-up: VM vs App Service

### Analyze, choose, and justify the appropriate resource option for deploying the app

This CMS app is a Flask web application with Azure SQL Database, Azure Blob Storage, user authentication (including Microsoft identity), and straightforward HTTP request/response traffic. For this type of application, both Azure VM and Azure App Service can work, but they differ significantly in operational overhead and scaling model.

#### 1) Cost comparison

**Azure VM**
- You pay for the full virtual machine uptime, attached storage, and any supporting resources.
- OS management effort increases total cost (patching, security hardening, monitoring, backups, and updates).
- Cost efficiency is lower for small-to-medium traffic apps because infrastructure is always running.

**Azure App Service**
- Pricing is tied to App Service Plan tier/instances and is simpler to estimate for web workloads.
- Lower operations burden reduces indirect engineering cost (platform handles much of the runtime hosting and patching).
- Better cost-to-value for this course project because the app is web-only and does not need full OS-level control.

#### 2) Scalability comparison

**Azure VM**
- Scaling usually means resizing the VM or creating additional VMs behind a load balancer.
- Requires more manual setup and operational planning for horizontal scaling.
- Slower to adapt to variable traffic patterns.

**Azure App Service**
- Built-in horizontal/vertical scaling through App Service Plan controls.
- Easier and faster to scale with minimal deployment redesign.
- Better fit for an app where traffic can change and quick scaling is desired.

#### 3) Availability comparison

**Azure VM**
- Availability depends on how well the VM architecture is designed (availability zones/sets, load balancer, health checks, failover design).
- Achieving strong uptime generally requires more infrastructure components and management.

**Azure App Service**
- Platform-managed availability features reduce operational complexity.
- Easy integration with deployment slots and health-oriented deployment workflows.
- Generally offers higher practical reliability for small teams without dedicated infrastructure engineering.

#### 4) Workflow comparison

**Azure VM**
- Team is responsible for server provisioning, runtime setup, patching, process management, and deployment scripts.
- CI/CD can be done, but usually requires more custom scripting and maintenance.

**Azure App Service**
- Supports streamlined deployment workflows (for example, direct GitHub/Azure deployment integration).
- Team can focus on application code and data integration rather than server administration.
- Faster developer iteration cycle for this project’s scope.

### Selected option: Azure App Service

I would deploy this CMS app on **Azure App Service**.

### Justification for App Service

App Service is the better choice because it aligns with this application’s architecture and project goals:
- The app is a standard web workload (Flask + SQL + Blob + auth), which App Service is designed to host efficiently.
- It minimizes infrastructure management and therefore reduces time spent on OS/server tasks.
- It improves delivery speed by simplifying deployments and scaling.
- It provides strong practical availability without requiring a complex VM architecture.
- It is the best balance of cost, scalability, and operational simplicity for a course project and for many small/medium production web apps.

### Assess app changes that would change the decision

I would reconsider and potentially choose **Azure VM** if the app or organization requirements changed in the following ways:
- **Need for deep OS-level control:** custom kernel modules, specialized system services, or strict host-level hardening not supported in App Service.
- **Legacy/runtime constraints:** dependencies requiring non-standard runtime behavior or software that is difficult to host within App Service constraints.
- **Complex networking/security topology:** highly customized network appliances, unusual inbound/outbound routing, or strict enterprise controls requiring full VM control.
- **Non-web co-hosted workloads:** if this solution must run tightly-coupled background daemons or other server processes that are better managed on full virtual machines.
- **Organization operations model:** if the team already has mature VM operations (patching, golden images, automation, incident response) and prefers full infrastructure ownership.

In short, App Service is the best current choice for this CMS app, but VM becomes more attractive when control and customization requirements outweigh platform-managed simplicity.