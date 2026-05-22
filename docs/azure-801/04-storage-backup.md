
# Storage & Backup

[![AZ-801](https://img.shields.io/badge/AZ--801-Domain%204-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)]()
[![Weight](https://img.shields.io/badge/Exam%20Weight-15--20%25-f59e0b?style=flat-square)]()

---

## Storage Accounts

A storage account is the **namespace** for Azure Storage services. One account can hold blobs, files, queues, and tables.

### Replication Options

```
LRS   Locally Redundant    3 copies, 1 zone, 1 region      Cheapest, no HA
ZRS   Zone Redundant       3 copies, 3 zones, 1 region     Good HA
GRS   Geo Redundant        6 copies, 2 regions              DR capable
GZRS  Geo+Zone Redundant  6 copies, 3+3 zones, 2 regions  Best protection
RA-GRS / RA-GZRS          Same as above + readable failover
```

{: .tip }
**Exam:** GRS replicates to a paired region but the secondary is **read-only by default**. RA-GRS makes it readable (for extra cost).

### Storage Account Types

| Type | Supports | Use |
|---|---|---|
| **Standard General Purpose v2** | Blob, Files, Queue, Table | Most workloads |
| **Premium Block Blob** | Blob only | Low-latency blob access |
| **Premium File Shares** | Files only | High-perf file shares |
| **Premium Page Blob** | Page blobs (VM disks) | Unmanaged disks |

---

## Blob Storage

Best for: large objects, images, videos, backups, logs, static website files.

### Access Tiers

| Tier | Storage cost | Retrieval | Min storage duration |
|---|---|---|---|
| **Hot** | Highest | Immediate | None |
| **Cool** | Medium | Immediate | 30 days |
| **Cold** | Low | Immediate | 90 days |
| **Archive** | Lowest | 1–15 hours (rehydration) | 180 days |

**Lifecycle Management Policy** — automatically move blobs between tiers:
```
After 30 days → move to Cool
After 90 days → move to Cold
After 365 days → move to Archive
After 730 days → delete
```

### Blob Access Control

| Method | Scope | Use |
|---|---|---|
| **Access Key** | Full account | Emergency / admin only |
| **SAS Token** | Container or blob, time-limited | Temporary access for apps |
| **AAD + RBAC** | Fine-grained | Recommended for managed identities |
| **Anonymous public access** | Container/blob | Public content only |

{: .tip }
**Exam:** SAS tokens are preferred over access keys for third-party access. Keys = full access to the account.

### Soft Delete
Protects against accidental deletion — deleted blobs retained for 1–365 days. Enable on every storage account.

### Immutable Storage (WORM)
Write Once, Read Many — blobs cannot be modified or deleted during retention period.
- **Time-based retention** — set period (e.g. 7 years)
- **Legal hold** — indefinite until hold is released
- Required for: financial records, healthcare (HIPAA), legal compliance

---

## Azure Files

Network file shares accessible via **SMB** (Windows/Mac/Linux) or **NFS** (Linux).

```
On-premises or Azure VM
      ↓ Mount via SMB/NFS
  \\storageaccount.file.core.windows.net\sharename
```

| Feature | Details |
|---|---|
| **Max share size** | 100 TB |
| **Max file size** | 4 TB |
| **Snapshots** | Point-in-time share snapshots |
| **Azure File Sync** | Sync on-prem file server with Azure Files |

### Azure File Sync
Cache frequently used files on-premises while tiering older files to Azure.

```
On-prem file server ←──[File Sync]──→ Azure Files
Local cache of hot files        Full copy in cloud
```

---

## Azure Backup

### Recovery Services Vault
Central hub for backup. Configure policies, store backups, manage recovery.

### What Can Be Backed Up

| Resource | Agent required | Recovery types |
|---|---|---|
| **Azure VMs** | None (snapshot-based) | Full VM, file/folder, disk |
| **SQL in Azure VM** | SQL Backup extension | Full, differential, log |
| **Azure Files** | None | Share snapshots |
| **On-prem (MARS)** | MARS agent | File/folder, system state |
| **On-prem (DPM/MABS)** | DPM/MABS agent | Full workloads |

### Backup Policy
Define: **frequency** (daily/weekly) and **retention** (30 days, 1 year, 7 years).

```
Example policy:
  Daily backup → retain 30 days
  Weekly backup → retain 12 weeks
  Monthly backup → retain 12 months
  Yearly backup → retain 5 years
```

### Restore Options

| Option | Description |
|---|---|
| **Create new VM** | Full VM restore to new VM |
| **Replace existing** | Overwrite existing VM's disks |
| **Restore disks** | Create disk, attach manually |
| **File Recovery** | Mount backup as disk, copy individual files |

{: .tip }
**Exam:** File Recovery is useful when you only need to restore a single file, not the whole VM.

---

## Azure Site Recovery (ASR)

Disaster recovery — **replicates VMs** to a secondary region continuously.

```
Primary region (running VMs)
         ↓ continuous replication
Secondary region (standby copies)

On disaster: Failover → run from secondary
After recovery: Failback → return to primary
```

| Concept | Value |
|---|---|
| **RPO** | ~30 seconds for Azure-to-Azure replication |
| **RTO** | Minutes (automated failover) |
| **Cost** | Per VM per month (~$25 + target infrastructure) |

### Recovery Plans
Script the failover sequence — VMs start in the right order, with optional pre/post scripts.

---

## Managed Disks vs Unmanaged

| | Managed | Unmanaged |
|---|---|---|
| Storage account | Azure manages | You manage |
| Limits | No storage account limits | 20,000 IOPS cap per account |
| Snapshots | Built-in | Manual |
| Recommendation | **Always use** | Legacy only |

### Disk Snapshots
Point-in-time copy of a managed disk. Incremental — only changed blocks stored.

```
Snapshot → Create new disk from snapshot → Attach to VM
```

---

## Exam Checklist

- [ ] Name the 4 replication options (LRS, ZRS, GRS, RA-GRS) and when to use each
- [ ] Explain blob access tiers and lifecycle policies
- [ ] Compare access key vs SAS token vs AAD RBAC for blob access
- [ ] Explain soft delete and immutable storage
- [ ] Describe Azure Backup and Recovery Services Vault
- [ ] Explain the difference between VM restore options (full VM vs file recovery)
- [ ] Explain ASR and the failover/failback process
- [ ] Explain RPO and RTO in a disaster recovery context
