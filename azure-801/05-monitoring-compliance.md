# 5. Monitoring & Compliance 📊

## Azure Monitor

### What Is Azure Monitor?
- **Centralized monitoring** for all Azure resources
- **Metrics, logs, traces**
- **Alerts** when problems detected
- **Dashboards** for visualization

### Components

**Metrics:**
- **Numeric data** (CPU %, RAM, disk I/O)
- **Real-time** (near-instant)
- **Retention:** 93 days
- **Multi-dimensional:** Filter by region, VM name, etc.

**Logs (Analytics):**
- **Detailed events** (application logs, errors)
- **Query with KQL** (Kusto Query Language)
- **Retention:** 30-730 days (configurable)
- **Slower** than metrics (but more detailed)

**Application Insights:**
- **Application monitoring** (exceptions, performance)
- **Detect issues** users experience
- **User analytics**
- **Dependency tracking** (calls to APIs, databases)

### Data Flow
```
Resource → Monitor → Diagnostic Settings → Storage/Logs
                   ↓
              Metrics (fast)
              Alerts
```

---

## Log Analytics

### What Is KQL?
- **Query language** for Azure Logs
- **Similar to SQL** (but simpler)
- **Retrieve and analyze** logs

### Simple KQL Examples
```kusto
// Find all errors from past 24 hours
Syslog
| where Severity == "ERROR"
| where TimeGenerated > ago(24h)

// Count requests by response code
requests
| summarize count() by resultCode
| order by count() desc

// Find slow queries
requests
| where duration > 5000
| project timestamp, name, duration
```

### Workspaces
- **Container** for logs
- **Regional** (you choose)
- **Billing unit**
- **Access control** (RBAC)

---

## Alerts & Actions

### Alert Rules
```
IF metric exceeds threshold
THEN execute action
```

### Metrics Alerts
- **Monitor metrics** (CPU, memory)
- **Simple conditions** (CPU > 80%)
- **Fast** (seconds to alert)

### Log Alerts
- **Monitor logs** via query
- **Complex conditions** (errors from specific service)
- **Slower** (query takes time)

### Alert Actions
| Action | Example |
|--------|---------|
| **Email** | admin@company.com |
| **SMS** | Send text to phone |
| **Webhook** | Call external API |
| **Runbook** | Auto-remediate (VM restart) |
| **Logic App** | Complex automation |

### Action Groups
- **Reusable** set of actions
- **Email A, SMS B, Webhook C** together
- **Apply to multiple** alerts

---

## Application Insights

### Key Features
- **Exception tracking** (errors)
- **Performance monitoring** (slow requests)
- **Dependency tracking** (calls to APIs, databases)
- **User analytics** (sessions, page views)
- **Custom events** (business metrics)

### Instrumentation
```
Install SDK → Send telemetry → Application Insights → Analyze
```

### Performance Counters
- **Server response time** (p50, p95, p99)
- **Request volume**
- **Availability** (synthetic monitoring)
- **Dependency performance** (database queries)

---

## Azure Advisor

### What Is It?
- **AI recommendations** based on your resources
- **5 categories:**
  - **Cost:** Save money
  - **Reliability:** Improve HA
  - **Performance:** Speed up
  - **Operational Excellence:** Best practices
  - **Security:** Security issues

### Common Recommendations
- **Unused resources:** Delete (save money)
- **Reserved instances:** Buy (save 30-70%)
- **Availability:** Add redundancy
- **Security:** Enable MFA, patch VMs

---

## Diagnostic Settings

### What It Does
- **Route logs/metrics** to storage
- **Archive to:** Log Analytics, Storage, Event Hubs
- **Enable monitoring** of resources

### Typical Setup
```
Azure Resource
  → Diagnostic Settings
    → Send metrics to Log Analytics (query)
    → Send logs to Storage (archive)
    → Send to Event Hubs (stream to SIEM)
```

---

## Azure Security Center

### Capabilities
- **Security recommendations** (patching, firewalls)
- **Threat detection** (suspicious activity)
- **Vulnerability scanning** (exposed databases, weak settings)
- **Compliance assessment** (HIPAA, GDPR, etc.)

### Secure Score
- **0-100 metric** of security posture
- **Recommendations** to improve
- **Track improvement** over time

---

## Compliance & Policy

### Azure Policy

**What It Does:**
- **Enforce** governance rules
- **Prevent** non-compliant resources
- **Audit** for compliance

**Example Policies:**
- "All VMs must have tags"
- "Storage accounts must use HTTPS"
- "VMs must use managed disks"
- "Databases must have encryption"

**Enforcement:**
- **Audit:** Report violations (don't block)
- **Deny:** Block non-compliant resource creation
- **Audit + Append:** Report + add default values

### Policy Assignments
```
Policy: "All VMs must have backup"
Scope: Resource Group "Production"
Effect: Deny (reject VM creation if no backup)
```

### Initiatives
- **Collection of policies** (group related)
- **Example:** "CIS Azure Foundations" (20+ policies)

### Policy Effects
| Effect | What Happens |
|--------|-------------|
| **Audit** | Report violation (allow creation) |
| **Deny** | Block resource creation |
| **Append** | Add missing properties |
| **Modify** | Change resource properties |
| **Disabled** | Policy ignored |

---

## Compliance Offerings

### Built-in Certifications
- **GDPR:** EU data protection
- **HIPAA:** Healthcare (US)
- **PCI-DSS:** Payment cards
- **FedRAMP:** US government
- **SOC 2:** Service organization
- **ISO 27001:** Information security

### Compliance Manager
- **Track** compliance status
- **Microsoft assessments** (what's done)
- **Customer actions** (what you must do)
- **Improvement actions** → increase score

---

## Governance Best Practices

### Naming Convention
```
company-environment-resource-instance
Example: acme-prod-vm-web01
```

### Tagging Strategy
```
Tags: Cost Center, Environment, Owner, Application
Examples:
- costcenter: 1234
- environment: production
- owner: alice@acme.com
- application: website
```

### Resource Organization
```
Management Group (Corp)
├── Production
│   ├── RG-WebServers
│   ├── RG-Databases
├── Non-Production
│   ├── RG-Dev
│   ├── RG-Test
```

---

## Backup Compliance

### Backup Policies
- **Retention:** 7 years typical
- **Encryption:** Customer-managed keys
- **Geo-redundant:** Secondary region
- **Audit logs:** Track access

### RTO/RPO Targets
| Service | RTO | RPO |
|---------|-----|-----|
| **VMs** | 2 hours | 1 day |
| **Databases** | 1 hour | 5 minutes |
| **File shares** | 1 hour | 1 hour |

---

## Exam Tips

- **Monitor:** Metrics + Logs
- **Metrics:** Real-time, 93-day retention
- **Logs:** Detailed, 30-730 days retention
- **Alert:** When metric exceeds threshold
- **Advisor:** Recommendations (cost, reliability, etc.)
- **Security Center:** Security score + recommendations
- **Policy:** Enforce rules (audit/deny)
- **Compliance Manager:** Track compliance status
- **Diagnostic Settings:** Route logs to storage
- **KQL:** Query language for logs
- **Tagging:** Organize resources (cost tracking)
