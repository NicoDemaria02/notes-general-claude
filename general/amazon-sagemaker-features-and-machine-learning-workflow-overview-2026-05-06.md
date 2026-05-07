# Amazon SageMaker features and machine learning workflow overview
**Date:** May 6, 2026
**Folder:** general

---

### Amazon SageMaker Overview

- Enables developers and data scientists to build, train, and deploy machine learning models efficiently
- Abstracts complex infrastructure management so teams can focus on model building rather than underlying architecture
- Supports multiple ML frameworks including TensorFlow and PyTorch
- Provides direct integration with Jupyter notebooks for interactive development
- Automatically manages scaling resources up and down based on demand
- Handles large data volumes while speeding up training processes
- Offers reliable model deployment with high availability through AWS infrastructure

### SageMaker Studio IDE

- Web-based visual interface designed for ML development workflow
- Enables collaboration between team members with Git integration for version control
- Manages code, notebooks, and projects more efficiently
- Key components include:
  1. **Notebooks** - Pre-configured Jupyter notebooks for interactive model development and data visualization
  2. **Experiments** - Container-like organization system to track and compare model iterations
  3. **Debugger** - Analysis tools to debug model training and improve performance
  4. **Autopilot** - Automated model creation with options for manual control and modification

### Access Management and Security

- Multiple policy attachment options for granular access control
- **Direct user policies:**
  - SageMaker Full Access policy can be attached to users or roles
  - Includes permissions for related services like S3 buckets and ECR
- **Service-specific policies:**
  - SageMaker Read Only access
  - SageMaker Notebooks Service Role (service-only attachment)
- **Execution roles:**
  - Default execution role includes permissions for cross-service actions
  - S3 bucket access limited to buckets with "SageMaker" or "AWS Glue" in the name
  - Additional policies can be attached for broader bucket access
- **Resource-based policies:**
  - Attach directly to SageMaker resources (notebook instances, endpoints, models)
  - Specify user access and permitted actions per resource
- **Tag-based access control:**
  - Uses key-value pairs for conditional access
  - Example: Department tags can restrict access to marketing team resources only
  - Supports project names and development stages (dev/prod)
- Integrates with VPC for network access control and KMS for encryption key management

### Feature Store

- Centralized repository for storing and managing ML model input variables (features)
- **Feature definition:** Input variables used for predictions (e.g., daily temperature, user access patterns)
- Eliminates repetitive preprocessing work across ML projects
- Ensures consistency across different machine learning initiatives
- **Storage options:**
  1. **Online store** - Optimized for real-time applications with low latency access (recommendation systems, dynamic pricing)
  2. **Offline store** - Used for model training and batch inference, stored in S3 buckets with append-only format, more cost-effective
- **Feature groups:** Structured collections of related features, similar to database tables where each feature is a column and each observation is a row
- **Data ingestion sources:** EMR, Glue, Kinesis, Lambda, and others
- **Ingestion methods:** Streaming for real-time updates or batch processing for offline storage

### ML Lineage Tracking

- Provides governance, auditing, and visibility into model lifecycle
- Tracks workflow components from development through deployment
- **Experiment entities:**
  1. **Trial components** - Individual workflow steps (data processing, model training, evaluation)
  2. **Trials** - Specific model tests or configurations, composed of multiple trial components
  3. **Experiments** - Containers organizing trials aimed at solving specific problems
- **Lineage entities:**
  1. **Context** - Logical groupings of artifacts and actions
  2. **Actions** - Operations that manipulate or transform artifacts
  3. **Artifacts** - Data objects generated during ML lifecycle (datasets, model outputs, logs)
  4. **Associations** - Relationships between different entities
- SageMaker automatically tracks entities during processing and training jobs
- Provides visual representation of entity connections for better model understanding

### Data Wrangler

- Visual interface for ML-specific data preparation and preprocessing
- Simplifies data cleaning, organization, and transformation processes
- **Data import sources:** S3, Redshift, SageMaker Feature Store
- **Transformation capabilities:**
  - Handle missing values and convert data types
  - ML-specific operations like one-hot encoding and normalization
  - Broad library of built-in transformations
- **Visualization tools:**
  - Data distribution analysis and relationship identification
  - Histograms, line plots, and bar charts
  - Helps inform feature selection and engineering decisions
- **Feature engineering:** Create and modify features specifically for model training
- **Export options:** Integration with SageMaker for model training or other AWS services
- **Quick Model feature:**
  - Visualizes feature importance scores
  - Estimates predictive power of each feature on target variable
  - Automatically determines problem type (regression vs classification)
  - Provides automated data splitting and simple model training for quick evaluation
