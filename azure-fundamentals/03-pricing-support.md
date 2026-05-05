---
title: 3. Pricing & Support
parent: Azure Fundamentals (AZ-900)
nav_order: 3
---

# Pricing & Support

[![AZ-900](https://img.shields.io/badge/AZ--900-Domain%203-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-10--15%25-f59e0b?style=flat-square)]()

---

## Pricing Models

| Model | Discount | Commitment | Best for |
|---|---|---|---|
| **Pay-as-you-go** | None | None | Testing, unpredictable workloads |
| **Reserved Instances** | 30–72% | 1 or 3 years, upfront | Stable, long-running workloads |
| **Spot VMs** | Up to 90% | None (can be evicted) | Fault-tolerant batch jobs |
| **Dev/Test pricing** | 40–55% | Visual Studio subscription | Non-production only |

{: .tip }
**Exam:** Spot VMs can be evicted at any time. Never use for production databases.

---

## What Affects Cost

```
Compute:    VM size × hours running (stop = no charge if deallocated)
Storage:    GB stored + tier (hot/cool/archive) + operations
Networking: Ingress (IN) = FREE | Egress (OUT) = charged
Database:   DTUs or vCores + storage
```

### Key Rules
- **Deallocated VM** = no compute charge (still pays for storage)
- **Data ingress** = always free
- **Data egress** = costs money — minimise cross-region transfers
- **Region matters** — US East is generally cheapest; Australia / Brazil most expensive
- **Windows VMs** cost more than Linux (OS licensing)

---

## Cost Management Tools

| Tool | What it does |
|---|---|
| **Azure Pricing Calculator** | Estimate cost before you deploy |
| **TCO Calculator** | Compare on-prem vs Azure total cost |
| **Cost Management + Billing** | Track real spending, set budgets, get alerts |
| **Azure Advisor** | Recommendations to reduce waste |

{: .tip }
**Exam:** Pricing Calculator = estimate future cost. TCO Calculator = justify moving to cloud. Cost Management = track actual spend.

---

## Service Level Agreements (SLAs)

An SLA is Microsoft's uptime **guarantee**. If they miss it, you get service credits.

| SLA | Max downtime/month | Requirement |
|---|---|---|
| **99.9%** | ~43 minutes | Single instance VM |
| **99.95%** | ~22 minutes | 2+ VMs in Availability Set |
| **99.99%** | ~4 minutes | 2+ VMs across Availability Zones |

### How to Improve Your SLA
1. Use multiple instances (never single VM in production)
2. Deploy across Availability Zones (not just Availability Sets)
3. Use managed PaaS services (they handle HA for you)
4. Use region pairs for geo-redundancy

{: .tip }
**Exam:** A single VM has an SLA. Two VMs in an Availability Set have a *better* SLA. Two VMs across Zones have the *best* SLA.

### Composite SLA
When services depend on each other, multiply their SLAs:

```
App Service (99.95%) × SQL Database (99.99%) = 99.94% composite
```

The weakest link reduces your overall availability.

---

## Azure Support Plans

| Plan | Monthly Cost | Critical Response | Best for |
|---|---|---|---|
| **Basic** | Free | Community only | Learning |
| **Developer** | ~$29 | < 8 hours | Dev/test |
| **Standard** | ~$100 | < 1 hour | Production |
| **Professional Direct** | ~$1,000 | < 15 minutes | Business-critical |
| **Premier/Unified** | Custom | < 15 minutes | Enterprise |

{: .tip }
**Exam:** Production workloads = Standard minimum. Standard includes 24/7 support for critical issues.

---

## Azure Free Account

| Offer | Details |
|---|---|
| **Credit** | $200 USD for first 30 days |
| **Free 12 months** | Select services (VM B1s, 5 GB storage, SQL DB, etc.) |
| **Always free** | 55+ services with monthly limits |

**Always-free examples:**
- Azure Functions: 1 million executions/month
- App Service: 10 apps (F1 tier)
- Cosmos DB: 1,000 RU/s + 25 GB
- Azure DevOps: 5 users

---

## Factors in Total Cost

1. **Resource type** — VMs cost more than storage
2. **Consumption** — More use = more cost
3. **Region** — Prices vary by region
4. **Bandwidth** — Egress is expensive
5. **Reserved vs pay-as-you-go** — Reservations save 30–72%
6. **Licensing** — Azure Hybrid Benefit (use existing Windows/SQL licences)

### Azure Hybrid Benefit
- **Use your existing** on-premises Windows Server or SQL Server licences in Azure
- **Save up to 40%** on VMs and 55% on SQL Database
- Requires Software Assurance

---

## Exam Checklist

- [ ] Name the 3 main pricing models and tradeoffs
- [ ] Explain what affects egress cost (and that ingress is free)
- [ ] Calculate a composite SLA
- [ ] Match support plan to scenario (dev, prod, enterprise)
- [ ] Describe the Azure free account limits
- [ ] Explain Azure Hybrid Benefit
