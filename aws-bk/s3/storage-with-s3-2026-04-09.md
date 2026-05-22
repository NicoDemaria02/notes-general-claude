# Storage with S3
**Date:** Apr 9, 2026  
**Folder:** s3  

---

### S3 Data Partitioning

- Partitioning involves setting up folder/directory structure in S3 buckets based on different attributes
  - Most commonly time-based (year/month/day folders)
  - Can also partition by region or other attributes depending on data access patterns
- Improves query performance by reducing amount of data that needs to be scanned
  - Benefits both Athena and Glue for data processing
  - Enables more efficient data retrieval by accessing only relevant partitions
- Requires metadata registration in data catalog
  - Use Glue crawlers to automatically create partition keys and store metadata
  - Folder structure must be registered with corresponding metadata
- Common implementation uses key-value method
  - Example: /year=2026/month=04/day=09/
  - Metadata stored and managed by Glue data catalog
- Partition strategy should align with typical data filtering and access patterns

### S3 Storage Classes and Lifecycle Management

- **Standard Storage Classes:**
  - S3 Standard: Default for frequently accessed data, low latency, general purpose use
  - S3 Intelligent Tiering: Automatically moves data between access tiers based on usage patterns
    - Frequent access tier initially
    - Moves to infrequent access after 30 consecutive days of no access
    - Moves to archive instant access after 90 days of no access
    - Optional asynchronous archive access available
  - S3 Express One Zone: High performance single AZ storage
    - Delivers single-digit millisecond access for most frequently accessed data
    - Up to 10x faster access speed, 50% lower request costs vs S3 Standard
    - Uses Amazon S3 Directory buckets supporting hundreds of thousands requests/second

- **Infrequent Access Classes:**
  - S3 Standard-IA: For less frequently accessed data requiring rapid access when needed
  - S3 One Zone-IA: Similar to Standard-IA but stored in single availability zone
    - Lower availability, suitable for recreatable data or secondary backups

- **Glacier Archive Classes:**
  - Glacier Instant Retrieval: Millisecond retrieval for archive data accessed ~once per quarter
  - Glacier Flexible Retrieval: 1 minute to 12 hours retrieval time, suitable for data accessed 1-2 times yearly
  - Glacier Deep Archive: Cheapest storage option, 12-hour retrieval time for long-term archival

### Lifecycle Rules Implementation

- Lifecycle rules automate transitions between storage classes and object deletion
- Two main action types:
  1. Transition actions: Move objects to different storage classes after specified time periods
  2. Expiration actions: Automatically delete objects after defined timeframes
- Configuration options include:
  - Scope filtering by prefix (folder paths), tags, or object size
  - Multiple transition stages (e.g., Standard → Intelligent Tiering → Glacier)
  - Automatic deletion after retention period
- Example: Immediate move to Intelligent Tiering → Glacier Instant Retrieval after 180 days → Deep Archive → delete after 720 days

### S3 Versioning

- Maintains multiple versions of objects as they change over time
- Benefits: protection against accidental deletion, disaster recovery, data integrity, regulatory compliance
- Each version gets unique identifier and cannot be changed once created
- Storage cost implications: complete new version saved (not incremental)
- Enable only for critical or sensitive datasets
- Lifecycle rules can manage retention of non-current versions separately

### Cross-Region Replication

- Copies and synchronizes data across multiple AWS regions
- Benefits: disaster recovery, reduced latency, increased availability
- Unidirectional replication (source to destination only)
- Deletions in source bucket don't replicate by default (safety feature)
- Requires versioning enabled in both source and destination buckets

### S3 Encryption

- **Encryption in Transit:** SSL/TLS to protect data traveling to/from S3

- **Encryption at Rest (Server-Side):**
  - All buckets have encryption at rest by default
  - SSE-S3 (S3 Managed Keys): Default, AWS handles all key management
  - SSE-KMS (AWS Key Management Service): More control, create and manage own encryption keys
  - SSE-KMS Dual Layer: Two layers of encryption using separate KMS keys
  - SSE-C (Customer Provided Keys): Full customer responsibility for key management

### Bucket Policies and Access Control

- **Bucket Policies:** JSON documents defining access rules at bucket level
  - Components: Version, Statement, Effect (Allow/Deny), Principal, Action, Resource, Condition

- **S3 Access Points:**
  - Customizable entry points with individual policies
  - Each has unique DNS name (Internet or VPC origin)
  - Simplified access management for multiple teams/use cases

### Advanced S3 Features

- **Object Lambda:** Transform data during retrieval using Lambda functions
  - Use cases: PII redaction, format conversion, data augmentation
  - Eliminates need for duplicate data storage

- **Event Notifications:** Trigger actions based on S3 bucket events
  - Supported events: object creation, deletion, restoration, lifecycle transitions
  - Destinations: SNS, SQS, Lambda functions, EventBridge

### Data Architecture Concepts

- **Data Mesh:** Decentralized data ownership architecture
  - Core principles: domain-oriented ownership, data as products, self-service infrastructure, federated governance
  - AWS implementation: S3, Glue, Redshift, Lake Formation, Athena, API Gateway

- **AWS Data Exchange:** Centralized catalog for third-party data discovery and subscription
  - Use cases: Financial data, healthcare research, geospatial data, retail analytics
  - Integration with S3, Lake Formation, and AWS Marketplace