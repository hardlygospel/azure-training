# 3. Pricing & Support 💰

## Pricing Models

### Pay-As-You-Go
- **Cost:** Highest per unit
- **Commitment:** None
- **Best for:** Testing, variable workloads

### Reserved Instances
- **Cost:** 30-72% discount
- **Commitment:** 1-3 years upfront
- **Best for:** Stable, long-term workloads

### Spot VMs
- **Cost:** Up to 90% discount
- **Catch:** Can be evicted anytime
- **Best for:** Fault-tolerant, batch jobs

---

## Cost Factors

### Compute Costs
- **Hourly rate** varies by VM size and region
- **License model:** Windows costs more than Linux
- **Reserved instances:** 30% cheaper (1-year) or 72% (3-year)

### Storage Costs
- **Capacity:** Per GB stored
- **Tiers:** Hot (most expensive) > Cool > Archive
- **Operations:** Read, write, delete transactions
- **Data transfer:** Egress costs (ingress is free)

### Data Transfer Costs
- **Ingress (in):** FREE
- **Egress (out):** $$$ (most expensive)
- **Inter-region transfer:** More expensive than same-region
- **Tip:** Use CDN or ExpressRoute to reduce egress

---

## Cost Management Tools

### Azure Pricing Calculator
- Estimate costs before deployment
- Adjust VM size, region, reserved instances
- **Link:** [Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

### Azure Cost Management
- See actual spending by service/resource/tag
- Set budgets and alerts
- Recommendations to reduce costs

### Azure Advisor
- Personalized recommendations
- Categories: Cost, Security, Reliability, Performance, Operational Excellence

---

## Azure Support Plans

| Plan | Price | Response Times | Best For |
|------|-------|-----------------|----------|
| **Free** | $0 | Community support only | Learning, non-production |
| **Developer** | $29/month | <24 hours | Development/testing |
| **Standard** | $100/month | <1 hour critical | Production workloads |
| **Professional Direct** | $1,000/month | <15 mins critical | Mission-critical systems |

### What's Included?
- **Free:** Docs, forums, community
- **Paid:** Direct Microsoft support, faster responses, architectural guidance

---

## Service Level Agreements (SLAs)

**SLA** = Microsoft's guarantee of uptime

### Common SLA Tiers
- **99.9%** = ~8 hours downtime/year (single instance)
- **99.95%** = ~22 minutes downtime/month (requires 2+ instances)
- **99.99%** = ~52 minutes downtime/year (requires multiple zones/regions)

### Increasing SLA
1. Use multiple instances
2. Deploy across availability zones
3. Use managed services (they handle HA)
4. Implement fault tolerance

---

## Free Resources

### Azure Free Account
- **$200 credit** for first month
- **Free services for 12 months:** VM, SQL Database, storage, etc.
- **Always free:** 
  - 1 million transactions/month (Functions)
  - 12 months compute
  - Cognitive Services (limited)

### Free Tier Limits
- 1GB blob storage free
- After 12 months = pay or downgrade

---

## Key Pricing Concepts

### Regions Matter
- **US East 1:** Cheapest
- **Europe/Asia:** More expensive (infrastructure costs)
- **Premium regions (Australia):** Most expensive

### Reserved Capacity
- Commit to usage = massive savings (30-72%)
- Unused commitment = waste
- Best for predictable workloads

### TCO Calculator
- Compare on-premises vs Azure costs
- Factor in hardware, licensing, support
- [TCO Calculator](https://azure.microsoft.com/en-us/pricing/tco/calculator/)

---

## Cost Optimization Tips ✅

1. **Right-size VMs** — Don't over-provision
2. **Use auto-scaling** — Pay only for what you use
3. **Reserved instances** — 1-3 year commitment = big savings
4. **Spot instances** — For non-critical workloads
5. **Stop resources** — Turn off non-prod at night
6. **Delete unused resources** — RGs, VMs, storage
7. **Monitor spending** — Use Cost Management tool
8. **Clean up data transfer** — egress is expensive

---

## Exam Tips

- **Free tier:** Limited to 12 months and specific quotas
- **SLA:** Single instance = no SLA; 2+ instances = 99.95%
- **Support plans:** Production = at least Standard
- **Reserved instances:** Not refundable (commitment)
- **Data transfer:** Most expensive part of cloud bill
- **CDN:** Reduces egress costs + speeds up content
