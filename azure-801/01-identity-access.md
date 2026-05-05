# 1. Identity & Access Management 👤

## Azure Active Directory (Entra ID)

### What is AAD?
- **Identity provider** for Azure and Microsoft services
- **Single Sign-On (SSO)** across applications
- **Directory:** Contains users, groups, and applications
- **Tenant:** Your organization's AAD instance

### Key Concepts
- **User Account:** Real person
- **Service Principal:** App/service identity
- **Managed Identity:** AAD identity for Azure resources (no password needed)
- **Guest User:** External user invited to tenant

---

## User & Group Management

### Creating Users
- **Cloud-only:** Create directly in AAD
- **Synced:** From on-premises Active Directory (Azure AD Connect)

### Guest Users
- **Invite external users** (contractors, partners)
- **Limited permissions** by default
- **B2B Collaboration:** Cross-org access

### Groups
- **Security groups:** For access control (RBAC)
- **Microsoft 365 groups:** For collaboration (Teams, SharePoint)
- **Distribution lists:** Email grouping (on-prem)

### Dynamic Groups
- **Automatic membership** based on rules
- **Example:** All marketing department users automatically added

---

## Authentication Methods

### Traditional
- **Username + Password:** Basic, not recommended for production
- **Multi-Factor Authentication (MFA):** Required for security

### Modern Authentication
- **Windows Hello:** Biometric/PIN
- **FIDO2:** Security key (hardware token)
- **Passwordless sign-in:** App approval or phone sign-in

### MFA Options
1. **Microsoft Authenticator App:** Notification approval
2. **SMS:** Text message code
3. **Voice Call:** Phone verification
4. **Hardware token:** Time-based OTP device

**Best Practice:** Passwordless + MFA for critical accounts

---

## Role-Based Access Control (RBAC)

### How RBAC Works
```
Security Principal + Role + Scope = Permission
(User/Group)      (Permissions) (Resource level)
```

### Assignment Process
1. Go to resource (VM, RG, subscription)
2. Add Role Assignment
3. Select role (Reader, Contributor, Owner, custom)
4. Select user/group/service principal
5. Save

### Scope Levels (top to bottom)
- **Management Group:** Multiple subscriptions
- **Subscription:** Entire subscription
- **Resource Group:** All resources in RG
- **Resource:** Single VM, database, etc.

### Permission Inheritance
- Permissions flow **down** (inheritance)
- Assign at higher scope = applies to everything below
- Most specific permission **wins**

---

## Built-in Roles (Key Ones)

| Role | What They Can Do | Best For |
|------|-----------------|----------|
| **Owner** | Everything + assign roles | Admin users |
| **Contributor** | Create/modify (no role assignment) | Developers |
| **Reader** | View only | Auditors |
| **User Access Admin** | Manage role assignments only | Access control team |
| **Virtual Machine Contributor** | Manage VMs only | VM-specific admins |

---

## Custom Roles

### When to Create Custom Roles
- **Existing roles too permissive**
- **Need specific permission combination**
- **Compliance requirement:** Least privilege

### Custom Role Structure
```json
{
  "Name": "VM Restarter",
  "Permissions": [
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Compute/virtualMachines/read"
  ]
}
```

---

## Service Principals & Managed Identities

### Service Principal (App Identity)
- **App registration** in AAD
- **Username/password** (not recommended)
- **Certificate-based** (secure)
- **Use case:** App needs Azure API access

### Managed Identity
- **No password management**
- **Automatic credential rotation**
- **AAD-issued token** automatically
- **Recommended:** For Azure resources

#### Types of Managed Identity
- **System-assigned:** One per resource (created/deleted with resource)
- **User-assigned:** Created separately, reusable across resources

### Example: VM with Managed Identity
1. Enable managed identity on VM
2. Assign role to managed identity
3. VM automatically gets token
4. No credentials stored

---

## Conditional Access

### What Is It?
- **Policy-based access** (if-then rules)
- **Block or grant** based on conditions
- **No passwords needed** in some scenarios

### Common Conditions
- **Location:** Block access from outside corporate network
- **Device:** Require compliant device
- **Risk:** Block risky sign-in attempts
- **User/Group:** Different rules for different people

### Example Policy
```
IF user signs in from foreign country
AND device is not enrolled
THEN block access
ELSE require MFA
```

---

## Azure AD Connect

### Purpose
- **Sync** on-premises AD users to Azure AAD
- **One identity** across cloud and on-prem
- **Seamless experience** (users same username everywhere)

### Two Modes
- **Password Hash Sync:** Hashes synced (simple)
- **Pass-Through Auth:** Authentication happens on-prem
- **Federation (ADFS):** Complex, legacy

### What Gets Synced?
- User accounts
- Groups
- Email addresses
- Home directory path
- License assignments

---

## Administrative Units (AUs)

### Purpose
- **Delegate admin** to non-global admins
- **Scope:** User accounts in specific OU only
- **Use case:** Multi-tenant, large organizations

### Example
```
AU: "Sales Department"
Admin: Can only manage users in Sales AU
Cannot touch HR or Finance users
```

---

## Exam Tips

- **RBAC:** Principle of least privilege (most important)
- **Scope:** Highest level = most impact (assign carefully)
- **MFA:** Always recommended for production
- **Managed Identity:** Preferred over certificates
- **Custom Roles:** Only when built-in roles don't fit
- **Service Principal:** For apps; Managed Identity preferred
- **Azure AD Connect:** For hybrid (on-prem + cloud)
- **Conditional Access:** For policy-based security
