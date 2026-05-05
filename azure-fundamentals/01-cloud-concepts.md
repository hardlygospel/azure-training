# 1. Cloud Concepts & Models

## What is Cloud Computing?

**Cloud computing** = On-demand access to computing resources (compute, storage, networking) via the internet.

### Key Characteristics
- **On-demand self-service** — Resources available instantly
- **Pay-as-you-go** — Only pay for what you use
- **Scalability** — Easily increase or decrease resources
- **Elasticity** — Automatically scale based on demand
- **Measured service** — Usage tracked and billed

---

## Cloud Deployment Models

### Public Cloud ☁️
- **Owner:** Cloud provider (Microsoft, AWS, Google)
- **Access:** Anyone with internet connection
- **Cost:** Lower (shared infrastructure)
- **Control:** Least
- **Example:** Azure public regions

### Private Cloud 🔒
- **Owner:** Organization
- **Access:** Internal users only
- **Cost:** Higher (dedicated)
- **Control:** Full
- **Example:** On-premises datacenter

### Hybrid Cloud 🌉
- **Mix:** Public + Private
- **Cost:** Medium
- **Flexibility:** High
- **Example:** On-prem data + Azure compute

---

## Cloud Service Models

### IaaS (Infrastructure as a Service) 🔧
*"Rent the hardware"*

- You manage: Applications, data, runtime, middleware, OS
- Provider manages: Virtualization, servers, networking, storage

**Examples:** Azure VMs, Azure App Service (compute)

**Best for:** Developers needing full control

### PaaS (Platform as a Service) 🏗️
*"Rent the platform"*

- You manage: Applications, data
- Provider manages: Everything else (OS, middleware, runtime)

**Examples:** Azure App Service, Azure SQL Database, Azure Functions

**Best for:** Rapid development without infrastructure headache

### SaaS (Software as a Service) 📧
*"Just use it"*

- Provider manages: Everything
- You: Just use the application

**Examples:** Microsoft 365, Dynamics 365, Office Online

**Best for:** End users (no technical knowledge needed)

---

## Responsibilities Matrix

| Layer | IaaS | PaaS | SaaS |
|-------|------|------|------|
| **Applications** | You | You | Provider |
| **Data** | You | You | Provider |
| **Runtime** | You | Provider | Provider |
| **Middleware** | You | Provider | Provider |
| **OS** | You | Provider | Provider |
| **Virtualization** | Provider | Provider | Provider |
| **Hardware** | Provider | Provider | Provider |

---

## Benefits of Cloud ✅

1. **Cost-effective** — No upfront hardware costs
2. **Scalable** — Grow from 1 to 1000 users easily
3. **Reliable** — Built-in redundancy and SLAs
4. **Secure** — Enterprise-grade security
5. **Global reach** — Data centers worldwide
6. **Latest technology** — Always on current versions

---

## Cloud Architecture Patterns

### Fault Tolerance
- System continues despite component failures
- **Example:** Multiple instances in different zones

### Disaster Recovery
- Recover from major outages
- **RTO** (Recovery Time Objective) = How quickly to recover
- **RPO** (Recovery Point Objective) = How much data loss acceptable

### High Availability (HA)
- System always accessible
- **SLA:** Service Level Agreement (e.g., 99.95% uptime = 22 mins downtime/month)

---

## Key Exam Tips

- **CapEx vs OpEx:** Cloud = OpEx (operating expense), not CapEx (capital expense)
- **Scalability vs Elasticity:** Scalability = growth over time; Elasticity = instant response
- **Public vs Private vs Hybrid:** Know use cases for each
- **IaaS/PaaS/SaaS:** Understand what each provides and who manages what
