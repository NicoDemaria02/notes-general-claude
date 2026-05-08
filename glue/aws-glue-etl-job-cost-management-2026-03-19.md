# AWS Glue: ETL, Job Types & Cost Management
**Date:** Mar 19, 2026
**Folder:** glue

---

## Overview

AWS Glue is a fully managed serverless ETL service. It handles data discovery, cataloging, transformation, and orchestration across the AWS data ecosystem. Central to DEA-C01 data pipeline and data lake topics.

---

## Core Components

| Component | Purpose |
|---|---|
| **Glue Data Catalog** | Central metadata repository — databases, tables, schemas, partitions |
| **Glue Crawlers** | Auto-discover data in S3, RDS, DynamoDB and populate the catalog |
| **Glue ETL Jobs** | Apache Spark / Python Shell jobs for data transformation |
| **Glue Studio** | Visual drag-and-drop ETL job builder |
| **Glue DataBrew** | No-code visual data preparation and profiling |
| **Glue Workflows** | Orchestrate multi-step ETL pipelines |
| **Glue Job Bookmarks** | Track processed data for incremental ETL |

---

## Glue ETL Jobs

### Job Types
| Type | Runtime | Use Case |
|---|---|---|
| **Spark** | Apache Spark | Large-scale distributed transformations |
| **Spark Streaming** | Spark Structured Streaming | Real-time from Kinesis/MSK |
| **Python Shell** | Python 3 | Lightweight scripts, small datasets |
| **Ray** | Ray framework | ML workloads, Python-native parallelism |

### DPU (Data Processing Units)
- 1 DPU = 4 vCPUs + 16 GB memory; billed per second, min 1 minute
- **G.1X**: 1 DPU, memory-optimized | **G.2X**: 2 DPU, heavy transforms | **G.025X**: 0.25 DPU, cost-efficient
- Auto Scaling: `--enable-auto-scaling` shrinks cluster during idle stages

### DynamicFrame
- Glue's extension of Spark DataFrame — handles schema inconsistencies
- `ResolveChoice`: handle ambiguous types (cast, project, make_struct)
- `ApplyMapping`: rename, cast, map columns in one step
- `dyf.toDF()`: convert to standard Spark DataFrame

---

## Glue Job Bookmarks

- Tracks processed data — prevents reprocessing old S3 objects or JDBC rows
- Modes: **ENABLED**, **DISABLED**, **PAUSE**
- Reset to reprocess all data from scratch

---

## Glue Schema Registry

- Schema management for streaming data: Avro, JSON Schema, Protobuf
- Integrates with Kinesis Data Streams, MSK, Lambda
- **Compatibility modes**: BACKWARD, FORWARD, FULL, NONE

---

## Cost Optimization

1. Right-size DPUs — start small, use CloudWatch to tune
2. Auto Scaling — scale down during idle stages
3. G.025X workers for small jobs
4. Job bookmarks — process only new data
5. Parquet output — reduces downstream Athena/Redshift Spectrum costs
6. Crawl on-demand/daily instead of hourly
7. `push_down_predicate` in DynamicFrame to filter at source

---

## Common DEA Exam Scenarios

- **Auto-discover schema**: Glue Crawler → Catalog → Athena
- **CSV to Parquet**: Glue Spark job with ApplyMapping
- **Incremental ETL from RDS**: Glue job with bookmarks
- **No-code prep**: Glue DataBrew
- **Schema validation for Kinesis**: Schema Registry with Avro
- **Mixed-type column**: DynamicFrame ResolveChoice
- **ETL inside VPC**: Glue JDBC connection with VPC config