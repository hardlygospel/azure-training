# 4. Security, Privacy & Compliance 🔐

## Azure Security Layers

### Physical Security 🏢
- Microsoft secures data centers
- Biometric access, 24/7 monitoring
- You: No responsibility

### Network Security 🌐
- **Network Security Groups (NSGs):** Firewall rules (allow/deny traffic)
- **Azure Firewall:** Centralized network protection
- **DDoS Protection:** Built-in and standard
- **You & Microsoft:** Shared responsibility

### Application Security 📱
- **Application Gateway:** Layer 7 protection
- **Web Application Firewall (WAF):** Protect web apps
- **API Management:** Secure API access
- **You:** Responsible for application code

### Data Security 🔒
- **Encryption at rest:** Data encrypted in storage
- **Encryption in transit:** Data encrypted when moving
- **Azure Key Vault:** Store secrets/keys/certificates
- **You:** Encrypt sensitive data, manage keys

---

## Encryption

### At Rest
- Data stored on disk/in database = encrypted
- **Service:** Transparent Server-Side Encryption (TSLE)
- **Automatic:** Yes, no action needed
- **Key management:** Customer Managed Keys (CMK) available

### In Transit
- Data moving over network = TLS/SSL encrypted
- **HTTPS:** Always use for web traffic
- **VPN/ExpressRoute:** For private connections

### Key Vault
- Centralized secret management
- Store: Passwords, keys, certificates, connection strings
- **Access:** Secure, audit-logged, role-based

---

## Access Control & Identity 👤

### Azure Active Directory (AAD / Entra ID)
- **Purpose:** User identity and access management
- **Single Sign-On (SSO):** One login for multiple apps
- **Multi-Factor Authentication (MFA):** Username + password + phone
- **Application registration:** Grant app permissions

### Role-Based Access Control (RBAC)
- **Principle:** Least privilege (minimum permissions needed)
- **Components:**
  - **Security Principal:** User, group, service principal
  - **Role:** Set of permissions (Reader, Contributor, Owner)
  - **Scope:** Subscription, Resource Group, Resource

### Built-in Roles
| Role | Permissions |
|------|------------|
| **Owner** | Full access, can assign roles |
| **Contributor** | Create/modify, cannot assign roles |
| **Reader** | View only, no changes |
| **User Access Admin** | Manage role assignments |

### Custom Roles
- Define exactly what users can do
- Fine-grained permissions

---

## Network Security

### Network Security Groups (NSGs)
- **Firewall rules** at VM level
- **Allow/Deny** specific traffic (ports, protocols, IPs)
- **Inbound rules:** Control incoming traffic
- **Outbound rules:** Control outgoing traffic

### Example NSG Rule
```
Allow HTTP (port 80) from internet to VMs
Allow RDP (port 3389) from admin IP only
Deny all other traffic
```

### Application Security Groups (ASGs)
- Group VMs logically (tag-based)
- Apply NSG rules to groups, not individual IPs

---

## Compliance & Privacy 📋

### Azure Compliance Offerings
Microsoft maintains certifications for:
- **GDPR:** EU data protection
- **HIPAA:** Healthcare data
- **PCI-DSS:** Credit card data
- **FedRAMP:** US government
- **SOC 2:** Service organization security

### Your Responsibility
- **Data residency:** Choose region where data lives
- **Data classification:** Mark what's sensitive
- **Encryption:** Encrypt sensitive data
- **Audit logs:** Enable monitoring

---

## Azure Policy & Governance

### Azure Policy
- **Enforce standards** across resources
- **Prevent non-compliant** resources
- **Example:** "All VMs must have tags"

### Initiative
- **Collection of policies** (group related rules)

### Management Groups
- **Organize subscriptions** hierarchically
- **Apply policies** at multiple levels
- **Example:** Corporate > Business Unit > Subscription

---

## Shared Responsibility Model

| Area | Microsoft | You |
|------|-----------|-----|
| **Physical security** | ✓ | |
| **Network infrastructure** | ✓ | |
| **Hypervisor** | ✓ | |
| **OS** | Managed services | IaaS VMs |
| **Application** | | ✓ |
| **Data** | | ✓ |
| **Access control** | Framework | User/password |
| **Compliance** | Certifications | Implementation |

---

## Security Tools

| Tool | Purpose |
|------|---------|
| **Azure Security Center** | Security recommendations |
| **Azure Sentinel** | SIEM (Security info event management) |
| **Azure Defender** | Threat detection |
| **Network Watcher** | Monitor/troubleshoot network |

---

## DDoS Protection

### Standard (Included)
- Basic protection (no extra cost)
- Automatic mitigation
- Sufficient for most workloads

### Premium
- Advanced protection
- DDoS attack notifications
- Cost: ~$3,000/month
- For critical services only

---

## Data Privacy & Residency

### Data Residency
- **You choose:** Which region stores your data
- **Exceptions:** Backup copies, service logs, replication
- **Compliance:** GDPR requires EU data stay in EU

### Sovereign Clouds
- **Azure Government:** For US government workloads
- **Azure China:** For China-based organizations
- Separate from public Azure

---

## Exam Tips

- **Shared Responsibility:** Microsoft = infrastructure; You = data & apps
- **RBAC:** Least privilege principle
- **NSG:** Firewall rules (allow/deny)
- **MFA:** Required for security-critical roles
- **Encryption:** At rest AND in transit
- **Compliance:** Microsoft provides frameworks; you implement
- **Data residency:** Choose your region wisely
- **Key Vault:** For secrets, not application code
