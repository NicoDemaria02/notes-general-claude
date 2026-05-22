# AWS RDS Database Services and Best Practices Overview
**Date:** May 1, 2026  
**Folder:** rds  

---

### AWS RDS Overview

- RDS = Relational Database Service — fully managed relational database service
- Eliminates traditional database setup complexity
- AWS manages all underlying infrastructure, updates, backups, and maintenance
- Supports MySQL, PostgreSQL, and other common database engines

### ACID Compliance

- **Atomicity**: All-or-nothing transactions
- **Consistency**: Transactions follow database constraints
- **Isolation**: Changes invisible to other transactions until completion
- **Durability**: Data persists even after system failures

### Performance Best Practices

- Monitor with CloudWatch: CPU, storage, replication metrics
- Schedule backups during low I/O periods
- Set DNS cache TTL under 30 seconds (prevents connection issues after failover)
- RDS Performance Insights: dashboard for visualizing database load

### Amazon Aurora

- Up to 5x better performance than MySQL, 3x better than PostgreSQL
- Automatic storage scaling from 10GB to 128TB
- **Aurora Serverless**: Dynamic compute, pay-as-you-go, Aurora Capacity Units (ACUs)

### Amazon DocumentDB
- NoSQL compatible with MongoDB, JSON documents
- Six copies across three AZs, continuous backup to S3

### Amazon Neptune
- Graph database — fraud detection, recommendation engines, social networks
- Property graph (Gremlin) and RDF (SPARQL) models
- Billions of relationships at 8ms latency

### Amazon Keyspaces
- Managed Apache Cassandra compatible NoSQL
- On-demand or provisioned capacity modes

### Amazon MemoryDB for Redis
- In-memory database with multi-AZ durability
- High-performance caching, real-time apps, session management

### Amazon Timestream
- Serverless time series database
- Use cases: IoT, application logs, financial market data
- Integration: Lambda, Kinesis Data Streams, Apache Flink, Grafana