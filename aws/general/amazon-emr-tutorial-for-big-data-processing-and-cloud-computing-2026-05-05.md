# Amazon EMR tutorial for big data processing and cloud computing
**Date:** May 5, 2026
**Folder:** general

---

### Amazon EMR Overview

- Elastic MapReduce: managed cluster platform for big data frameworks
- Primary use: data processing and machine learning model training
- Integrates with AWS services (S3, EC2, VPC)
- On-demand scaling eliminates need for 24/7 Hadoop clusters
- Uses YARN for cluster resource management

### EMR Architecture

- **Primary node**: coordinates data/task distribution, tracks status, monitors health
- **Core nodes**: run tasks and store data in HDFS (ephemeral storage)
- **Task nodes** (optional): run tasks but don't store HDFS data

### Key Integrations

- **S3 via EMRFS**: decouples storage from compute, data persists beyond cluster
- **EC2**: m5 (general batch), c5 (ML), x1 (memory intensive), fleet mixing on-demand/spot/reserved
- **Step Functions**: job orchestration

### Storage Options

- **HDFS**: local disk, high-speed but temporary
- **EMRFS**: HDFS over S3, persistent and cost-effective
- **EBS volumes**: additional capacity, deleted with cluster termination

### Scaling and Deployment

- Manual scaling, managed scaling (automatic), custom CloudWatch-based policies
- **EMR on EKS**: container-based via Kubernetes
- **EMR Serverless**: fully abstracted, automatic scaling