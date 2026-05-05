---
title: 1. Identity & Access
parent: Azure Administrator (AZ-801)
nav_order: 1
---

# Identity & Access Management

[![AZ-801](https://img.shields.io/badge/AZ--801-Domain%201-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-20--25%25-f59e0b?style=flat-square)]()

---

## Azure Active Directory (Entra ID)

Your cloud **identity directory**. Every user, group, app, and device lives here.

| Concept | Description |
|---|---|
| **Tenant** | Your organisation's AAD instance |
| **User** | A person with a login |
| **Group** | Collection of users for bulk permissions |
| **Service Principal** | App/service identity (has client ID + secret) |
| **Managed Identity** | Azure resource identity — no password needed |
| **Guest User** | External person invited via B2B |

{: .tip }
**Prefer Managed Identity** over Service Principal wherever possible — no secrets to rotate.

---

## User Types

| Type | Created in | Synced from | Use |
|---|---|---|---|
| **Cloud-only** | Azure AD | — | Pure cloud environment |
| **Synced** | On-prem AD | Azure AD Connect | Hybrid environment |
| **Guest** | Invitation | External tenant | Partners, contractors |

### Azure AD Connect
Syncs on-premises Active Directory → Azure AD.

```
On-prem AD  ──[Azure AD Connect]──→  Azure AD (Entra ID)
Users, groups, passwords synced continuously
```

Options:
- **Password Hash Sync** — Hash synced to cloud (simplest, recommended)
- **Pass-through Auth** — Auth happens on-prem (no hash leaves network)
- **Federation (ADFS)** — Complex, mostly legacy

---

## Authentication

### Multi-Factor Authentication (MFA)

| Method | Strength |
|---|---|
| **FIDO2 / Windows Hello** | Strongest — phishing-resistant |
| **Authenticator app (push)** | Strong |
| **Authenticator app (TOTP)** | Good |
| **SMS / phone call** | Weak — SIM-swap vulnerable |

### Conditional Access
Policy engine: **if** conditions → **then** grant/block/require MFA.

```
IF:  User is in "Finance" group
AND: Signing in from outside corporate network
AND: Device is not compliant
THEN: Block access
```

Common conditions: location, device compliance, sign-in risk, user group, app being accessed.

---

## Role-Based Access Control (RBAC)

```
Principal   +   Role definition   +   Scope   =   Permission
(who)           (what actions)        (where)

Example:
Alice  +  Contributor  +  /subscriptions/abc123/resourceGroups/Prod
= Alice can do anything in the Prod resource group
```

### Assignment Process (Portal)
1. Navigate to resource / RG / subscription
2. **Access control (IAM)** → **Add role assignment**
3. Select role → Select member → Save

### Scope Hierarchy
```
Management Group  (highest — inheritance flows down)
  └── Subscription
        └── Resource Group
              └── Resource  (most specific — overrides higher)
```

**Most specific scope wins.** Deny at any level overrides Allow.

### Built-in Roles

| Role | Create/Edit | Delete | Assign roles |
|---|---|---|---|
| **Owner** | ✓ | ✓ | ✓ |
| **Contributor** | ✓ | ✓ | ✗ |
| **Reader** | ✗ | ✗ | ✗ |
| **User Access Administrator** | ✗ | ✗ | ✓ |

### Custom Roles
When no built-in role fits. Define exact allowed actions.

```json
{
  "Name": "VM Operator",
  "Actions": [
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Compute/virtualMachines/read"
  ],
  "NotActions": [],
  "AssignableScopes": ["/subscriptions/your-sub-id"]
}
```

{: .tip }
Custom roles are created at subscription or management group scope, then assigned anywhere within that scope.

---

## Managed Identities

Azure handles credentials automatically — no secrets stored anywhere.

| Type | Lifecycle | Use when |
|---|---|---|
| **System-assigned** | Created/deleted with resource | One resource needs identity |
| **User-assigned** | Independent resource | Multiple resources share same identity |

### How to use (example: VM accessing Key Vault)
1. Enable managed identity on VM
2. Assign Key Vault role to that identity
3. VM gets token automatically from IMDS (169.254.169.254)
4. No credentials in code

---

## Privileged Identity Management (PIM)

Just-in-time privileged access — roles are **eligible** not **permanent**.

```
Normal day → User has Reader role
Need admin access → Request elevation (approval required)
After task → Role expires automatically
```

Benefits: reduces standing privileged access, full audit trail, requires justification.

---

## Administrative Units

Delegate administration to a subset of users.

```
Global Admin sets up:
  AU: "Sydney Office"
  Assigns: Sydney IT team as User Admin for that AU only
  Result: Sydney IT can manage Sydney users — can't touch Melbourne
```

Use for large organisations with regional IT teams.

---

## Exam Checklist

- [ ] Explain cloud-only vs synced vs guest users
- [ ] Name 3 MFA methods and rank by strength
- [ ] Explain Conditional Access — conditions and controls
- [ ] Assign a role at resource group scope in the portal
- [ ] Explain scope inheritance (management group → resource)
- [ ] Explain system-assigned vs user-assigned managed identity
- [ ] Describe when to use a custom role
- [ ] Explain PIM and why it's used
