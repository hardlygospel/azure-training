# 3. Compute Management 🖥️

## Virtual Machines (VMs)

### VM Basics
- **Own OS, applications, data**
- **Full control** of configuration
- **Pay by hour** (or reserved instances)
- **Requires:** VNet, storage, NIC

### VM Lifecycle
```
Stopped (deallocated) → Started → Running → Stopped → Deleted
Cost: Free when deallocated | Cost: Pay per hour when running
```

### Creating a VM
1. **Resource Group**
2. **Name + Region**
3. **Image** (Windows 2022, Ubuntu 20.04, custom)
4. **Size** (B2s, D2s, E16s, etc.)
5. **Admin account** (username/password or SSH key)
6. **Disks** (OS disk + data disks)
7. **VNet + Subnet**
8. **Public IP** (optional)
9. **NSG** (firewall rules)

### VM Sizes
| Category | Use | Example |
|----------|-----|---------|
| **B (Burstable)** | Dev, test, light | B2s, B3s |
| **D (General Purpose)** | Most workloads | D2s, D4s, D16s |
| **E (Memory Optimized)** | Databases, SAP | E2s, E8s |
| **F (Compute Optimized)** | Batch, HPC | F2s, F4s |
| **M (Mega)** | Very large workloads | M64s, M416s |

### VM Disks
- **OS disk:** Windows/Linux system
- **Data disks:** Additional storage
- **Temp disk:** Temporary (lost on reboot)
- **Managed disks:** Azure manages storage account

### Disk Types
| Type | Speed | Cost | Use |
|------|-------|------|-----|
| **Premium SSD** | 7,500 IOPS | $$ | Production DBs |
| **Standard SSD** | 500 IOPS | $ | General purpose |
| **Standard HDD** | 60 IOPS | $ | Backup, archive |

---

## Scale Sets & Availability

### Virtual Machine Scale Sets (VMSS)
- **Automatically scale** VMs based on demand
- **Load balancer** included
- **Create/delete** VMs automatically
- **Use case:** Web apps, APIs with variable load

### Availability Set
- **Ensures VMs spread** across hardware
- **Fault domains:** Physical rack separation
- **Update domains:** Patch separately
- **SLA:** 99.95% with 2+ VMs

### Availability Zones
- **Physically separate** data centers (same region)
- **SLA:** 99.99% with 3+ VMs across zones
- **Preferred:** Over availability sets

### VM Deployment Strategy
```
Production:
- Minimum 2 VMs
- Across availability zones
- Behind load balancer
= 99.95% - 99.99% uptime SLA
```

---

## VM Extensions

### What Is an Extension?
- **Post-deployment** configuration
- **Install software** automatically
- **Run scripts** on startup
- **Examples:** Anti-malware, monitoring, domain join

### Common Extensions
| Extension | Purpose |
|-----------|---------|
| **Custom Script** | Run PowerShell/bash script |
| **Desired State Config** | Infrastructure as code |
| **Domain Join** | Join Windows domain |
| **Anti-malware** | Windows Defender settings |
| **Dependency Agent** | VM monitoring |

---

## VM Administration

### Remote Access

**Windows RDP (Remote Desktop Protocol)**
- **Port:** 3389
- **Tool:** Remote Desktop Connection, mstsc.exe
- **Security:** Don't expose to internet (use Bastion)

**Linux SSH (Secure Shell)**
- **Port:** 22
- **Key-based auth:** SSH keys (preferred)
- **Password auth:** Less secure

### Azure Bastion
- **Secure RDP/SSH** without public IP
- **Browser-based** access
- **Cost:** ~$10/hour
- **Best for:** Jump host, security

### Run Command
- **Execute commands** on VM without RDP/SSH
- **Built-in** (no agent needed)
- **Use case:** Quick fixes, scripts
- **Output:** Command output returned

### VM Agent
- **System service** on VM
- **Manages extensions**
- **Runs scripts**
- **Enabled by default** (most images)

---

## Updates & Patching

### Automatic Patching
- **Windows:** Enable automatic updates (recommended)
- **Linux:** Use package manager or automation

### Azure Update Management
- **Centralized patch** management
- **Schedule patches** (Tuesday 2am, etc.)
- **Track compliance** (patched vs unpatched)
- **Pre/post scripts** for custom steps

### Maintenance Configuration
- **Schedule maintenance** windows
- **Group VMs** for bulk updates
- **Prevent simultaneous** updates

---

## VM Monitoring

### Diagnostics
- **Boot diagnostics:** Startup troubleshooting
- **Guest OS diagnostics:** OS-level monitoring
- **CPU, memory, disk** metrics

### Metrics & Alerts
- **Metric:** CPU %, Memory %, Disk I/O
- **Alert:** Notify when threshold exceeded
- **Action:** Email, SMS, webhook, automation

---

## Azure Container Instances (ACI)

### Containers vs VMs
| | Container | VM |
|--|-----------|-----|
| **Size** | MB | GB |
| **Startup** | Seconds | Minutes |
| **OS** | Shared | Full OS |
| **Cost** | Cheaper | More |
| **Use** | Apps | Any workload |

### ACI Features
- **Quick container deployment**
- **No container orchestration** (simple)
- **Serverless** (no infrastructure)
- **Pay per second**

### When to Use ACI
- **Simple containers** (not many)
- **Short-running** tasks
- **One-off jobs**
- **Best for:** Batch jobs, scripts, microservices

---

## Azure Kubernetes Service (AKS)

### Kubernetes Basics
- **Container orchestration** platform
- **Manages scaling, deployment,** networking
- **Nodes:** VMs running containers
- **Pods:** Smallest unit (one or more containers)
- **Services:** Expose pods to network

### AKS Features
- **Managed Kubernetes** (Microsoft manages control plane)
- **Auto-scaling** (node pools)
- **Integrated monitoring**
- **RBAC** for cluster access

### When to Use AKS
- **Complex, multi-container** apps
- **Need auto-scaling**
- **Microservices architecture**
- **Learning curve:** Steep

---

## Instance Metadata Service (IMDS)

### What Is It?
- **Local HTTP endpoint** on every VM
- **Provides VM info:** IP, location, SSH keys
- **Access:** 169.254.169.254 (internal only)
- **No authentication** needed

### Use Cases
- **Get VM name/region** at runtime
- **Fetch managed identity token** (IMDS endpoint)
- **Application configuration** stored in IMDS

---

## Exam Tips

- **VMSS:** Auto-scale, load balance, multiple VMs
- **Availability Set:** Spread across hardware
- **Availability Zones:** Spread across data centers (prefer this)
- **RDP:** Windows remote access (port 3389)
- **SSH:** Linux remote access (port 22)
- **Bastion:** Secure RDP/SSH without public IP
- **Extensions:** Post-deployment configuration
- **ACI:** Simple containers, quick start
- **AKS:** Complex Kubernetes workloads
- **IMDS:** Get VM info from within VM
