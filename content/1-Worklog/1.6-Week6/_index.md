---
title: "Week 6 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Goals:

*   Continue studying Module 04
*   Study Module 05
*   Prepare for lab exercises

### Tasks for this week:
| Day | Task                                                                                                                                                                                           | Start Date   | End Date        | Resources                                |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------------- |
| Mon | - Study Module 04 - 04: Snow Family - Storage Gateway - Backup                                                                                                                                 | 13/10/2025   | 13/10/2025      | [Module 04 - 04](https://www.youtube.com/watch?v=YXn8Q_Hpsu4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=106) |
| Tue | - Study Module 05 - 01: Shared Responsibility Model <br> - Study Module 05 - 02: Amazon Identity and Access Management                                                                            | 14/10/2025   | 14/10/2025      | [Module 05 - 01](https://www.youtube.com/watch?v=tsobAlSg19g&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=150) <br> [Module 05 - 02](https://www.youtube.com/watch?v=N_vlJGAqZxo&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=151)  |
| Wed | - Study Module 05 - 03: Amazon Cognito <br> - Study Module 05 - 04: AWS Organizations                                                                                                          | 15/10/2025   | 15/10/2025      | [Module 05 - 03](https://www.youtube.com/watch?v=pZ2fgEFK3Vs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=152) <br> [Module 05 - 04](https://www.youtube.com/watch?v=5oQY8Rogz9Y&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=153) |
| Thu | - Revise blog translation and submit the missing translated article <br>- Study Module 05 - 05: AWS Identity Center (SSO) <br> - Study Module 05 - 06: Amazon Key Management Service            | 16/10/2025   | 16/10/2025      | [Module 05 - 05](https://www.youtube.com/watch?v=NW1xrMkNMjU&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=154) <br> [Module 05 - 06](https://www.youtube.com/watch?v=GMihNQojhZc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=155)  |
| Fri | - Study Module 05 - 07: AWS Security Hub                                                                                       | 17/10/2025   | 17/10/2025      | [Module 05 - 07](https://www.youtube.com/watch?v=clj2E0rNBEs&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=156) <br> [Module 05 - 08](https://www.youtube.com/watch?v=0SdpD2GPYz4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=157) |

### Week 6 Outcomes:
*   Module 04 - 04: Snow Family - Storage Gateway - Backup
    *   Learned about the Snow Family:
        *   Snowball
        *   Snowball Edge
        *   Snowmobile
    *   Learned about Storage Gateway: a hybrid storage solution that combines storage in a traditional on-premises environment with the AWS cloud environment.
        *   File Gateway: Stores and retrieves objects in S3 using Network File Sharing (NFS) and Server Message Block (SMB).
        *   Volume Gateway: Uses the iSCSI protocol to store block data in S3, accessed via EBS snapshots (automated by AWS Backup), which can then be used to create EBS Volumes.
        *   Tape Gateway: Provides backup applications with an iSCSI virtual tape library (VTL) interface. Virtual tape data is stored in Amazon S3 or Amazon Glacier.
    *   Studied Storage Gateway.
    *   Learned about Disaster Recovery:
        *   Recovery Time Objective (RTO): The shortest time to restore a service.
        *   Recovery Point Objective (RPO): The maximum acceptable period of data loss.
    *   Learned about 4 recovery strategies:
        *   Backup and Restore
        *   Pilot Light (Active - Standby)
        *   Low-capacity Active - Active
        *   Full-capacity Active - Active
    *   Learned about AWS Backup:
        *   It is a managed backup service.
        *   Can be configured and scheduled (backup schedule).
        *   Has backup policies (backup retention).
        *   Monitors backup activities for AWS resources such as EBS, EC2, Amazon RDS, Amazon DynamoDB, Amazon EFS, and AWS Storage Gateway Volumes.

*   Module 05 - 01: Shared Responsibility Model
    *   Learned about the Shared Responsibility Model.
    *   Security responsibilities vary depending on the service type:
        *   Infrastructure-level services => Customer's responsibility.
        *   Managed services with shared control => Shared responsibility between the customer and AWS.
        *   Services fully managed by AWS => AWS's responsibility.

*   Module 05 - 02: Amazon Identity and Access Management
    *   Gained a deeper understanding of the IAM service, understanding the concepts of IAM User, Group, Role, and Policy (Identity-based policy and Resource-based policy).

*   Module 05 - 03: Amazon Cognito
    *   Understood the purpose of Cognito: helps with user authentication, authorization, and management.
    *   Understood the two main components of Cognito:
        *   User Pools: User directories that provide sign-up and sign-in options.
        *   Identity Pools: Provide users with access to other AWS services.
        *   User Pools and Identity Pools can be combined to provide direct access to AWS services.

*   Module 05 - 04: AWS Organizations
    *   Learned about AWS Organizations.
        *   Understood Organizational Units (OUs) (can create new AWS accounts, allocate resources, and organize AWS accounts), and Consolidated Billing.
        *   Service Control Policies (SCPs):
            *   Can be applied to OUs and AWS Accounts.
            *   SCPs only set the maximum permissions for IAM Users or IAM Roles within the assigned OU or AWS Account.
            *   Allow for the setup of deny-based policies.

*   Module 05 - 05: AWS Identity Center (SSO)
    *   Learned about AWS Identity Center.
    *   Learned the concept of a Permission Set: the level of access that Users and Groups have to the AWS accounts within an AWS Organization.

*   Module 05 - 06: Amazon Key Management Service
    *   Learned about the KMS data encryption service.
        *   Customer Managed Key (CMK).
        *   Data Key: A type of key used outside of AWS KMS to encrypt data.

*   Module 05 - 07: AWS Security Hub
    *   Learned about Security Hub and its features.
    *   Security Hub runs continuously, checking service configurations and performing security checks based on AWS best practices.