# AWS Compute Services Deep Dive: EC2, Batch, SAM, and Auto Scaling Overview
**Date:** May 1, 2026  
**Folder:** compute  

---

### AWS EC2 Fundamentals

- Foundational compute service providing secure, resizable capacity in cloud
- Virtual server instances with on-demand scalable compute
- Full control over configuration: OS, networking, storage, security
- High availability across multiple availability zones
- Auto scaling adjusts instances based on workload changes
- Integrates with IAM, S3, CloudWatch and other services

### EC2 Instance Types

- **General Purpose**: Balanced compute, memory, networking — web servers, code repositories
- **Compute Optimized**: High-performing processors — batch processing, media transcoding, HPC, gaming servers, ML inference
- **Memory Optimized**: Fast performance for in-memory data processing
- **Accelerated Computing**: Hardware acceleration — floating point, graphics processing, data pattern matching
- **Storage Optimized**: High sequential read/write access to large datasets
- **HPC Optimized**: High performance computing — big data processing, deep learning workloads

### AWS Batch Overview

- Service for running batch jobs based on Docker images
- Handles operational aspects automatically
- Automatically scales resources based on demand
- Can schedule jobs and integrate with AWS Step Functions
- Supports both EC2/Spot instances and Fargate for serverless
- Pricing based on compute resources consumed (instance hours)

### Batch vs Other Services

- **Lambda**: Lightweight, event-driven tasks for real-time responses
- **Glue**: Managed ETL service for data integration using Spark
- **Batch**: General purpose, compute-intensive batch computing jobs

### AWS SAM (Serverless Application Model)

- Framework for building/managing serverless applications
- Simplifies deployment for Lambda, API Gateway, DynamoDB
- Uses SAM templates (YAML configuration files)
- Local testing capabilities that mimic AWS environment
- IDE integration with VS Code, PyCharm, IntelliJ
- Key commands:
  1. `sam build` — Processes template, builds source code
  2. `sam package` — Packages code/dependencies, uploads to S3
  3. `sam deploy` — Creates CloudFormation stack from template

### Application Auto Scaling

- Automatically scales resources for various AWS services:
  - Aurora, DynamoDB, SageMaker, Lambda provisioned concurrency
  - Managed Kafka, Neptune clusters, EMR clusters
- **Target Tracking Policies**: Maintains metric target (e.g., 50% CPU) — works like a thermostat
  - Uses AWS or custom CloudWatch metrics
- **Scheduled Scaling**: Proactive scaling for predictable patterns
  - Set capacity changes for specific times/days
  - Optimizes cost during low traffic periods, ensures performance during peaks