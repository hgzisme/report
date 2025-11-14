---
title: "Week 5 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

*   Study Module 04
*   Complete Lab 10
*   Translate and submit a blog post

### Tasks for this week:
| Day | Task                                                                                                                              | Start Date   | Completion Date | Reference                                                                                                                                                                                                                                 |
| --- | --------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Study Module 04-01: Cloud Storage Services <br>- Study Module 04-02: Amazon Simple Storage Service (S3) - Access Point - Storage Classes | 10/06/2025   | 10/06/2025      | [Module 04-01](https://www.youtube.com/watch?v=hsCfP0IxoaM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=103) & [Module 04-02](https://www.youtube.com/watch?v=_yunukwcAwc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=104) |
| 3   | - Study Module 04-03: S3 Static Website & CORS - Access Control - Object Key & Performance - Glacier                           | 10/07/2025   | 10/07/2025      | [Module 04-03](https://www.youtube.com/watch?v=mPBjB6Ltl_Q&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=105)                                                                                                                            |
| 4   | - Complete Lab 10                                                                                                                 | 10/08/2025   | 10/08/2025      | [Lab10](https://000010.awsstudygroup.com/)                                                                                                                                                                                              |
| 5   | - Translate an AWS blog post                                                                                                      | 10/09/2025   | 10/09/2025      |                                                                                                                                                                                                                                         |
| 6   | - Continue translating and submit the blog post                                                                                   | 10/10/2025   | 10/10/2025      |                                                                                                                                                                                                                                         |

### Week 5 Achievements:

*   Module 04-01: Cloud Storage Services
    *   Initial introduction to the S3 service and related services such as:
        *   Amazon Storage Gateway
        *   AWS Snow Family
        *   Disaster Recovery on AWS
        *   AWS Backup

*   Module 04-02: Amazon Simple Storage Service (S3) - Access Point - Storage Classes
    *   Learned about the S3 service.
    *   Understood the concept of an Access Point.
    *   Learned about S3 storage classes:
        *   S3 Standard
        *   S3 Standard-IA (Infrequent Access)
        *   S3 Intelligent-Tiering
        *   S3 One Zone-IA
        *   S3 Glacier / Deep Archive

*   Module 04-03: S3 Static Website & CORS - Access Control - Object Key & Performance - Glacier
    *   Understood how S3 hosts static websites.
    *   Understood the concept of a Single Page Application (SPA).
    *   Controlling access to S3:
        *   Using S3 Access Control Lists (ACLs)
        *   Using S3 Bucket Policies
        *   Using IAM Policies
    *   Learned about two S3 features:
        *   Endpoints
        *   Versioning
    *   Understood how S3 stores data:
        *   Object Key
        *   Learned about the internal partitioning in S3 for data storage. As the amount of data increases, partitions split automatically, which can indirectly impact S3 performance.
    *   Optimizing S3 performance using random prefixes to distribute objects across as many partitions as possible.
    *   Learned about Glacier.

*   Completed Lab 10, achievements include:
    *   Gained an introduction to the AWS CloudFormation service.
    *   Practiced creating a template, reconfiguring a Security Group (SG), and connecting to an EC2 Instance using a Remote Desktop Gateway Server (RDGW).
    *   Practiced creating a Directory Service.
    *   Learned about Route 53:
        *   Created an Outbound Endpoint for Route 53.
        *   Created Resolver Rules.
        *   Created an Inbound Endpoint for Route 53.
    *   Successfully tested the connection afterward.
    *   Successfully established a connection between an on-premises environment and the AWS environment via Directory Service and a Remote Desktop Gateway Server.