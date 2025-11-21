---
title: "Week 7 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Goals:

*   Complete Module 06
*   Do Lab19 & Lab53

### Tasks for this week:
| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|--------------------|
| 2   |  - Learn Module 06 - 01: Database Concepts review   | 20/10/2025 | 20/10/2025      |   [Module 06 - 01](https://www.youtube.com/watch?v=OOD2RwWuLRw&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=217)                |
| 3   |    - Learn Module 06 - 02: Amazon RDS & Amazon Aurora   | 21/10/2025 | 21/10/2025      |   [Module 06 - 02](https://www.youtube.com/watch?v=qbrobQZrokY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=218)                 |
| 4   |    - Learn Module 06 - 03: Redshift - ElastiCache  | 22/10/2025 | 22/10/2025      |  [Module 06 - 03](https://www.youtube.com/watch?v=UvdiRW34aNI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=219)                 |
| 5   |  - Do Lab19: VPC Peering   | 23/10/2025 | 23/10/2025      |  [Lab19](https://000019.awsstudygroup.com/vi/1-introduce/)               |
| 6   |  - Do Lab57: Getting Started with Amazon S3   | 24/10/2025 | 24/10/2025      |   [Lab57](https://000057.awsstudygroup.com/vi/1-introduce/)                |

### Week 7 Achievements:

*   Module 06 - 01: Database Concepts review
    *   Reviewed concepts in databases
        *   PK, FK, Database Log, etc.
        *   Became familiar with new concepts such as Index, Partitions, Execution Plan - Query Plan, Buffers.
    *   Initial understanding of Online Transaction Processing (OLTP) and Online Analytical Processing (OLAP)
        *   OLTP: focuses on fast processing, the database is frequently read from and written to, and system logic ensures data integrity.
        *   OLAP: focuses on response time for complex queries, applied to large volumes of data, and when combined with a data warehouse, can provide analysts with the ability to use custom reporting tools to turn data into information.

*   Module 06 - 02: Amazon RDS & Amazon Aurora
    *   Learned about Amazon RDS
        *   Managed by AWS
        *   Has features such as:
            *   Automated backups
            *   Creating Read Replicas to serve Read Workloads (e.g., Reporting)
            *   A Read Replica can be promoted to become a Primary Node
            *   Data encryption at rest and in transit
            *   Storage Auto Scaling
            *   Scaling (changing instance size)
        *   Can run with an automatic failover mechanism, also known as Multi-AZ
        *   Used for OLTP applications
    *   Learned about Amazon Aurora
        *   A database optimized at the underlying storage infrastructure for high parallel read and write performance
        *   Has features such as:
            *   Backtrack - Restore a DB to a previous point in time
            *   Clone - Create a copy
            *   Global Database
            *   Multi-Master
        *   Aurora classifies and groups related data (Clustering) across multiple AZs

*   Module 06 - 03: Redshift - ElastiCache
    *   Learned about the Redshift data warehouse service
        *   Core is PostgreSQL, optimized for OLAP
        *   Uses a Massively Parallel Processing (MPP) Database architecture
        *   Data is partitioned and stored on Compute nodes
        *   The Leader node coordinates and aggregates queries
        *   Stores data in columnar storage format
        *   Uses SQL and JDBC, ODBC drivers
        *   Supports cost-optimization features:
            *   Transient clusters
            *   Redshift Spectrum - Data that doesn't require frequent analysis is moved off the compute nodes and stored in S3
    *   Learned about ElastiCache
        *   Supports two engines: Redis and Memcached
        *   Is placed in front of a database to cache data, reducing the load on the database layer
        *   Using ElastiCache requires writing and managing caching logic within the application

*   Lab19: VPC Peering
    *   Created a CloudFormation Template, configured Security Groups, and created 2 EC2 instances
    *   Created a Peering Connection between 2 VPCs and configured the Route Table to allow SSH to the server
    *   Successfully pinged after creating the VPC Peering

*   Lab57: Amazon S3
    *   Became familiar with creating buckets, storing/deleting/moving data in S3
    *   Learned about Bucket ACL, Bucket Policy, and Bucket Versioning
    *   Hosted a static website on S3
    *   Accelerated the static website hosting using CloudFront
    *   Copied S3 Object data to another region
