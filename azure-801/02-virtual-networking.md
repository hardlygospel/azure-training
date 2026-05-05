# 2. Virtual Networking 🌐

## Virtual Networks (VNets) Overview

### What Is a VNet?
- **Isolated network** in Azure
- **Your own IP address space**
- **Contains subnets, VMs, services**
- **Regional:** Single region per VNet

### VNet Basics
- **Address space:** CIDR notation (e.g., 10.0.0.0/16 = 65,536 IPs)
- **Subnets:** Divide address space further (10.0.0.0/24 = 256 IPs)
- **Gateway:** Connect to on-premises or other VNets
- **DNS:** Azure-provided or custom

---

## Subnets

### Purpose
- **Divide VNet** into logical segments
- **Apply policies** (NSG) at subnet level
- **IP management:** Control IP ranges

### Subnet Planning
- **Web tier:** 10.0.1.0/24 (256 IPs)
- **App tier:** 10.0.2.0/24 (256 IPs)
- **Database tier:** 10.0.3.0/24 (256 IPs)
- **Reserved:** Gateway, firewall, etc.

### Reserved IPs (Cannot Use)
- **.0** = Network address
- **.1** = Gateway
- **.2, .3** = DNS
- **.255** = Broadcast
- **5 IPs minimum reserved** per subnet

---

## Network Security Groups (NSGs)

### What Is an NSG?
- **Firewall rules** at subnet or VM level
- **Allow or deny** traffic
- **Source/Destination:** IP, CIDR, service tag
- **Port/Protocol:** Specific or any

### NSG Rule Structure
```
Direction: Inbound or Outbound
Priority: 100-4096 (lower = process first)
Name: Descriptive
Source: IP, CIDR, Service Tag
Protocol: TCP, UDP, ICMP, Any
Port: 80, 443, range, or *
Action: Allow or Deny
```

### Common Rules
| Direction | Source | Port | Action | Purpose |
|-----------|--------|------|--------|---------|
| Inbound | Internet | 80 | Allow | HTTP traffic |
| Inbound | Internet | 443 | Allow | HTTPS traffic |
| Inbound | Internet | 3389 | Deny | Block RDP (use Bastion) |
| Inbound | 10.0.0.0/8 | 1433 | Allow | SQL from internal |
| Outbound | Any | Any | Allow | Default (allow all out) |

### Service Tags
- **Predefined IP ranges** for Azure services
- **Example:** "AzureCloud" = all Azure IPs
- **Use case:** Allow traffic to specific Azure service

### Application Security Groups (ASGs)
- **Group resources logically**
- **Tag-based** (not IP-based)
- **Cleaner NSG rules**

### NSG Effective Rules
- **Order matters:** Lower priority number = higher precedence
- **Deny overrides Allow**
- **Check both inbound/outbound**
- **VM NSG + Subnet NSG both apply**

---

## IP Addressing

### Public IP
- **Internet-routable** address
- **Static or Dynamic**
- **Static preferred** (doesn't change)
- **Cost:** ~$3/month for unused

### Private IP
- **Internal only** (10.x, 172.x, 192.x)
- **Assignment:** Static or Dynamic
- **VM always has** at least one

### Network Interfaces (NICs)
- **Attach IP addresses** to VMs
- **VM can have multiple NICs** (different subnets)
- **Each NIC = private IP + optional public IP**

---

## Routing

### System Routes (Default)
- **Automatic** created by Azure
- **Route:** Traffic within VNet goes directly
- **0.0.0.0/0 (default):** Goes to internet

### Custom Routes (Route Table)
- **Override default** routing
- **Next hop:** VM, VPN gateway, firewall, internet
- **Use case:** Force traffic through firewall

### Route Priority
1. **Most specific route** wins (longest prefix match)
2. **System routes** before custom routes
3. **If no match:** Drop or route to default

### User Defined Routes (UDR)
```
Example: Route 192.168.0.0/16 through Firewall VM
- Destination: 192.168.0.0/16
- Next hop type: Virtual appliance
- Next hop IP: 10.0.0.4 (Firewall VM)
```

---

## Connectivity

### VNet-to-VNet Peering
- **Connect two VNets** directly
- **Low latency, high bandwidth**
- **No encryption** (private link)
- **Transitive peering:** No (A-B, B-C ≠ A-C)

### Site-to-Site VPN
- **Connect on-premises to Azure**
- **Over internet** (encrypted)
- **Slower** than ExpressRoute
- **Cost:** Cheaper than ExpressRoute

### ExpressRoute
- **Dedicated private link**
- **Higher speed, lower latency**
- **Expensive** ($50-350/month)
- **No internet** traffic

### VPN Gateway
- **Manages VPN connections**
- **Located in subnet** (GatewaySubnet required)
- **Requires:** VNet with /27 or larger subnet
- **Policy-based or Route-based**

---

## Network Watcher

### Features
- **IP Flow Verify:** Check if traffic allowed
- **Next Hop:** Trace routing path
- **Connection Troubleshoot:** Test connectivity
- **NSG Flow Logs:** Monitor NSG traffic
- **Packet Capture:** Capture packets for analysis

### Use Cases
- **VM can't connect?** IP Flow Verify
- **Traffic going wrong way?** Next Hop
- **Too much traffic?** NSG Flow Logs

---

## Azure Firewall vs NSG

| Feature | NSG | Azure Firewall |
|---------|-----|----------------|
| **Level** | VM/Subnet | Network-wide |
| **Stateful** | Yes | Yes |
| **FQDN filtering** | No | Yes |
| **Threat intelligence** | No | Yes |
| **Cost** | Free | ~$1.25/hour |
| **Best for** | Simple rules | Enterprise |

---

## DNS

### Azure-Provided DNS
- **Automatic** for all VNets
- **Recursive resolver** (168.63.129.16)
- **Sufficient for most** scenarios

### Custom DNS
- **Configure DNS servers** in VNet
- **Point to:** Custom DNS servers
- **Use case:** On-premises AD, special requirements

### Private DNS Zones
- **Internal DNS** within VNet
- **Not visible** to internet
- **Useful for:** Multiple VNets sharing DNS

---

## Load Balancing

### Load Balancer (Layer 4)
- **Distribute TCP/UDP** traffic
- **Low cost**
- **Best for:** Simple load balancing

### Application Gateway (Layer 7)
- **HTTP/HTTPS** aware
- **URL-based routing** (/api → backend1, /images → backend2)
- **SSL termination**
- **Web Application Firewall** (WAF)

### Front Door (Global)
- **Geo-redundant load balancing**
- **Global load balancing**
- **Route to nearest region**

---

## Exam Tips

- **VNet:** Region-specific, isolated network
- **Subnet:** Divide VNet, apply NSG
- **NSG:** Stateful firewall (deny overrides allow)
- **Service Tag:** Predefined Azure IP ranges
- **Private vs Public IP:** Private = internal, Public = internet
- **Routing:** Most specific route wins
- **Peering:** Direct VNet-to-VNet (not transitive)
- **VPN vs ExpressRoute:** VPN cheaper, ER faster/private
- **Firewall vs NSG:** NSG = simple, Firewall = advanced
