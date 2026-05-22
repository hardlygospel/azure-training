
# Azure Fundamentals (AZ-900) Q&A

## Cloud Models & Concepts

**Q: What's the difference between scalability and elasticity?**
A: 
- **Scalability:** Ability to grow over time (add more VMs)
- **Elasticity:** Automatically respond to demand (add/remove VMs instantly)
- **Example:** Your app grows from 1M to 10M users = scalability. It handles traffic spikes at noon = elasticity.

**Q: Which cloud model gives you the MOST control?**
A: **Private Cloud** (you own everything). Public cloud gives LEAST control.

**Q: When would you use a hybrid cloud?**
A: When you need:
- Some data on-premises (compliance)
- Some in public cloud (scalability)
- Example: Store patient data locally (HIPAA), use Azure for analytics

**Q: Is cloud computing expensive?**
A: Depends:
- **Upfront:** No hardware costs (good)
- **Monthly:** Can be high if over-provisioned (bad)
- **Solution:** Right-size resources, use reserved instances

---

## Service Models (IaaS/PaaS/SaaS)

**Q: I need an OS I can control. Which service model?**
A: **IaaS** (you manage OS, apps, data). Example: Azure VM.

**Q: I don't want to manage the OS.**
A: **PaaS** (provider manages OS). Example: App Service.

**Q: I just want to use the app.**
A: **SaaS** (provider manages everything). Example: Office 365.

**Q: Who manages security patches for VMs?**
A: **You** (partly). VM OS = you. Hypervisor = Microsoft.

**Q: Can I run containers on App Service?**
A: **Yes**, but it's still PaaS. App Service can host Docker containers.

---

## Azure Services

**Q: When would you use Blob Storage vs File Shares?**
A: 
- **Blob:** Large files, images, videos, archives
- **File Shares:** Network shares (like SMB), shared folders
- **Example:** Video library = Blob. Shared folder for documents = File Share.

**Q: What's the difference between Azure SQL Database and SQL Server on VM?**
A:
- **SQL Database:** PaaS (Microsoft manages patches, backups, HA)
- **SQL Server on VM:** IaaS (you manage everything)
- **Best practice:** Use SQL Database (less work)

**Q: When would you use Cosmos DB instead of SQL?**
A: When you need:
- **Global distribution** (data in multiple regions)
- **NoSQL** (flexible schema)
- **High throughput** (millions of reads/sec)
- **Example:** Mobile app with users worldwide

**Q: What's Azure Functions used for?**
A: **Event-driven, serverless compute**. Examples:
- Process image when uploaded to blob
- Send email when database changes
- Run scheduled job at midnight
- Handle webhook from external service

**Q: How is Functions cheaper than VMs?**
A: You **only pay for execution time** (not idle time). VM runs 24/7 = always paying.

---

## Pricing & Costs

**Q: Why is data transfer out so expensive?**
A: 
- Infrastructure cost (limited bandwidth)
- Cloud providers charge to recoup costs
- **Solution:** Use CDN, ExpressRoute, or keep data internal

**Q: What's the difference between reserved instances and spot VMs?**
A:
- **Reserved:** Commit 1-3 years, 30-72% discount, won't be evicted
- **Spot:** Up to 90% discount, can be kicked off anytime
- **Best for spot:** Batch jobs, fault-tolerant apps

**Q: Free account limits?**
A: 
- $200 credit for first month
- Free services for 12 months (then pay)
- Some always free (limited): Functions, Cognitive Services

**Q: Does Azure charge for failed transactions?**
A: **Yes**, some services charge per operation (read/write/delete). Failed requests still count.

---

## Security & Compliance

**Q: Who's responsible for security?**
A: **Both** (shared responsibility):
- **Microsoft:** Infrastructure, physical, hypervisor
- **You:** OS, apps, data, user access, encryption

**Q: Does Azure encrypt data by default?**
A: **Yes** (at rest, in storage). But:
- **Not by default:** VM disks (you can enable)
- **Not included:** App-level encryption (you must do)

**Q: What's the difference between a role and a permission?**
A:
- **Role:** Container of permissions (Owner, Contributor, Reader)
- **Permission:** Specific action (read VM, delete storage)

**Q: Can I restrict a user to one resource?**
A: **Yes**, assign role at that resource level (not subscription).

**Q: What happens if I delete a resource group?**
A: **Everything inside is deleted** (VMs, databases, storage). Be careful!

---

## Availability & Disaster Recovery

**Q: What does 99.95% SLA mean?**
A: System is down **maximum 22 minutes/month**.

**Q: How do I get 99.95% SLA?**
A: Deploy 2+ instances across availability zones or availability sets.

**Q: What's the difference between RTO and RPO?**
A:
- **RTO:** How quickly you recover (time objective)
- **RPO:** How much data you can lose (point objective)
- **Example:** RTO=1 hour, RPO=5 minutes (lose at most 5 mins of data)

**Q: Do I need disaster recovery?**
A: Depends on business impact:
- **Critical system:** Yes (massive cost)
- **Development:** No
- **Business-critical:** Probably

---

## Networking

**Q: What's a virtual network (VNet)?**
A: **Isolated network** in Azure (like private network). You define:
- IP address range (10.0.0.0/16)
- Subnets
- Routing, DNS, security

**Q: Can VNets in different regions talk to each other?**
A: **Yes**, via:
- **Peering:** Fast, low latency, same Azure backbone
- **VPN:** Over internet, slower
- **ExpressRoute:** Dedicated private link, fastest

**Q: What's an NSG?**
A: **Network Security Group** = firewall rules. Control:
- Inbound/outbound traffic
- Port, protocol, source, destination

---

## Exams & Certification

**Q: Is AZ-900 required to take AZ-801?**
A: **No** (but recommended). AZ-801 is harder and assumes knowledge.

**Q: How long is the AZ-900 exam?**
A: **45-60 minutes**, 40-60 questions.

**Q: Can I use study materials during the exam?**
A: **No** (proctored), no notes, browsers, or references allowed.

**Q: What's the passing score?**
A: Approximately **700/1000** (~70%). Score varies by question difficulty.

**Q: How long are certifications valid?**
A: **1 year** from passing date. Then must renew.

---

## Common Misconceptions

**Q: Is Microsoft 365 part of Azure?**
A: **No** (different service). But you can integrate them.

**Q: Do I pay Microsoft when my resource is stopped?**
A: **VM:** No (if deallocated). **Database:** Yes (still reserved). **Storage:** Yes (still storing).

**Q: Is private cloud cheaper than public cloud?**
A: **No**, usually more expensive (you buy/maintain hardware).

**Q: Does Azure backup automatically?**
A: **No** (must enable explicitly). Always enable for important data.

**Q: Can I access my VM with a keyboard and mouse?**
A: **Yes**, via RDP (Remote Desktop) or SSH.

---

## Study Tips ✅

1. **Read thoroughly** — Each bullet has exam questions
2. **Understand the Why** — Know *why* you choose a service
3. **Compare services** — Understand tradeoffs (cost vs performance)
4. **Take practice exams** — Microsoft Learn has free ones
5. **Review failures** — Learn from questions you get wrong
6. **Manage time** — ~1-1.5 mins per question
