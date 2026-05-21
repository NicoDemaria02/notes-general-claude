# Amazon SageMaker features and machine learning workflow overview
**Date:** May 6, 2026
**Folder:** general

---

### Amazon SageMaker Overview

- Build, train, and deploy ML models — abstracts infrastructure management
- Supports TensorFlow, PyTorch; integrates with Jupyter notebooks
- Automatic scaling, handles large data volumes

### SageMaker Studio IDE

- Web-based visual interface with Git integration
- **Notebooks**: pre-configured Jupyter for interactive development
- **Experiments**: track and compare model iterations
- **Debugger**: analyze and improve model training
- **Autopilot**: automated model creation with manual control options

### Feature Store

- Centralized repository for ML input variables (features)
- **Online store**: low latency, real-time (recommendation systems, dynamic pricing)
- **Offline store**: S3-backed, append-only, for training and batch inference
- Feature groups: structured collections, like database tables
- Ingestion: streaming (real-time) or batch

### ML Lineage Tracking

- Governance, auditing, visibility into model lifecycle
- **Trial components** → **Trials** → **Experiments**
- **Context**, **Actions**, **Artifacts**, **Associations** (lineage entities)
- Automatic tracking during processing and training jobs

### Data Wrangler

- Visual interface for ML data preparation and preprocessing
- Sources: S3, Redshift, SageMaker Feature Store
- 250+ transformations: missing values, type conversion, one-hot encoding, normalization
- **Quick Model**: estimates feature importance and predictive power automatically

### Access Management

- SageMaker Full Access, Read Only, Notebooks Service Role
- Execution roles: default includes S3 access for buckets with 'SageMaker'/'AWS Glue' in name
- Tag-based access control for department/project/environment isolation
- VPC integration and KMS encryption support