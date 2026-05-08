# Other Storage Services
**Date:** Apr 10, 2026  
**Folder:** storage  

---

### Amazon EBS (Elastic Block Store)

- Durable block storage for EC2 — persistent, survives instance stop/termination
- One volume → one instance at a time; one instance can have multiple volumes
- Data replicated within AZ for hardware failure protection

### EBS Volume Types

- **GP2/GP3 (General Purpose SSD)**: balanced price/performance; GP3 has independent IOPS/throughput
- **IO1 (Provisioned IOPS SSD)**: consistent performance for IO-intensive, latency-sensitive workloads
- **ST1 (Throughput HDD)** and **SC1 (Cold HDD)**: lower cost, infrequent access
- IO2 Block Express: 99.999% durability

### EBS Snapshots

- Incremental — only changed blocks saved
- Stored in S3, replicated across AZs, compressed and encrypted
- Lifecycle management: automated retention/deletion, cross-region copy

### Amazon EFS (Elastic File System)

- Serverless, fully elastic — **supports multiple EC2 instances simultaneously** (key diff from EBS)
- NFSv4.1 protocol, multi-AZ replication, pay-as-you-use
- **Performance modes**: General Purpose (low latency) / Max IO (big data)
- **Throughput modes**: Bursting (credit system) / Provisioned (manual)
- **Storage classes**: Standard / Infrequent Access (IA) / One Zone IA

### AWS Backup Service

- Centralized backup across EC2, RDS, EFS, and more
- Cross-region and cross-account backup for disaster recovery
- IAM integration for access control

### AWS Backup VaultLock

- **Compliance mode**: policy cannot change or be deleted — not even root — strictest
- **Governance mode**: specified IAM roles can manage, still protects against deletion
- Critical for regulatory compliance (finance, healthcare)