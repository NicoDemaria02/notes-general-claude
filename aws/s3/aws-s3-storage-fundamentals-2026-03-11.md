# AWS S3 Storage Fundamentals
**Date:** Mar 11, 2026
**Folder:** s3

---

## Overview

Amazon S3 (Simple Storage Service) is AWS's core object storage service — infinitely scalable, highly durable, and the backbone of virtually every data engineering pipeline on AWS. For the DEA-C01 exam, S3 is tested extensively across all four domains.

---

## Core Concepts

### Object Storage Model
- Objects = data + metadata + unique key (path-like string)
- Buckets are global namespace containers — names must be globally unique across all AWS accounts
- Objects can be up to **5 TB**; single PUT limit is **5 GB** (use Multipart Upload for >100 MB)
- No actual folder hierarchy — prefixes simulate directories (e.g., `data/raw/2026/file.csv`)

### Bucket Configuration
- Buckets are **regional** — data stays in the region unless explicitly replicated
- Default: private; no public access unless explicitly enabled
- **Block Public Access** settings operate at account or bucket level — critical for compliance

---

## Storage Classes

| Class | Use Case | Retrieval | Durability |
|---|---|---|---|
| **S3 Standard** | Frequently accessed data | Milliseconds | 99.999999999% (11 9s) |
| **S3 Intelligent-Tiering** | Unknown/changing access patterns | Milliseconds | 11 9s |
| **S3 Standard-IA** | Infrequent access, rapid retrieval | Milliseconds | 11 9s |
| **S3 One Zone-IA** | Infrequent, non-critical | Milliseconds | 99.999999999% (single AZ) |
| **S3 Glacier Instant Retrieval** | Archive, quarterly access | Milliseconds | 11 9s |
| **S3 Glacier Flexible Retrieval** | Archive, hours acceptable | Minutes to hours | 11 9s |
| **S3 Glacier Deep Archive** | Long-term archive (7–10 years) | Up to 12 hours | 11 9s |

**Intelligent-Tiering details:**
- Monitors access, automatically moves objects between tiers
- No retrieval fees, small monthly monitoring fee per object
- Archive tiers available: Archive Access (90 days), Deep Archive Access (180 days)

---

## S3 Lifecycle Policies

- **Transition actions**: Move objects to cheaper class after N days
- **Expiration actions**: Delete objects or incomplete multipart uploads
- Common pattern: Standard → Standard-IA (30 days) → Glacier (90 days) → Expire (365 days)
- Minimum storage durations: Standard-IA/One Zone-IA = 30 days; Glacier Instant = 90 days; Deep Archive = 180 days

---

## S3 Security

### Bucket Policies
- JSON-based resource policies attached to the bucket
- Can grant/deny cross-account access

### S3 Access Points
- Named network endpoints with individual policies
- Ideal for data lake architectures with multiple teams

### Pre-signed URLs
- Temporary access URL — expiration configurable (max 7 days with IAM role)

### S3 Encryption

| Method | Who manages keys | Description |
|---|---|---|
| **SSE-S3** | AWS | AES-256, automatic |
| **SSE-KMS** | AWS KMS | Customer manages via CMKs; CloudTrail audit |
| **SSE-C** | Customer | Customer provides key per request |
| **Client-side** | Customer | Encrypted before upload |

- **Bucket key**: Reduces KMS API calls → significant cost savings at scale

---

## S3 Performance

- **Multipart Upload**: recommended >100 MB, required >5 GB — parallel parts
- **Transfer Acceleration**: routes via CloudFront edge locations
- **Request rate**: 3,500 PUT and 5,500 GET per second per prefix
- **S3 Select**: server-side SQL filtering on CSV/JSON/Parquet — reduces data transfer

---

## S3 Versioning & Replication

- Versioning: delete creates a delete marker; MFA Delete for permanent removal
- **CRR** (Cross-Region): disaster recovery, compliance, latency
- **SRR** (Same-Region): log aggregation, data sovereignty
- Both require versioning enabled; existing objects: use S3 Batch Replication

---

## S3 Object Lock

- **WORM** model — prevents deletion/overwrite for retention period
- **Compliance mode**: no override, even root — strictest
- **Governance mode**: IAM users with special permission can override
- **Legal Hold**: indefinite protection, independent toggle

---

## S3 in Data Engineering Pipelines

- Central storage layer: raw / processed / curated zones
- Integrates with: Glue (catalog + ETL), Athena (query), EMR (processing), Redshift Spectrum
- Use **Parquet/ORC** for analytics — columnar, compressed, predicate pushdown
- **S3 events → EventBridge → Lambda/Glue**: event-driven pipeline pattern

---

## Key Exam Scenarios

- **CRR for DR**: versioning + CRR, can replicate to different account
- **Cost optimization**: Lifecycle → Glacier Deep Archive
- **Secure sharing**: Pre-signed URLs
- **WORM compliance**: Object Lock (Compliance mode)
- **Reduce KMS costs**: S3 Bucket Key
- **Multi-team access**: S3 Access Points with per-team policies