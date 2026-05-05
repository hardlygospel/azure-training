# 4. Storage & Backup 💾

## Azure Storage Account

### What Is a Storage Account?
- **Container** for all Azure Storage services
- **Unique name** (globally unique)
- **Region** where data lives
- **Replication** strategy
- **Cost depends on:** Type, region, replication, operations

### Storage Account Name
- **3-24 characters** (lowercase + numbers)
- **Globally unique** (like a domain)
- **Affects URL:** mystorageacct.blob.core.windows.net

### Replication Strategies

| Strategy | Copies | Regions | Cost | SLA | Use Case |
|----------|--------|---------|------|-----|----------|
| **LRS** (Local) | 3 | 1 region, 1 zone | $ | 99.9% | Dev/test |
| **ZRS** (Zone) | 3 | 1 region, 3 zones | $$ | 99.95% | HA |
| **GRS** (Geo) | 6 | 2 regions | $$ | 99.99% | DR |
| **RA-GRS** | 6 | 2 regions (readable) | $$$ | 99.99% | Best HA |

---

## Blob Storage

### What Are Blobs?
- **Large files** (images, videos, documents, backups)
- **Object storage** (not file system)
- **Scalable** to petabytes
- **Cost-effective** for large data

### Access Tiers
| Tier | Cost/GB | Retrieval | Use |
|------|---------|-----------|-----|
| **Hot** | Most expensive | Instant | Frequent access |
| **Cool** | Moderate | ~30 min | Monthly access |
| **Archive** | Cheapest | ~15 hours | Yearly access |

### Blob Types
- **Block blobs:** Large files, text, images
- **Page blobs:** Random access (VM disks)
- **Append blobs:** Logs (append only)

### Blob Lifecycle Management
- **Automatically move** to cooler tiers
- **Example:** Move to Cool after 30 days, Archive after 90
- **Save costs** automatically

### Blob Snapshots
- **Point-in-time copy** of blob
- **Read-only**
- **Lower cost** than full backup

---

## File Shares (Azure Files)

### What Are File Shares?
- **Network file shares** (like SMB/NFS)
- **Mount from Windows/Linux/Mac**
- **100 TB per share**
- **Use case:** App data, shared storage

### SMB vs NFS
| | SMB | NFS |
|--|-----|-----|
| **OS** | Windows/Linux/Mac | Linux |
| **Speed** | Good | Better |
| **Standard** | Windows domains | POSIX |

### Snapshots
- **Share-level snapshots** (all files)
- **Point-in-time recovery**
- **Easy restore**

---

## Tables & Queues

### Table Storage
- **NoSQL** key-value store
- **Fast lookups**
- **Structured data** (user profiles, logs)
- **Lower cost** than databases

### Queue Storage
- **Message queue** (FIFO)
- **Async processing**
- **Decouple components**
- **Example:** Worker process picks messages

---

## Managed Disks

### What Are Managed Disks?
- **Storage for VMs**
- **Azure manages** underlying storage account
- **No storage account** management needed
- **Better reliability** (Microsoft manages)

### Disk Types
- **Premium SSD:** High performance, high cost
- **Standard SSD:** Good performance, moderate cost
- **Standard HDD:** Low performance, low cost

### Disk Snapshots
- **Copy of disk** at point in time
- **Create new disk** from snapshot
- **Backup mechanism**

### Image (Generalized)
- **Template** for VM creation
- **OS + installed software**
- **Faster VM deployment**

---

## Backup & Recovery

### Azure Backup

**What It Does:**
- **Automated backup** of VMs, SQL, file shares
- **Point-in-time recovery**
- **Off-site storage** (geo-redundant)
- **Compliance** (retention policies)

**Backup Types:**
| Type | What | Frequency | Cost |
|------|------|-----------|------|
| **Full** | Everything | Weekly | $ |
| **Incremental** | Changes only | Daily | $ |
| **Differential** | Changes since last full | Daily | $$ |

### Backup Vault (Recovery Services)
- **Central backup management**
- **Backup policies** (frequency, retention)
- **Encryption** of backups
- **Disaster recovery** (geo-redundant)

### Restore Options
- **Full VM restore:** Entire VM
- **File restore:** Individual files (attach as disk)
- **Database restore:** To point in time
- **Cross-region restore:** Recover in different region

### Backup SLA
- **Daily backup:** 24 hours old maximum
- **Retention:** 7 years typical
- **Recovery time:** Minutes to hours

---

## Azure Site Recovery

### What Is ASR?
- **Disaster recovery** orchestration
- **Replicate VMs** to secondary region/site
- **Automatic failover** on outage
- **Minimal data loss**

### How It Works
1. **Enable replication** on VM
2. **ASR replicates** continuously to secondary
3. **Outage happens** → automatic failover
4. **Run from secondary** region
5. **Failback** when primary recovers

### RPO vs RTO
- **RPO** (Recovery Point Objective): Max data loss (e.g., 5 mins)
- **RTO** (Recovery Time Objective): Max recovery time (e.g., 30 mins)

### Use Cases
- **Critical systems:** Need DR
- **Compliance:** Regulatory requirement
- **Risk management:** Business continuity

---

## Data Protection

### Encryption
- **At rest:** Default (TDE for SQL, etc.)
- **In transit:** HTTPS/TLS
- **Customer-managed keys:** Bring your own encryption key

### Soft Delete
- **Recover deleted blobs** within retention period
- **Default:** 7 days
- **Safety feature**

### Immutable Storage (WORM)
- **Write Once, Read Many**
- **Cannot modify** or delete
- **Compliance:** Regulatory requirements

### Access Control
- **Storage Account Key:** Full access (dangerous)
- **SAS Token:** Limited access (time-bound, scoped)
- **Managed Identity:** App without credentials
- **Firewall:** Network restrictions

---

## Azure Synapse Analytics (Data Warehouse)

### What Is It?
- **Data warehouse** (massive analytics)
- **SQL pools:** Execute queries
- **Spark pools:** Big data processing
- **Scale independently:** Storage separate from compute

### Use Cases
- **Business intelligence:** Dashboards, reports
- **Data science:** Analysis, modeling
- **Ad-hoc queries:** Explore data

---

## Cost Optimization

### Storage Tips
1. **Hot → Cool after 30 days** (lifecycle policy)
2. **Delete old snapshots** (cost adds up)
3. **Use GRS wisely** (2x cost of LRS)
4. **Monitor usage** (find unused storage)
5. **Archive old data** (cheapest tier)

### Data Transfer
- **Ingress:** Free
- **Egress:** Expensive
- **Use ExpressRoute** to reduce egress

---

## Exam Tips

- **Blob tiers:** Hot > Cool > Archive (cost inverse)
- **Lifecycle policy:** Move blobs automatically
- **Replication:** LRS (cheap), GRS (redundant), RA-GRS (readable)
- **Managed Disk:** Always prefer (Azure manages)
- **Backup Vault:** Centralized backup/recovery
- **ASR:** Disaster recovery (secondary region)
- **SAS Token:** Time-bound, scoped access (better than key)
- **Immutable storage:** Compliance/audit requirements
- **Snapshots:** Cheap point-in-time backups
