
# Azure Services & Products

[![AZ-900](https://img.shields.io/badge/AZ--900-Domain%202-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-35--40%25-f59e0b?style=flat-square)]()

The largest exam domain. You need to know **what each service does** and **when to pick it over alternatives**.

---

## Compute

| Service | Type | Pick it when… |
|---|---|---|
| **Virtual Machines** | IaaS | Need full OS control, custom software |
| **App Service** | PaaS | Web app / API, don't want to manage OS |
| **Azure Functions** | Serverless | Event-triggered code, pay per execution |
| **Container Instances (ACI)** | Serverless containers | Run a container fast, no orchestration |
| **Kubernetes Service (AKS)** | Managed K8s | Many containers, auto-scaling, microservices |
| **Virtual Machine Scale Sets** | IaaS | Many identical VMs with auto-scale |
| **Azure Batch** | HPC | High-volume parallel processing jobs |

{: .tip }
**Exam:** VM = you manage OS. App Service = Microsoft manages OS. Functions = pay only when code runs.

---

## Storage

```
Blob Storage          File Shares           Queue Storage
─────────────         ─────────────         ─────────────
Large objects         Network shares        Async messages
Images, video         Like SMB/NFS          Between services
Unstructured          Structured file       Max 64KB/msg

Access tiers:         Mount from:           Use with:
Hot → frequent        Windows, Linux        Functions, Apps
Cool → monthly        macOS                 Workers, Logic Apps
Archive → rarely
```

### Blob Access Tiers

| Tier | Storage Cost | Retrieval | Use |
|---|---|---|---|
| **Hot** | Highest | Instant | Accessed daily |
| **Cool** | Medium | Instant | Accessed monthly |
| **Archive** | Lowest | 1–15 hours | Accessed yearly |

{: .tip }
**Exam:** Moving from Hot → Archive is instant. *Retrieving* from Archive takes up to 15 hours (rehydration).

---

## Databases

| Service | Type | Use |
|---|---|---|
| **Azure SQL Database** | Relational (SQL Server) | Structured data, ACID compliance |
| **Azure Database for PostgreSQL** | Relational (open source) | PostgreSQL workloads |
| **Azure Database for MySQL** | Relational (open source) | MySQL workloads |
| **Cosmos DB** | NoSQL, multi-model | Global distribution, flexible schema |
| **Azure Cache for Redis** | In-memory | Session state, caching, real-time |

{: .tip }
**Exam:** Cosmos DB = globally distributed, low latency, NoSQL. SQL Database = structured, relational, ACID.

---

## Networking

| Service | Purpose |
|---|---|
| **Virtual Network (VNet)** | Isolated private network in Azure |
| **Load Balancer** | Layer 4 (TCP/UDP) traffic distribution |
| **Application Gateway** | Layer 7 (HTTP/HTTPS), URL routing, WAF |
| **Azure Front Door** | Global load balancing + CDN + WAF |
| **VPN Gateway** | Site-to-site VPN over internet |
| **ExpressRoute** | Private dedicated connection (not internet) |
| **Content Delivery Network (CDN)** | Cache content at edge locations globally |
| **DNS** | Host your domain in Azure |

{: .tip }
**Exam:** Load Balancer = Layer 4 (ports). Application Gateway = Layer 7 (URLs). ExpressRoute = private, not internet.

---

## AI & Machine Learning

| Service | What it does |
|---|---|
| **Azure AI Services (Cognitive Services)** | Pre-built AI APIs — vision, speech, language, decision |
| **Azure Machine Learning** | Build, train, deploy custom ML models |
| **Azure Bot Service** | Build and host chatbots |
| **Azure OpenAI Service** | GPT models via API |

---

## Management & Monitoring

| Service | Purpose |
|---|---|
| **Azure Monitor** | Centralised metrics, logs, alerts |
| **Azure Advisor** | Personalised cost, security, reliability tips |
| **Azure Policy** | Enforce rules across resources |
| **Cost Management** | View and optimise spending |
| **Resource Manager (ARM)** | Deploy and manage resources via templates |
| **Azure Arc** | Manage non-Azure resources from Azure |

---

## Resource Organisation

```
Management Groups  (top level — policy across subscriptions)
  └── Subscriptions  (billing boundary, access control)
        └── Resource Groups  (logical container, same lifecycle)
              └── Resources  (VM, DB, storage account…)
```

| Level | Purpose |
|---|---|
| **Management Group** | Apply policy across multiple subscriptions |
| **Subscription** | Billing unit, quota limits, access scope |
| **Resource Group** | Group resources with same lifecycle — delete RG = delete all |
| **Resource** | Individual service (VM, VNet, SQL Database) |

{: .note }
Resources inherit tags and policies from their parent scope.

---

## Regions & Availability Zones

```
Region (e.g. Australia East)
  ├── Zone 1  (separate data centre, power, cooling)
  ├── Zone 2
  └── Zone 3
```

| Concept | Meaning |
|---|---|
| **Region** | Geographic area with one or more data centres |
| **Region Pair** | Two regions paired for disaster recovery (e.g. East AU / SE AU) |
| **Availability Zone** | Physically separate data centre within a region |
| **Sovereign Cloud** | Isolated cloud — Azure Government, Azure China |

{: .tip }
**Exam:** Zones protect against data centre failure. Region pairs protect against regional failure.

---

## Azure Management Tools

| Tool | When to use |
|---|---|
| **Azure Portal** | Web GUI — day-to-day management |
| **Azure CLI** | Cross-platform scripting (`az` commands) |
| **Azure PowerShell** | Windows scripting (`Az` module) |
| **Cloud Shell** | Browser-based terminal (CLI or PowerShell) |
| **ARM Templates** | Infrastructure as code (JSON) |
| **Bicep** | Cleaner ARM template language |
| **Terraform** | Third-party IaC (multi-cloud) |

---

## Exam Checklist

- [ ] Name 3 compute services and when to use each
- [ ] Explain blob tiers (hot/cool/archive) and the cost tradeoff
- [ ] Distinguish Load Balancer from Application Gateway
- [ ] Explain VPN Gateway vs ExpressRoute
- [ ] Know the resource hierarchy (Management Group → Resource)
- [ ] Explain Availability Zones vs Region Pairs
