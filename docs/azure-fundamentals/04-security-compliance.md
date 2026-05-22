
# Security, Privacy & Compliance

[![AZ-900](https://img.shields.io/badge/AZ--900-Domain%204-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-25--30%25-f59e0b?style=flat-square)]()

---

## Shared Responsibility Model

```
ALWAYS MICROSOFT:          ALWAYS YOU:            DEPENDS ON MODEL:
─────────────────          ───────────            ─────────────────
Physical security          Your data              OS patches (IaaS = you, PaaS = MS)
Data centre                User accounts          App security (IaaS/PaaS = you)
Network infrastructure     Identity config        Encryption keys (optional)
Hypervisor                 Compliance actions
```

| Responsibility | IaaS | PaaS | SaaS |
|---|---|---|---|
| Data & identities | You | You | You |
| Applications | You | You | Microsoft |
| OS & middleware | You | Microsoft | Microsoft |
| Infrastructure | Microsoft | Microsoft | Microsoft |

{: .tip }
**Exam:** You are **always** responsible for your data and user accounts, regardless of service model.

---

## Azure Active Directory (Entra ID)

Microsoft's cloud **identity platform** — not the same as on-premises Active Directory.

| Feature | Description |
|---|---|
| **Single Sign-On (SSO)** | One login for Azure, Microsoft 365, and third-party apps |
| **Multi-Factor Authentication** | Password + second factor (app, SMS, hardware key) |
| **Conditional Access** | Policy-based access (block risky sign-ins) |
| **B2B / B2C** | Invite external users or support consumer identities |

### Authentication Strength (best → weakest)
1. Passwordless (FIDO2 key, Windows Hello)
2. Authenticator app (push notification)
3. SMS / voice code
4. Password alone *(never use for production)*

{: .tip }
**Exam:** Azure AD is not on-prem AD. You use **Azure AD Connect** to sync on-prem AD users to Azure AD.

---

## Role-Based Access Control (RBAC)

Grant access using **minimum permissions needed** (principle of least privilege).

```
Who (Security Principal) + What (Role) + Where (Scope) = Access

Example:
  Alice   +   Contributor   +   Resource Group "Prod"
  = Alice can create/edit anything in that resource group
```

### Built-in Roles

| Role | Can do | Can't do |
|---|---|---|
| **Owner** | Everything | — |
| **Contributor** | Create & manage resources | Assign roles |
| **Reader** | View only | Anything |
| **User Access Administrator** | Manage role assignments | Manage resources |

### Scope (permission flows downward)

```
Management Group
  └── Subscription       ← assign here = applies to all below
        └── Resource Group
              └── Resource   ← narrowest scope
```

---

## Network Security

### Network Security Groups (NSGs)
Stateful firewall rules applied to **subnets or individual VMs**.

```
Rule anatomy:
  Priority (100–4096) | Source | Port | Protocol | Action (Allow/Deny)

Lower priority number = evaluated first
Explicit Deny beats Allow at same level
```

### Azure Firewall
- Centrally managed, cloud-native firewall
- Supports FQDN filtering, threat intelligence, forced tunnelling
- More powerful than NSG — use for hub-spoke networks

### DDoS Protection

| Tier | Cost | Protection |
|---|---|---|
| **Network (Basic)** | Free | Always-on, automatic |
| **IP Protection** | Per IP | Adds telemetry, rapid response |
| **Network Protection** | ~$2,944/month | Full protection, SLA, DDoS experts |

---

## Encryption

| Where | How |
|---|---|
| **At rest** | Azure Storage Service Encryption (automatic) |
| **In transit** | TLS 1.2+ enforced |
| **Managed keys** | Microsoft manages by default |
| **Customer-managed keys** | You bring your own key via Azure Key Vault |

### Azure Key Vault
Centralised storage for **secrets, keys, and certificates**.

- Store: connection strings, API keys, passwords, TLS certificates
- Access: RBAC controlled, audit-logged
- **Never hard-code secrets in application code**

---

## Microsoft Defender for Cloud

Formerly Security Center. Provides:

| Feature | What it does |
|---|---|
| **Secure Score** | 0–100 rating of your security posture |
| **Recommendations** | Specific steps to improve score |
| **Regulatory compliance** | Map your environment to standards |
| **Threat protection** | Detect and alert on active attacks |

---

## Privacy & Compliance

### Microsoft's Commitments
- **Online Services Terms (OST)** — What Microsoft does with your data
- **Data Protection Addendum (DPA)** — GDPR compliance commitments
- **Microsoft Privacy Statement** — How Microsoft handles personal data

### Compliance Certifications Azure Holds
`GDPR` `HIPAA` `PCI-DSS` `FedRAMP` `ISO 27001` `SOC 1/2/3` `IRAP (Australia)`

{: .note }
Microsoft holds the certifications. **You** are responsible for configuring your workloads to meet the standards.

### Azure Policy
Enforce governance rules across subscriptions.

```
Policy: "Storage accounts must use HTTPS only"
Effect:
  Audit     → report violations, allow creation
  Deny      → block non-compliant resource creation
  Modify    → auto-fix the property
```

### Microsoft Compliance Manager
- Dashboard showing compliance status against frameworks
- Lists what Microsoft has done and what **you** must do
- Available in Microsoft Purview

---

## Governance Tools Summary

| Tool | Purpose |
|---|---|
| **Azure Policy** | Enforce configuration standards |
| **Resource Locks** | Prevent accidental delete/modify |
| **Blueprints** (legacy) | Package policies + RBAC + templates |
| **Management Groups** | Apply policy across subscriptions |
| **Tags** | Metadata for cost tracking and filtering |

### Resource Locks

| Lock type | Can read | Can modify | Can delete |
|---|---|---|---|
| **Read-only** | Yes | No | No |
| **Delete** | Yes | Yes | No |

{: .tip }
**Exam:** Locks override RBAC. Even Owners can't delete a resource with a Delete lock unless they remove it first.

---

## Exam Checklist

- [ ] Explain the shared responsibility model for IaaS/PaaS/SaaS
- [ ] Explain RBAC — who, what role, which scope
- [ ] Name the 4 built-in roles and what each can/can't do
- [ ] Explain NSG vs Azure Firewall
- [ ] Describe encryption at rest vs in transit
- [ ] Explain what Azure Key Vault is for
- [ ] Describe the difference between Audit and Deny policy effects
- [ ] Explain resource locks (read-only vs delete)
