# AWS Athena Overview
**Date:** Mar 12, 2026
**Folder:** athena

---

## Overview

Amazon Athena is a serverless, interactive query service that analyzes data directly in S3 using standard SQL. Charges per query based on data scanned. Central to DEA-C01 data lake query patterns.

---

## Core Architecture

- **Engine**: Presto/Trino (distributed SQL)
- **Catalog**: AWS Glue Data Catalog as default metastore
- **Serverless**: no clusters, auto-scales
- **Pricing**: $5 per TB scanned (no charge for DDL, failed queries, metadata ops)

---

## Performance Optimization

- **Columnar formats**: Parquet/ORC — scan only needed columns, up to 87% less data
- **Partitioning**: Athena skips non-matching partitions; always filter on partition key
- **Partition projection**: define rules in table properties → no MSCK REPAIR TABLE needed
- **File size**: ideal 128MB–1GB; small files = overhead
- **Compression**: Snappy (splittable + Parquet) > GZIP (not splittable)
- **Bucketing**: pre-group by column within partitions → reduces JOIN shuffling

---

## Key Features

### CTAS (Create Table As Select)
- Create new table from query results in S3
- Convert CSV → Parquet in one step; can repartition simultaneously

### Athena Federated Query
- Lambda-based connectors for: RDS, DynamoDB, Redshift, CloudWatch Logs, on-premises
- Combine federated + S3 data in single SQL query
- Results spilled to S3 for large datasets

### Athena Workgroups
- Per-query or per-workgroup data scan limits (block or alert)
- Separate result locations, encryption enforcement, CloudWatch metrics
- Useful for cost chargeback and prod/dev isolation

### Athena for Apache Spark
- Interactive Spark notebooks — no cluster management
- Charged per DPU-hour

---

## Security

- Results encrypted: SSE-S3, SSE-KMS, or CSE-KMS
- Lake Formation: column-level and row-level security on Glue catalog tables
- Results cached 7 days; query history 45 days

---

## Common DEA Exam Scenarios

- **Query S3 logs without a DB**: Athena + Glue Crawler
- **Cost-efficient ad-hoc analytics**: Parquet + partitioning
- **Multi-team cost tracking**: Athena Workgroups per team
- **Query DynamoDB + S3 together**: Federated Query
- **Convert CSV to Parquet**: CTAS statement
- **Row-level security**: Lake Formation + Athena
- **Reduce KMS costs on results**: SSE-S3 or S3 Bucket Key