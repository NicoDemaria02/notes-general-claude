# Data Streaming
**Date:** Apr 8, 2026
**Folder:** streaming

---

### Replayability

- Ability to reprocess/re-ingest data that has already been handled
- Core importance: error handling, data consistency, schema change adaptation, testing
- Implementation: idempotent operations, logging/auditing, checkpointing, backfilling

### Amazon Kinesis Overview

1. **Kinesis Data Streams** — ingest streaming data at large volumes with dynamic scaling
2. **Kinesis Firehose** — fully managed delivery to S3, Redshift, OpenSearch, Splunk
3. **Managed Apache Flink** — real-time analysis using SQL, Python, Scala, Java

### Kinesis Data Streams

- **Producers**: AWS SDK, Kinesis Producer Library, Kinesis Agent
- **Data Records**: Up to 1MB, contains data value + partition key
- **Shards**: 1MB/s or 1,000 records/s input; 2MB/s output per shard
- Data retention: 24 hours (default) to 365 days — immutable once written
- **Provisioned mode**: Manual shard count, hourly rate per shard
- **On-demand mode**: Auto-scaling, pay for actual throughput

### Enhanced Fan Out

- Each consumer gets dedicated 2MB/s via HTTP/2 (vs shared 2MB/s)
- Supports up to 20 consumers per shard
- Latency: ~70ms vs ~200ms standard; ideal for 5+ consumers

### Kinesis Data Firehose

- Near real-time (buffered — not true real-time)
- No custom producer/consumer code, automatic scaling
- Destinations: S3, Redshift (via COPY), OpenSearch, Splunk, MongoDB
- Built-in Lambda transformations, Parquet/ORC conversion, encryption
- Fallback S3 bucket for failed deliveries

### Managed Service for Apache Flink

- Stateful computations, checkpointing, anomaly detection
- Sources: Kinesis Data Streams, MSK, S3
- Pricing: 1 KPU = 1 vCPU + 4GB memory; +2 KPUs for Flink Studio

### Amazon MSK (Managed Streaming for Kafka)

- **vs Kinesis**: Messages up to 10MB (vs 1MB), topics/partitions, more config control
- **Security**: TLS, mutual TLS + Kafka ACLs, username/password, or IAM
- **MSK Connect**: managed Kafka Connect for external integrations
- **MSK Serverless**: auto resource provisioning and scaling

### MSK vs Kinesis

- **Choose MSK**: Messages >1MB, need granular config, complex scenarios
- **Choose Kinesis**: Simpler setup, messages ≤1MB, managed AWS experience