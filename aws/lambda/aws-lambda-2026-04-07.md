# AWS Lambda
**Date:** Apr 7, 2026  
**Folder:** lambda  

---

### AWS Lambda Overview

- Serverless compute — runs code without managing servers
- Automatically scales, stateless execution per invocation
- Supports multiple programming languages
- Pay only for actual compute time used

### Event-Driven Patterns

- **S3 Integration**: file upload → S3 notification → Lambda → process/move to destination bucket
- **Kinesis**: IoT devices → Data Stream → Lambda (configurable batch size, default 100 records)
- Real-time event processing, workflow automation

### Lambda Layers

- ZIP file containing shared code, libraries, custom runtimes
- Multiple functions share same layer — reduces deployment package size
- Centralized dependency management across functions

### Key DEA Exam Points

- Lambda + S3 events: event-driven ETL trigger
- Lambda + Kinesis: stream processing with auto-scaling
- Lambda + DynamoDB Streams: real-time reaction to table changes
- Lambda + Glue: trigger ETL jobs from events
- Lambda transformations in Kinesis Firehose: on-the-fly data modification