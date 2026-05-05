---
title: Quick Reference Cheat Sheet
nav_order: 5
---

# Azure Quick Reference Cheat Sheet

**Keep this open during study & exams.**

---

## Service Selection Matrix

| Need | Service | Type |
|------|---------|------|
| **Run custom app** | VM | IaaS |
| **Web app** | App Service | PaaS |
| **Serverless** | Functions | Serverless |
| **Containers** | ACI / AKS | Container |
| **SQL database** | SQL Database | PaaS |
| **NoSQL** | Cosmos DB | NoSQL |
| **Data warehouse** | Synapse | Analytics |
| **Large files** | Blob Storage | Storage |
| **File shares** | File Shares | Storage |
| **Cache** | Redis Cache | Cache |
| **Load balancing** | Load Balancer | Networking |
| **Advanced routing** | App Gateway | Networking |

---

## Key Numbers to Remember

| Item | Value |
|------|-------|
| **Free tier duration** | 12 months |
| **Free tier credit** | $200 (first month) |
| **SLA: 99.9%** | ~8 hours/year downtime |
| **SLA: 99.95%** | ~22 minutes/month downtime |
| **SLA: 99.99%** | ~52 minutes/year downtime |
| **Blob hot tier cost** | Most expensive |
| **Blob archive cost** | Cheapest |
| **VM deallocated** | No compute cost |
| **Reserved instance (1-year)** | 30% discount |
| **Reserved instance (3-year)** | 72% discount |
| **Spot VM** | Up to 90% discount |
| **Data egress** | $$$$ (expensive) |
| **Data ingress** | FREE |

---

## Permissions (RBAC)

### Quick Assignment
```
Resource/RG → Access Control (IAM) → Add Role Assignment
→ Select role → Select user → Save
```

### Role Hierarchy
**Owner** (full) > **Contributor** (create/modify) > **Reader** (view only)

### Custom Role When Built-in Won't Work

---

## NSG Rules (Firewall)

**Typical Setup:**
```
Inbound:
- Port 80/443 from internet (web servers)
- Port 3389 from admin IP only (RDP)
- Port 22 from admin IP only (SSH)

Outbound:
- Allow all (default)
```

**Check Order:** Priority 100-4096 (lower = first)

---

## VM Sizing Quick Guide

| Size | CPUs | Memory | Use |
|------|------|--------|-----|
| **B2s** | 2 | 4 GB | Dev/test |
| **D2s** | 2 | 8 GB | General purpose |
| **D4s** | 4 | 16 GB | Production web |
| **E4s** | 4 | 32 GB | Databases |

---

## Storage Tiers (Blob)

1. **Hot** → Frequent access (expensive/month, free retrieval)
2. **Cool** → Monthly access (~30 day retrieval)
3. **Archive** → Yearly access (cheapest, ~15 hour retrieval)

---

## Database Selection

| When | Service |
|------|---------|
| **Structured data, ACID** | SQL Database |
| **Open source (PostgreSQL)** | Azure Database for PostgreSQL |
| **Global, NoSQL** | Cosmos DB |
| **In-memory caching** | Redis Cache |
| **Data warehouse** | Synapse Analytics |

---

## Networking Terms

| Term | Means |
|------|-------|
| **VNet** | Virtual network (isolated) |
| **Subnet** | Divide VNet into segments |
| **NSG** | Firewall rules |
| **Public IP** | Internet-facing address |
| **Private IP** | Internal address (10.x, 172.x, 192.x) |
| **Peering** | Connect VNets directly |
| **VPN** | Connect on-prem to cloud |
| **ExpressRoute** | Dedicated private link |

---

## Authentication Types

**Strong → Weak:**
1. **Passwordless** (FIDO2, Windows Hello)
2. **Password + MFA** (authenticator app)
3. **Password + SMS MFA**
4. **Password + Email MFA**
5. **Password only** (NOT recommended)

---

## Backup Strategy

```
Daily backup → 7-day retention
Weekly backup → 30-day retention
Monthly backup → 365-day retention (+ archive)
```

---

## Disaster Recovery Goals

| RTO | RPO | Cost |
|-----|-----|------|
| **Hours** | **Days** | $ (cheap) |
| **Minutes** | **Hours** | $$ (moderate) |
| **Seconds** | **Minutes** | $$$ (expensive) |

---

## Compliance Checklist

- [ ] Data residency (where is data stored?)
- [ ] Encryption (at rest + in transit)
- [ ] Audit logs (who accessed what?)
- [ ] Backup/retention (how long kept?)
- [ ] Access control (least privilege)
- [ ] Monitoring (alerts on suspicious activity)

---

## Cost Optimization Quick Wins

1. **Stop non-prod** at night
2. **Delete unused** resources
3. **Use reserved instances** (1-3 year commitment)
4. **Right-size VMs** (don't over-provision)
5. **Clean up snapshots** (add up fast)
6. **Archive old blobs** (move to Archive tier)
7. **Use CDN** (reduces egress)
8. **Monitor spending** (Cost Management tool)

---

## Monitoring Essentials

**Metrics** (real-time):
- CPU %
- Memory %
- Disk I/O
- Network I/O

**Logs** (detailed):
- Application logs
- System events
- Audit trail

**Alert When:**
- CPU > 80%
- Memory > 85%
- Disk space < 10%
- Failed logins (X times)

---

## Exam Day Tips

- **Read carefully** — Don't rush
- **Manage time** — ~1.5 mins per question
- **Flag uncertain** — Come back if time
- **Use references** — Portal allowed
- **No phone** — Not allowed
- **Take deep breath** — You've got this

---

**Print this page for your study desk!**
