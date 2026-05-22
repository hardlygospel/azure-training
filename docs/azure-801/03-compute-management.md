
# Compute Management

[![AZ-801](https://img.shields.io/badge/AZ--801-Domain%203-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-20--25%25-f59e0b?style=flat-square)]()

---

## Virtual Machines

### VM States & Billing

```
Stopped (OS shutdown)     → still billed for compute
Deallocated               → NOT billed for compute (still billed for disk)
Running                   → billed
Deleted                   → not billed (disks remain unless deleted)
```

{: .tip }
**Exam:** "Stopped" and "Deallocated" look the same to users but cost differently. Always deallocate, not just stop.

### VM Components
Every VM needs:
- **Compute** — size (vCPUs, RAM)
- **OS disk** — managed disk (Premium SSD recommended)
- **NIC** — attached to a subnet
- **OS image** — Windows Server, Ubuntu, RHEL, custom, etc.

Optional: Data disks, public IP, availability zone, extensions.

### VM Sizes

| Family | vCPU/RAM | Use |
|---|---|---|
| **B** (Burstable) | 1–20 / 0.5–80 GB | Dev, test, light workloads |
| **D** (General Purpose) | 2–96 / 4–384 GB | Web, app servers |
| **E** (Memory Optimised) | 2–104 / 16–672 GB | Databases, in-memory analytics |
| **F** (Compute Optimised) | 2–72 / 4–144 GB | CPU-heavy batch jobs |
| **L** (Storage Optimised) | 8–80 / 64–640 GB | High-throughput databases |
| **N** (GPU) | 4–64 | ML training, graphics rendering |

### Disk Types

| Type | Max IOPS | Cost | Use |
|---|---|---|---|
| **Premium SSD** | 20,000 | $$$ | Production databases |
| **Standard SSD** | 6,000 | $$ | General purpose |
| **Standard HDD** | 500 | $ | Backup, dev/test |
| **Ultra Disk** | 160,000 | $$$$ | Extreme performance |

{: .tip }
**Exam:** Premium SSD requires a Premium-capable VM size (e.g. D2s_v3 has the "s" suffix = supports Premium Storage).

---

## Availability

```
No redundancy:          Single point of failure, no SLA on hardware
Availability Set:       VMs spread across fault + update domains (99.95% SLA)
Availability Zones:     VMs in separate data centres (99.99% SLA)  ← preferred
Region pairs:           Full regional failover (DR scenario)
```

### Availability Sets
- **Fault domains** (FD): Separate physical racks, power, networking
- **Update domains** (UD): Patched in sequence so not all VMs restart at once
- Max 3 FDs, 20 UDs per set
- VMs in same set = 99.95% SLA for multi-instance

### Availability Zones
- Physically separate data centres with independent power, cooling, networking
- 2+ VMs across zones = **99.99% SLA**
- Zone-redundant storage and managed disks available
- **Prefer zones over availability sets** for new deployments

---

## Virtual Machine Scale Sets (VMSS)

Auto-scale a fleet of identical VMs.

```
Load: low  →  2 VMs running
Load: high →  auto-scale to 10 VMs
Load: low  →  scale back to 2
```

- Integrated with Load Balancer or Application Gateway
- Scale based on CPU, memory, schedule, or custom metric
- **Uniform mode** — identical VMs from same image
- **Flexible mode** — mix of VM configurations

---

## VM Extensions

Install software and run scripts **after** VM creation.

| Extension | What it does |
|---|---|
| **Custom Script Extension** | Run a PowerShell or bash script |
| **DSC (Desired State Config)** | Enforce configuration state |
| **Azure Monitor Agent** | Send metrics and logs to Monitor |
| **Microsoft Antimalware** | Windows Defender configuration |
| **Domain Join** | Join VM to Active Directory domain |

---

## Remote Access

| Method | Protocol | Port | Use |
|---|---|---|---|
| **RDP** | RDP | 3389 | Windows VMs |
| **SSH** | SSH | 22 | Linux VMs |
| **Azure Bastion** | HTTPS | 443 | Secure browser-based (no public IP) |
| **Run Command** | HTTPS | — | Execute script without any connection |
| **Serial Console** | — | — | Emergency access when VM won't boot |

{: .tip }
**Exam:** Never expose RDP/SSH directly to the internet. Use Bastion or Just-In-Time VM access.

### Just-In-Time (JIT) VM Access
- Locks down RDP/SSH ports by default
- Opens port only for approved duration (e.g. 3 hours) from specific IP
- Requires Microsoft Defender for Cloud Standard

---

## Azure Containers

### Container Instances (ACI)
Fastest way to run a container — no cluster, no VMs to manage.

```
docker run → az container create
Pay per second. Gone when done.
Good for: one-off tasks, CI/CD steps, event-driven jobs
```

### Azure Kubernetes Service (AKS)
Managed Kubernetes for production container workloads.

```
Control plane: Microsoft manages (free)
Node pools:    VMs you pay for

Pods ──→ Nodes (VMs) ──→ Node Pool ──→ AKS Cluster
```

- Auto-scale node pools based on demand
- Integrate with Azure AD, Monitor, Container Registry
- Use when: microservices, many containers, need orchestration

### Azure Container Registry (ACR)
Private Docker registry in Azure. Store and manage container images.

```
Build image → push to ACR → AKS or ACI pulls from ACR
```

---

## VM Images & Templates

### Azure Compute Gallery (Shared Image Gallery)
Store and replicate custom VM images across regions. Share across subscriptions.

### ARM Templates / Bicep
Deploy VMs (and all dependencies) as code.

```json
// ARM: verbose JSON
// Bicep: cleaner syntax, same result
resource vm 'Microsoft.Compute/virtualMachines@2023-03-01' = { ... }
```

---

## Exam Checklist

- [ ] Explain the difference between Stopped and Deallocated (billing)
- [ ] Name 3 VM disk types and when each is appropriate
- [ ] Explain Availability Set vs Availability Zones (SLA difference)
- [ ] Describe VMSS and how auto-scale works
- [ ] Name 3 VM extensions and their purpose
- [ ] Explain when to use ACI vs AKS
- [ ] Explain JIT VM access and why it's better than open RDP
