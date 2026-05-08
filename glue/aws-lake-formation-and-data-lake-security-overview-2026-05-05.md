# AWS Lake Formation and Data Lake Security Overview
**Date:** May 5, 2026
**Folder:** glue

---

### AWS Lake Formation Overview

- Comprehensive data lake management service built on top of AWS Glue
- Manages all aspects of data lake lifecycle from collection to analytics
- Fine-grained access control integrated with IAM
- Cross-account data sharing via AWS Resource Access Manager (RAM)

### Security and Permission Management

- Centralized access control — single location for defining security policies
- Controls access at **database, table, row, and cell levels**
- **Row-level security**: restrict rows by criteria (e.g., department)
- **Column-level security**: restrict access to sensitive/PII columns
- **Cell-level security**: combination of row + column restrictions

### Tag-Based Access Control (TBAC)

- LF tags for attribute-based access control
- Define permissions based on tag attributes rather than individual resources
- Scalable for large numbers of tables and users

### Analytics Integrations

- **Athena**: serverless queries using catalog managed by Lake Formation
- **Redshift**: query S3 directly via Data Catalog with LF permissions
- **SageMaker**: ML with Lake Formation managed data
- **Glue ETL**: respects Lake Formation permissions for read/write

### Amazon OpenSearch Service

- Fully managed search engine (formerly Elasticsearch)
- Document-based with index structure; built-in dashboards
- **Storage tiers**: Hot (default) / Ultra Warm (S3 + cache) / Cold (S3 archival)
- Cross-cluster replication, index state management, serverless option

### Amazon QuickSight

- Serverless BI — SPICE engine (in-memory columnar, 10GB/user)
- Sources: S3, Redshift, Aurora, Athena, OpenSearch, ODBC/JDBC
- Row-level and column-level security
- Standard: $9/user/month | Enterprise: advanced ML insights, hourly refresh