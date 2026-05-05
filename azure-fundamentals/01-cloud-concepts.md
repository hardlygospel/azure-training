---
title: 1. Cloud Concepts
parent: Azure Fundamentals (AZ-900)
nav_order: 1
---

# Cloud Concepts & Models

[![AZ-900](https://img.shields.io/badge/AZ--900-Domain%201-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-25--30%25-f59e0b?style=flat-square)]()

---

## What is Cloud Computing?

On-demand access to compute, storage, and networking resources over the internet — **pay only for what you use**.

### Five Key Characteristics

| Characteristic | Meaning |
|---|---|
| **On-demand self-service** | Provision instantly, no human interaction |
| **Broad network access** | Available from anywhere |
| **Resource pooling** | Shared infrastructure (multi-tenant) |
| **Rapid elasticity** | Scale up/down automatically |
| **Measured service** | Metered billing — pay per use |

---

## Cloud Deployment Models

```
PUBLIC                 PRIVATE               HYBRID
──────────────         ──────────────         ──────────────────────
  Azure (cloud)          Your datacenter        Both, connected
  Anyone can use         Internal only          Flexible split
  Least control          Full control           Mixed control
  Cheapest               Most expensive         Middle cost
```

### When to Use Each

| Model | Use When |
|---|---|
| **Public** | Normal workloads, variable scale, no special compliance |
| **Private** | Regulatory, sensitive data, full control required |
| **Hybrid** | Some data must stay on-premises, burst to cloud for scale |

{: .tip }
**Exam:** Hybrid cloud is for organisations that can't fully move to public cloud (compliance, legacy systems).

---

## Cloud Service Models

```
YOU MANAGE ←────────────────────────────────→ PROVIDER MANAGES

  SaaS          PaaS              IaaS
  (Use it)      (Build on it)     (Rent the hardware)
  ──────────    ─────────────     ──────────────────
  Office 365    App Service       Azure VMs
  Dynamics      SQL Database      Azure Storage
  Teams         Functions         Virtual Networks
```

### Shared Responsibility

| Layer | IaaS | PaaS | SaaS |
|---|---|---|---|
| Application | **You** | **You** | Provider |
| Data | **You** | **You** | Provider |
| Runtime | **You** | Provider | Provider |
| OS | **You** | Provider | Provider |
| Virtualisation | Provider | Provider | Provider |
| Hardware / Physical | Provider | Provider | Provider |

{: .tip }
**Exam:** With IaaS you're responsible for OS patches. With PaaS and SaaS you're not.

---

## CapEx vs OpEx

| | CapEx (Capital Expenditure) | OpEx (Operating Expenditure) |
|---|---|---|
| **What** | Buy hardware upfront | Pay monthly/hourly |
| **Example** | On-premises server | Azure subscription |
| **Cloud model** | Private cloud (you own hardware) | Public cloud |
| **Tax treatment** | Depreciated over time | Deducted immediately |

{: .tip }
**Exam:** Cloud = OpEx. On-premises = CapEx.

---

## Key Benefits of Cloud

| Benefit | Meaning |
|---|---|
| **High Availability** | Stays up despite failures (SLA guarantees) |
| **Scalability** | Add resources as demand grows |
| **Elasticity** | Auto-scale up AND down with demand |
| **Agility** | Deploy in minutes, not months |
| **Geo-distribution** | Data centres worldwide |
| **Disaster recovery** | Backup and failover built in |

**Scalability vs Elasticity:**
- **Scalability** = can grow (add more VMs over time)
- **Elasticity** = automatically grows *and shrinks* in real time

---

## Fault Tolerance & Disaster Recovery

| Term | Meaning |
|---|---|
| **Fault tolerance** | System keeps running when a component fails |
| **High Availability** | Minimal downtime — measured by SLA (e.g. 99.95%) |
| **Disaster Recovery** | Recover from major outage |
| **RTO** | Recovery Time Objective — max acceptable downtime |
| **RPO** | Recovery Point Objective — max acceptable data loss |

---

## Exam Checklist

- [ ] Name the 3 cloud models and a use case for each
- [ ] Explain IaaS / PaaS / SaaS and who manages what
- [ ] Explain CapEx vs OpEx
- [ ] Distinguish scalability from elasticity
- [ ] Define HA, fault tolerance, RTO, RPO
