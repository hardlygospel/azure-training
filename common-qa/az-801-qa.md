# Azure 801 (AZ-801) Q&A 🎯

## Identity & Access Management

**Q: When should I use a service principal vs managed identity?**
A:
- **Managed Identity:** Azure resource needs access (preferred, no password)
- **Service Principal:** App outside Azure, or fine-grained control needed
- **Best practice:** Always try managed identity first

**Q: How do I give a user permission to only restart VMs?**
A: Create **custom role** with only "restart" permission, assign to that user.

**Q: What's the difference between system-assigned and user-assigned managed identity?**
A:
- **System-assigned:** Created/deleted with resource (1:1)
- **User-assigned:** Created separately, reusable (1:many)
- **When to use:** System = simple, User = shared across resources

**Q: Can I have MFA without password?**
A: **Yes**, with passwordless sign-in (Windows Hello, FIDO2, authenticator app approval).

**Q: How do I let on-premises users access Azure resources?**
A: Use **Azure AD Connect** to sync identities, then assign roles.

**Q: What if a user has two roles with different permissions?**
A: **Union of permissions** (most permissive wins). If one allows and one denies, **Deny wins**.

---

## Virtual Networking

**Q: How do I prevent internet access from my VMs?**
A: 
1. Remove public IP
2. Block outbound 443/80 in NSG
3. Don't assign them to public subnet
4. Or: Use **Azure Firewall** to control outbound

**Q: Can I have two VNets with the same IP range?**
A: **Yes**, if they don't peer/connect. Once peered, must be different.

**Q: What's the smallest subnet I can create?**
A: **/30** (4 IPs), but Azure reserves 5. So /30 = only 1 usable IP (not recommended).

**Q: How do I route traffic through a firewall?**
A: Create **route table**:
- Destination: Traffic to reach
- Next hop: Firewall VM IP
- Apply to subnet

**Q: Can I use 0.0.0.0/0 as source in NSG?**
A: **Yes** (allow from internet). Good for web servers, bad for databases.

**Q: What's better: NSG or Azure Firewall?**
A:
- **NSG:** Simple, free, VM-level
- **Firewall:** Complex rules, advanced features, centralized
- **Enterprise:** Use both (NSG + Firewall)

**Q: How do I test if a VM can reach another VM?**
A: Use **Network Watcher → IP Flow Verify** or ping (if ICMP allowed).

---

## Compute Management

**Q: How do I ensure my VM doesn't go down?**
A: Deploy 2+ VMs across **availability zones**, behind load balancer.

**Q: What's the difference between availability set and availability zones?**
A:
- **Availability Set:** Spread across hardware (same zone)
- **Availability Zones:** Spread across data centers (separate zones)
- **Prefer:** Zones (better SLA: 99.99% vs 99.95%)

**Q: Can I resize a VM while it's running?**
A: **Sometimes**:
- **Same size family:** Yes (if not pinned to hardware)
- **Different family:** No (must stop, resize, start)

**Q: What's the easiest way to deploy identical VMs?**
A: Use **scale set** or **custom image** + ARM template.

**Q: How do I connect to a Linux VM without SSH key?**
A: Use **Azure Bastion** (browser-based RDP/SSH).

**Q: Can I install software on a VM after creation?**
A: **Yes**, via:
- **Custom Script Extension** (PowerShell/bash)
- **Azure Automation** (Desired State Config)
- **Manual RDP/SSH**

**Q: What's the max number of VMs in a scale set?**
A: **1000** (can be increased with request).

**Q: How do I monitor VM performance?**
A: **Azure Monitor** → Metrics (CPU, Memory, Disk I/O).

---

## Storage & Backup

**Q: When should I use GRS vs RA-GRS?**
A:
- **GRS:** Secondary region (read-only) = $$ 
- **RA-GRS:** Secondary region (read-write) = $$$
- **Use:** RA-GRS if you need to fail over and read from secondary

**Q: Can I move a blob from Hot to Archive instantly?**
A: **Yes**, but retrieval takes hours (Archive SLA: ~15 hours).

**Q: How do I recover a deleted blob?**
A: If **soft delete enabled**: Restore from recycle bin (7-365 days). Otherwise: Restore from snapshot.

**Q: What's the difference between a snapshot and a backup?**
A:
- **Snapshot:** Point-in-time copy (incremental, cheap)
- **Backup:** Full backup + incremental (managed, with retention policy)
- **Use:** Snapshot for quick recovery, backup for compliance

**Q: Can I have multiple data disks on a VM?**
A: **Yes** (up to 64 disks). But:
- Size limits: Standard 4 TB, Premium 32 TB
- Performance limits: IOPS and throughput

**Q: What happens to data if I delete a storage account?**
A: **Data is deleted** (usually immediately, sometimes 30-day grace period).

**Q: How do I encrypt data in storage?**
A: **By default:** Microsoft-managed encryption (free). **Optional:** Customer-managed keys (more control).

**Q: Can I change storage replication after creation?**
A: **Yes** (portal → Storage account → Configuration → Replication). Costs may change.

---

## Monitoring & Compliance

**Q: How long are Azure logs kept by default?**
A: **Depends:**
- **Metrics:** 93 days
- **Logs:** 30 days (default), up to 730 days (configurable)
- **Backup:** 7 years typical

**Q: What's a good alert threshold for CPU?**
A: **Depends on workload**, but typical:
- Warning: 70%
- Critical: 85%
- For VMs: Scale up when hitting 80%

**Q: How do I see what a user did on a resource?**
A: **Activity Log** (Resource → Activity Log). Shows create/delete/modify operations.

**Q: How do I prevent someone from deleting important resources?**
A: **Management Lock**:
- **Read-only:** Can view but not modify
- **Delete:** Can modify but not delete
- Applied at resource, RG, or subscription level

**Q: Can I audit who accessed my database?**
A: **Yes**:
- **SQL Database:** Audit feature (logging)
- **Storage:** Storage Analytics (optional)
- **All resources:** Activity Log

**Q: How often should I review my compliance score?**
A: **Weekly** (or after major changes). Use **Compliance Manager**.

**Q: What policy would I use to enforce tagging?**
A:
```
Policy: "Require tag: CostCenter"
Effect: Deny
Action: Block resource creation without tag
```

**Q: Can I backup a VM to a different region?**
A: **Yes**:
- **Backup Vault:** Cross-region restore available
- **Site Recovery:** Replicate to different region

---

## Troubleshooting Scenarios

**Q: My VM can't reach the internet. What do I check?**
A: Check in order:
1. **Public IP** (does VM have one?)
2. **Route Table** (is there a default route to internet?)
3. **NSG** (are outbound 443/80 allowed?)
4. **Network Watcher** → IP Flow Verify
5. **Firewall rules** (if Azure Firewall deployed)

**Q: Can't RDP into my VM.**
A: Check:
1. **VM status** (is it running?)
2. **Public IP** (do I have one? use Bastion if not)
3. **NSG** (is port 3389 allowed from your IP?)
4. **Firewall** (personal firewall blocking port?)
5. **RDP service** (running on VM?)

**Q: Storage account requests are throttled.**
A: Solutions:
1. **Increase throughput** (higher-tier disk)
2. **Distribute load** (multiple storage accounts)
3. **Implement caching** (CDN, Redis)

**Q: App can't write to database.**
A: Check:
1. **Connection string** (correct?)
2. **NSG** (port 1433 allowed from app subnet to DB subnet?)
3. **Firewall rule** (database firewall allows app?)
4. **Quota** (storage space available?)
5. **Permissions** (user account has write access?)

**Q: Backup failed.**
A: Check:
1. **Backup vault:** Permissions set?
2. **VM:** Running, accessible?
3. **Network:** Can VM reach backup service?
4. **Quota:** Storage space available?
5. **Logs:** Azure Monitor for error details

---

## Exam Strategy

**Q: How many questions should I expect on each topic?**
A: Rough breakdown:
- **Networking:** 15-20%
- **Compute:** 20-25%
- **Storage:** 10-15%
- **Identity:** 15-20%
- **Monitoring:** 10-15%
- **Misc:** 10%

**Q: Should I memorize IP ranges, ports, etc.?**
A: **No** (exam allows reference materials). Focus on:
- **Concepts:** Why use X instead of Y
- **Best practices:** When to use each service
- **Troubleshooting:** How to diagnose issues

**Q: Are there labs in the exam?**
A: **Yes**, some questions are hands-on labs (create resources, configure settings). Practice in Azure portal!

---

## Study Tips ✅

1. **Hands-on practice** — Create VMs, deploy resources in Azure
2. **Use free tier** — $200 credit + 12 months free services
3. **Review failures** — Understand why you got it wrong
4. **Know the tools** — Portal, CLI, PowerShell
5. **Time management** — ~1.5-2 minutes per question
6. **Take practice exams** — Microsoft Learn has official ones
