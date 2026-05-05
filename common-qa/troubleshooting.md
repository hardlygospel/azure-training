# Troubleshooting Guide 🔧

Quick reference for diagnosing Azure issues.

## Connectivity Issues

### VM Can't Reach Internet

**Checklist:**
- [ ] VM has public IP (or NAT gateway)
- [ ] Default route exists (0.0.0.0/0)
- [ ] Outbound NSG rule allows traffic (destination = internet, port 443/80)
- [ ] Route table doesn't override default

**Tools:**
```
Network Watcher → IP Flow Verify → Select source VM, destination internet
```

---

### VM Can't Talk to Another VM

**Checklist:**
- [ ] Both in same VNet (or peered)
- [ ] NSG on both sides (check inbound AND outbound)
- [ ] Private IP is correct
- [ ] Route exists (check route table)

**Diagnose:**
```
VM1 → Network Watcher → IP Flow Verify
Source: VM1 IP, Destination: VM2 IP, Port: 443
Result: Allow/Deny (tells you if NSG is blocking)
```

**If NSG blocks:**
- Add inbound rule on VM2 subnet/NSG
- Source: VM1 IP or subnet
- Port: Whatever you need

---

### RDP Connection Failed

**Checklist:**
- [ ] VM running?
- [ ] Public IP assigned (or use Bastion)?
- [ ] NSG allows port 3389 from your IP?
- [ ] Windows Firewall on VM allows RDP?
- [ ] Boot diagnostics successful (not hung)?

**Troubleshooting Steps:**
1. Check VM status → Should be "Running"
2. If VM stuck: Stop (deallocate) → Start
3. If still won't boot: Check boot diagnostics
4. If network issue: Check NSG (port 3389 inbound)

---

### SSH Connection Failed

**Checklist:**
- [ ] SSH key correct?
- [ ] Port 22 allowed in NSG?
- [ ] Public IP assigned?
- [ ] SSH daemon running on VM?

**Commands:**
```bash
# Test connectivity
ssh -v azure-user@<public-ip>

# If port blocked:
# Add NSG rule: Inbound, port 22, from your IP

# If key issue:
# Check file permissions: chmod 400 key.pem
```

---

## Performance Issues

### VM Running Slow

**Check:**
- [ ] CPU usage high? (Azure Monitor → CPU %)
- [ ] Memory high? (Azure Monitor → Memory %)
- [ ] Disk I/O high? (Azure Monitor → Disk read/write)
- [ ] Network latency? (Network Watcher → Connection Troubleshoot)

**Solutions:**
```
High CPU:     Resize to larger VM (more cores)
High Memory:  Add more RAM (resize)
High Disk I/O: Premium SSD (faster disks)
High Latency: Move to closer region
```

---

### Database Queries Slow

**Check:**
- [ ] Connection count maxed?
- [ ] Missing indexes?
- [ ] Large full table scan?
- [ ] Network latency to database?

**Diagnose:**
```
Azure Portal → SQL Database → Query Performance Insight
Shows: Slowest queries, resource-intensive queries
```

---

## Storage Issues

### Blob Upload Fails

**Checklist:**
- [ ] Storage account exists and accessible?
- [ ] Credentials correct (account key or SAS token)?
- [ ] Quota not exceeded?
- [ ] Network access allowed (firewall)?

**Common Errors:**
```
401 (Unauthorized):   Invalid credentials
403 (Forbidden):      Access denied, check RBAC
404 (Not Found):      Container doesn't exist
Timeout:              Network issue or large file
```

---

### Storage Account Throttled

**Symptoms:** Requests fail with 503 (Service Unavailable)

**Solutions:**
1. **Increase throughput:**
   - Upgrade disk type (Standard → Premium)
   - Distribute across multiple accounts

2. **Optimize:**
   - Cache frequently accessed data
   - Batch operations (don't do 1000 individual writes)
   - Use CDN for static content

---

## Permission Issues

### User Can't Delete Resource

**Check:**
- [ ] Role assigned at resource/RG level?
- [ ] Role includes "delete" permission?
- [ ] No resource lock (Read-only or Delete)?
- [ ] Is subscription owner role?

**Diagnose:**
```
Azure Portal → Access Control (IAM)
→ Check Roles for user
→ Check if permission includes "delete"
```

---

### App Can't Write to Database

**Check:**
- [ ] Database credentials correct?
- [ ] Database user exists?
- [ ] NSG allows traffic (port 1433 for SQL)?
- [ ] Firewall rule allows app IP?
- [ ] User has INSERT/UPDATE permission?

---

## Backup & Recovery

### Backup Failed

**Check:**
- [ ] Backup vault configured?
- [ ] VM accessible (running)?
- [ ] Backup agent installed (if needed)?
- [ ] Storage space available?
- [ ] Network accessible (can reach backup endpoint)?

**Solution:**
```
Azure Portal → Backup vault → Protected items
→ Click VM → See failure reason
→ Common: VM not running, agent failed
```

---

### Can't Restore from Backup

**Issues:**
```
Target VM deleted:     Restore to new VM
Wrong region:          Use cross-region restore
Quota exceeded:        Delete old resources first
Disk conflicts:        Rename disks during restore
```

---

## Monitoring & Logging

### No Data in Log Analytics

**Check:**
- [ ] Diagnostic settings configured?
- [ ] Data flowing to Log Analytics workspace?
- [ ] Workspace in correct region?
- [ ] Sufficient permissions to query?

**Diagnose:**
```
Resource → Diagnostic settings
→ Check "Send to Log Analytics"
→ Query: CommonSecurityLog | take 10
(should return data)
```

---

### Alert Not Firing

**Check:**
- [ ] Metric data present? (no data = no alert)
- [ ] Threshold correct? (metric not exceeding)
- [ ] Action group configured?
- [ ] Alert rule enabled?

---

## Networking Troubleshooting

### Traceroute Path Wrong

**Use Network Watcher:**
```
Network Watcher → Next Hop
Source VM: Check where traffic goes
Destination: Where is it being routed?
Result: Next hop type (VM, gateway, internet, none)
```

**If wrong:**
- Check route table on subnet
- Routes override default
- Most specific route wins

---

## Common Error Codes

| Code | Meaning | Fix |
|------|---------|-----|
| **401** | Unauthorized | Check credentials |
| **403** | Forbidden | Check permissions/RBAC |
| **404** | Not Found | Resource doesn't exist |
| **409** | Conflict | Resource already exists |
| **429** | Throttled | Too many requests, slow down |
| **503** | Unavailable | Service overloaded or maintenance |
| **508** | Loop Detected | Network routing loop |

---

## Quick Diagnostic Commands

### Azure CLI

```bash
# Check VM status
az vm list --resource-group MyRG --query "[].{Name:name, Status:powerState}"

# Check NSG rules
az network nsg rule list --resource-group MyRG --nsg-name MyNSG

# Check route table
az network route-table route list --resource-group MyRG --route-table-name MyRT

# Check RBAC assignments
az role assignment list --resource-group MyRG --query "[].{Role:roleDefinitionName, User:principalName}"

# Check diagnostics
az monitor diagnostic-settings list --resource /subscriptions/.../resourceGroups/MyRG/providers/Microsoft.Compute/virtualMachines/MyVM
```

### Azure Portal

1. **Resource → Activity Log** → See who did what when
2. **Resource → Diagnose and solve problems** → Automated troubleshooting
3. **Monitor → Metrics** → Check CPU, memory, disk
4. **Monitor → Logs** → Query events
5. **Network Watcher** → IP Flow Verify, Next Hop, Connection Test

---

## Escalation Checklist

Still stuck? Before calling support:

- [ ] Checked Azure Status (azure.status.microsoft)
- [ ] Verified credentials/permissions
- [ ] Checked NSG/firewall rules
- [ ] Reviewed activity log for errors
- [ ] Checked resource quotas
- [ ] Tried creating in different region
- [ ] Disabled extensions (if VM won't start)
- [ ] Reproduced in separate resource

---

**Pro Tip:** Enable diagnostic logs BEFORE you have problems. Troubleshooting is easier with historical data!
