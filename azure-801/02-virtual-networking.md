---
title: 2. Virtual Networking
parent: Azure Administrator (AZ-801)
nav_order: 2
---

# Virtual Networking

[![AZ-801](https://img.shields.io/badge/AZ--801-Domain%202-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-15--20%25-f59e0b?style=flat-square)]()

---

## Virtual Networks (VNets)

Your **private network** in Azure. Resources inside a VNet can talk to each other by default. Nothing gets in or out without you configuring it.

```
VNet: 10.0.0.0/16  (65,536 IPs)
  ├── Subnet: Web       10.0.1.0/24  (251 usable IPs)
  ├── Subnet: App       10.0.2.0/24
  ├── Subnet: Database  10.0.3.0/24
  └── Subnet: GatewaySubnet  10.0.255.0/27  (required for VPN/ER gateway)
```

**VNet rules:**
- Regional (one region per VNet)
- Address space must not overlap with peered VNets
- Azure reserves **5 IPs** per subnet (.0, .1, .2, .3, .255)

---

## Network Security Groups (NSGs)

Stateful firewall rules. Attach to a **subnet** (recommended) or individual NIC.

### Rule Structure
```
Priority | Name      | Source        | Port | Protocol | Action
100      | Allow-80  | Internet      | 80   | TCP      | Allow
200      | Allow-443 | Internet      | 443  | TCP      | Allow
300      | Deny-RDP  | Internet      | 3389 | TCP      | Deny
65000    | (default) | VirtualNetwork| *    | *        | Allow
65500    | (default) | *             | *    | *        | Deny
```

- **Lower priority number = evaluated first**
- **Deny beats Allow** at same priority
- Default rules (65000+) can't be deleted but can be overridden
- NSG applied to both subnet AND NIC — both evaluated (more restrictive wins)

### Service Tags
Pre-defined IP ranges for Azure services — use instead of manually listing IPs.

| Tag | Represents |
|---|---|
| `Internet` | All public IPs |
| `VirtualNetwork` | VNet + peered VNets |
| `AzureLoadBalancer` | Azure health probe IPs |
| `Storage` | All Azure Storage IPs |
| `Sql` | All Azure SQL IPs |

{: .tip }
**Exam:** Use service tags in NSG rules instead of specific IPs — they update automatically as Azure changes IPs.

---

## Routing

Azure creates **system routes** automatically. Override them with a **User-Defined Route (UDR)** table attached to a subnet.

```
Default system routes:
  10.0.0.0/16 → VirtualNetwork (stay in VNet)
  0.0.0.0/0   → Internet (everything else goes out)

Custom UDR example (force traffic through firewall):
  0.0.0.0/0   → Virtual Appliance (Firewall VM: 10.0.0.4)
```

**Longest prefix match wins** — more specific route takes priority.

Next hop types: `VirtualNetwork`, `Internet`, `VirtualAppliance`, `VirtualNetworkGateway`, `None`

---

## Connectivity Options

### VNet Peering
Connect two VNets directly — traffic stays on Azure backbone, not internet.

```
VNet-A (10.0.0.0/16) ←──── peering ────→ VNet-B (10.1.0.0/16)

Rules:
  ✓ Low latency, high bandwidth
  ✓ No encryption needed (private backbone)
  ✗ Not transitive: A↔B and B↔C does NOT give A↔C
  ✗ Address spaces cannot overlap
```

### Site-to-Site VPN
Connect on-premises network to Azure over encrypted internet tunnel.

```
On-prem network ──[IPSec/IKE]──→ VPN Gateway ──→ Azure VNet
                   (internet)
```
- Requires **VPN Gateway** in a `GatewaySubnet` (/27 or larger)
- **Policy-based** (static, legacy) vs **Route-based** (dynamic, recommended)
- Speed: up to 10 Gbps (VpnGw5)

### ExpressRoute
Private dedicated circuit — never touches the internet.

```
On-prem  ──[carrier circuit]──→ ExpressRoute edge ──→ Azure VNet
```

| | VPN Gateway | ExpressRoute |
|---|---|---|
| Path | Internet (encrypted) | Private circuit |
| Latency | Higher | Lower |
| Speed | Up to 10 Gbps | Up to 100 Gbps |
| SLA | 99.9% | 99.95% |
| Cost | Cheap | Expensive |
| Setup | Hours | Weeks |

{: .tip }
**Exam:** ExpressRoute = private, not internet. Use when compliance or latency matters. VPN = good enough for most.

---

## IP Addressing

| Type | Scope | Assignment |
|---|---|---|
| **Private IP** | Internal (10.x, 172.16–31.x, 192.168.x) | Dynamic (DHCP) or Static |
| **Public IP** | Internet-facing | Dynamic or Static |

**Always use Static public IPs** for anything that needs a consistent address (DNS records, firewall rules).

**Deallocating a VM releases a dynamic public IP** — it changes on restart. Use static to prevent this.

---

## Load Balancing

```
Internet users
      ↓
  Azure Load Balancer (Layer 4 — TCP/UDP)
      ↓
  Backend pool: VM1, VM2, VM3

  OR

  Application Gateway (Layer 7 — HTTP/HTTPS)
      ↓ routes by URL path:
      /api/*  → API servers
      /images/* → Storage
      /*      → Web servers
```

| Service | Layer | Features |
|---|---|---|
| **Load Balancer** | 4 (TCP/UDP) | Simple, fast, cheap |
| **Application Gateway** | 7 (HTTP/S) | URL routing, SSL termination, WAF |
| **Traffic Manager** | DNS-based | Global, latency/geo routing |
| **Front Door** | Global HTTP | CDN + WAF + load balance worldwide |

---

## Azure Bastion

Secure browser-based RDP/SSH — no public IP on the VM required.

```
Browser → Azure Portal → Bastion Host → VM (private IP only)
                          (in your VNet)
```

- Protects port 3389/22 from internet exposure
- Requires **AzureBastionSubnet** (/26 or larger)
- Cost: ~$140/month for standard tier

---

## Network Watcher

Diagnostic tools for networking issues.

| Tool | Use it to… |
|---|---|
| **IP Flow Verify** | Check if an NSG allows/blocks specific traffic |
| **Next Hop** | Find where a packet would be routed |
| **Connection Troubleshoot** | Test end-to-end TCP connectivity |
| **NSG Flow Logs** | Log which traffic was allowed/denied |
| **Packet Capture** | Capture packets on a VM's NIC |

---

## Exam Checklist

- [ ] Plan a VNet with 3 subnets and correct CIDR
- [ ] Create an NSG rule and explain priority evaluation
- [ ] Explain service tags and when to use them
- [ ] Describe UDRs and when you need a route table
- [ ] Compare VPN Gateway vs ExpressRoute
- [ ] Explain VNet peering limitations (non-transitive, no overlap)
- [ ] Compare Load Balancer vs Application Gateway
- [ ] Explain Azure Bastion and why it's preferred over public IP + RDP
