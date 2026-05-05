# 2. Azure Services & Products

## Azure Service Categories

### Compute Services 🖥️

| Service | Type | Use Case |
|---------|------|----------|
| **Virtual Machines (VMs)** | IaaS | Full OS control, Windows/Linux |
| **App Service** | PaaS | Web apps, APIs, mobile backends |
| **Azure Functions** | Serverless | Event-driven, pay-per-execution |
| **Container Instances** | Serverless | Quick container deployment |
| **Kubernetes Service (AKS)** | Managed K8s | Large-scale container orchestration |
| **Batch** | Compute | High-performance parallel processing |
| **Service Fabric** | Microservices | Complex distributed applications |

**Exam Focus:** VM vs App Service (VM = more control, App Service = easier)

---

### Storage Services 💾

| Service | Purpose | Use Case |
|---------|---------|----------|
| **Blob Storage** | Object storage | Large files, archives, backups |
| **File Shares** | Network shares | Like SMB/NFS but in cloud |
| **Queue Storage** | Message queue | Async messaging between apps |
| **Table Storage** | NoSQL | Fast key-value lookups |
| **Disk Storage** | VM disks | OS and data disks for VMs |

**Tiers:** Hot (frequent access) > Cool (infrequent) > Archive (rare, cheapest)

---

### Database Services 🗄️

| Service | Type | Best For |
|---------|------|----------|
| **SQL Database** | Relational | Structured data, ACID compliance |
| **Cosmos DB** | NoSQL | Global, multi-model data |
| **Database for PostgreSQL** | Relational | Open-source PostgreSQL |
| **Database for MySQL** | Relational | Open-source MySQL |
| **Cache for Redis** | In-memory | Caching, sessions, real-time data |

---

### Networking Services 🌐

| Service | Purpose |
|---------|---------|
| **Virtual Network (VNet)** | Isolated network environment |
| **Load Balancer** | Distribute traffic across VMs |
| **Application Gateway** | Layer 7 load balancing |
| **Azure Front Door** | Global load balancing + CDN |
| **Content Delivery Network (CDN)** | Cache content worldwide |
| **VPN Gateway** | Secure site-to-site VPN |
| **Express Route** | Dedicated private network link |

---

### Analytics & Big Data 📊

| Service | Purpose |
|---------|---------|
| **Synapse Analytics** | Data warehouse + analytics |
| **Data Lake Storage** | Big data storage |
| **Stream Analytics** | Real-time data processing |
| **Power BI** | Business intelligence/dashboards |
| **Databricks** | Apache Spark analytics |

---

### AI & Machine Learning 🤖

| Service | Purpose |
|---------|---------|
| **Cognitive Services** | Pre-built AI APIs (vision, language) |
| **Machine Learning** | Build custom ML models |
| **Bot Service** | Build chatbots |

---

### Integration Services 🔗

| Service | Purpose |
|---------|---------|
| **Logic Apps** | Workflow automation |
| **API Management** | Publish, manage, monitor APIs |
| **Service Bus** | Enterprise messaging |
| **Event Grid** | Event routing |

---

### Management & Governance 🎯

| Service | Purpose |
|---------|---------|
| **Azure Monitor** | Monitoring and logging |
| **Azure Advisor** | Cost & performance recommendations |
| **Azure Policy** | Enforce compliance rules |
| **Resource Manager** | Deploy and manage resources |
| **Cost Management** | Track spending |

---

## Resource Organization

### Resource Groups
- **Logical container** for resources in a region
- All resources must belong to one RG
- Easy to manage/delete together
- Scope for permissions

### Subscriptions
- **Billing boundary**
- Manage access, quotas, policies
- Can have multiple per account

### Regions & Availability Zones
- **Region:** Geographic area with data centers
- **Availability Zone:** Physically separated data centers (within same region)
- **Data residency:** Data stays in chosen region (with exceptions)

---

## Azure Management Tools

| Tool | Use |
|------|-----|
| **Azure Portal** | Web UI for everything |
| **Azure CLI** | Command-line tool |
| **PowerShell** | Windows scripting |
| **Visual Studio Code** | Code editor with Azure extension |
| **Cloud Shell** | Browser-based terminal |

---

## Key Exam Tips

- **Know the tiers:** Hot > Cool > Archive (cost increases in reverse)
- **Blob vs Files:** Blob = large objects, Files = shared network folders
- **VM vs App Service:** VMs require more management, App Service is PaaS
- **CDN:** Caches content at edge locations worldwide ([Azure CDN](https://azure.microsoft.com/en-us/services/cdn/))
- **Regions:** You choose where data lives (compliance matters)

---

## CDN Reference

Azure CDN edge locations cache content worldwide:

![CDN Diagram](https://cdnjs.cloudflare.com/ajax/libs/material-design-icons/7.2.96/svg/content/content_copy.svg)

**Reference:** [Azure CDN Documentation](https://docs.microsoft.com/en-us/azure/cdn/)
