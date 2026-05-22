
# Monitoring & Compliance

[![AZ-801](https://img.shields.io/badge/AZ--801-Domain%205-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-10--15%25-f59e0b?style=flat-square)]()

---

## Azure Monitor

Central platform for **all** observability data in Azure.

```
Resources → Diagnostic Settings → Azure Monitor
                                       ├── Metrics (numbers, real-time)
                                       ├── Logs (events, queryable)
                                       ├── Alerts (notify or act)
                                       └── Dashboards / Workbooks
```

### Metrics vs Logs

| | Metrics | Logs |
|---|---|---|
| **Type** | Numeric time-series | Structured records |
| **Latency** | Near real-time (~1 min) | Minutes |
| **Retention** | 93 days (free) | 30–730 days (configurable) |
| **Query** | Chart/threshold | KQL queries |
| **Examples** | CPU %, memory %, disk IOPS | Error events, audit logs, app traces |

### Diagnostic Settings
Enable to send resource logs/metrics to:
- **Log Analytics workspace** — query with KQL
- **Storage account** — archive cheaply
- **Event Hub** — stream to SIEM (Sentinel, Splunk)

```
Resource → Diagnostic settings → Add → select destinations
```

---

## Log Analytics & KQL

### Kusto Query Language (KQL)

```kusto
-- Find all errors in last 24 hours
Syslog
| where Severity == "err"
| where TimeGenerated > ago(24h)
| project TimeGenerated, Computer, SyslogMessage

-- Count by category
AzureActivity
| where OperationNameValue contains "delete"
| summarize count() by ResourceGroup
| order by count_ desc

-- Top 10 slowest requests
requests
| where timestamp > ago(1h)
| top 10 by duration desc
| project timestamp, name, duration, resultCode
```

KQL cheat sheet:
- `|` — pipe (chain operations)
- `where` — filter
- `project` — select columns
- `summarize count() by X` — group and count
- `ago(24h)` — relative time
- `top N by field` — top N rows

---

## Alerts

### Alert Rule Components

```
Condition: CPU % > 80% for 5 minutes
Severity:  2 (Warning)
Action Group: → Email ops@company.com
              → SMS +61-xxx-xxx
              → Webhook: https://...
              → Runbook: auto-restart-vm
```

### Alert Types

| Type | Based on | Latency | Use |
|---|---|---|---|
| **Metric alert** | Metric threshold | ~1 min | CPU, memory, disk |
| **Log alert** | KQL query result | 5+ min | Error count, custom logic |
| **Activity Log alert** | Azure operation | Near-instant | Resource deleted, policy changed |

### Action Groups
Reusable set of notification/action targets. Create once, attach to many alerts.

---

## Azure Advisor

AI-powered recommendations across 5 categories:

| Category | Example recommendation |
|---|---|
| **Cost** | "Deallocate VMs running <5% CPU" |
| **Reliability** | "Add VM to availability zone" |
| **Security** | "Enable MFA on accounts with admin roles" |
| **Performance** | "Upgrade SQL tier — near DTU limit" |
| **Operational Excellence** | "Enable soft delete on storage accounts" |

---

## Azure Policy

### How Policy Works

```
Policy Definition  →  Assignment  →  Scope  →  Effect
"Must have tags"      "All VMs"      Sub/RG    Deny / Audit / Modify
```

### Policy Effects (in order of strictness)

| Effect | What happens |
|---|---|
| **Disabled** | Policy ignored |
| **Audit** | Non-compliant resource created + flagged |
| **AuditIfNotExists** | Audit if a related resource doesn't exist |
| **Append** | Add missing fields (e.g. tags) |
| **Modify** | Change resource properties on create/update |
| **Deny** | Block non-compliant resource creation |
| **DeployIfNotExists** | Deploy a related resource if missing |

{: .tip }
**Exam:** Start with Audit to find existing violations. Switch to Deny once you're confident.

### Initiatives (Policy Sets)
Group multiple policies into one assignment.

Example: "CIS Azure Foundations Benchmark" = 100+ policies bundled.

### Compliance Dashboard
- See % compliant resources per policy
- Drill down to non-compliant resources
- Track over time

---

## Resource Locks

Prevent accidental changes, applied **on top of** RBAC.

| Lock | Read | Modify | Delete |
|---|---|---|---|
| **ReadOnly** | ✓ | ✗ | ✗ |
| **CanNotDelete** | ✓ | ✓ | ✗ |

```
Inheritance: Lock on RG applies to all resources in it
Override: Must remove lock first (requires Write on lock object)
```

{: .tip }
**Exam:** Even an Owner cannot delete a resource with a CanNotDelete lock without removing it first.

---

## Activity Log

Every create/modify/delete operation on Azure resources is recorded here.

- **Retention:** 90 days (export to Log Analytics for longer)
- **Includes:** Who did it, what resource, when, result
- **Use:** Audit trail, troubleshoot unexpected changes

```
Example: "Who deleted the production VM?"
→ Azure Monitor → Activity Log → filter by resource + timeframe
```

---

## Microsoft Defender for Cloud

Security posture management + workload protection.

| Feature | Purpose |
|---|---|
| **Secure Score** | 0–100 rating of security posture |
| **Recommendations** | Specific remediation steps |
| **Regulatory Compliance** | Map to NIST, PCI-DSS, ISO 27001, etc. |
| **Defender Plans** | Threat detection per workload type |

### Defender Plans (paid add-ons)

| Plan | Protects |
|---|---|
| Defender for Servers | VMs — vulnerability assessment, JIT |
| Defender for SQL | SQL databases — threat detection |
| Defender for Storage | Storage accounts — malware, unusual access |
| Defender for Containers | AKS, ACR — image scanning, runtime protection |

---

## Update Management

Manage OS patches across Azure and on-prem VMs.

```
Flow:
  Assessment  →  Schedule  →  Deploy  →  Report
  (what's missing)  (maintenance window)  (install)  (compliance)
```

- Supports: Windows and Linux
- Integrates with: Azure Monitor, Activity Log
- Pre/post scripts for custom steps (e.g. drain load balancer before patching)

---

## Exam Checklist

- [ ] Explain the difference between Metrics and Logs in Azure Monitor
- [ ] Write a basic KQL query (filter, project, summarize)
- [ ] Describe the components of an alert rule
- [ ] Explain Audit vs Deny policy effects
- [ ] Explain resource locks and how they interact with RBAC
- [ ] Describe the Activity Log and its retention period
- [ ] Explain Secure Score in Defender for Cloud
- [ ] Describe Update Management and how patches are deployed
