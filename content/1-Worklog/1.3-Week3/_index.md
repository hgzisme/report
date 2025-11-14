---
title: "Week 3 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
*   Continue to study and learn more about AWS services
*   Learn about the EC2 service
*   Complete Lab 03

### Tasks for this week:
| Day | Task                                                                                                                                                                                                                                                                                                                         | Start Date   | Completion Date | Reference                                                                                                                                                                                                                    |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 2   | - Complete Lab 03:<br>&emsp;+ Create a VPC<br>&emsp;+ Create a Route Table<br>&emsp;+ Create a Security Group<br>&emsp;+ Create Subnets<br>&emsp;+ Understand Network Access Control Lists (NACLs)<br>&emsp;+ Create EC2 Instances<br>&emsp;+ Test connectivity<br>&emsp;+ Create a NAT Gateway<br>&emsp;+ Create a VPC Endpoint and test its connection | 09/22/2025   | 09/22/2025      | [Lab03](https://000003.awsstudygroup.com/)                                                                                                                                                                                     |
| 3   | - Study Module 03-01-01: Instance Types                                                                                                                                                                                                                                                                               | 09/23/2025   | 09/23/2025      | [Module 03-01-01](https://www.youtube.com/watch?v=e7XeKdOVq40&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=73)   |
| 4   | - Study Module 03-01-02: AMI / Backup / Key Pair                                                                                                                                                                                                                                                                          | 09/24/2025   | 09/24/2025      | [Module 03-01-02](https://www.youtube.com/watch?v=yAR6QRT3N1k&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=74)                                                                                                                                                                                                                            |
| 5   | - Study Module 03-01-03: Elastic Block Store                                                                                                                                                                                                                                                                             | 09/25/2025   | 09/25/2025      | [Module 03-01-03](https://www.youtube.com/watch?v=hKr_TfGP7NY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=75)                                                                                                                                                                                    |
| 6   | - Study Module 03-01-04: Instance Store                                                                                                                                                                                                                                                                                        | 09/26/2025   | 09/26/2025      | [Module 03-01-04](https://www.youtube.com/watch?v=6IHNDJ85aoQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=76)                                                                                                                                                                                              |

### Week 3 Achievements:
*   Completed Lab 03, achievements include:
    *   Learned how to create a VPC and subnets.
    *   Configured Route Tables, Security Groups, and learned about NACLs.
    *   Successfully created an EC2 instance and tested connectivity.
        *   Used MobaXterm for the connection.
    *   Created a NAT Gateway and a VPC Endpoint.
        *   Also tested the Endpoint's connectivity.
        *   Note: To connect to the private instance, the instance's inbound Security Group rules had to be modified to allow SSH traffic from the Endpoint's Security Group.

*   Module 03-01-01: Instance Types
    *   Understood what an Instance Type is.
    *   Understood the core components of an EC2 Instance.
    *   Hardware Node
        *   Features Placement Options.
        *   Hypervisor
        *   PV: Paravirtualization
        *   HVM: Hardware Virtual Machine
        *   KVM: Nitro
        *   Availability Zone (AZ)

*   Module 03-01-02: AMI / Backup / Key Pair
    *   Understood what an AMI (Amazon Machine Image) is.
    *   Understood how to back up EC2 instances by creating Snapshots.
    *   Learned what a Key Pair is and its purpose.

*   Module 03-01-03: Elastic Block Store (EBS)
    *   Understood what EBS is.
    *   Understood how EBS volumes and EC2 instances are connected.
    *   Learned that EBS has two main volume types: HDD and SSD.
    *   Briefly researched the reasons why EBS can achieve 99.999% high availability.
    *   Learned about EBS-Optimized Instances.
    *   EBS Multi-Attach feature: An EBS volume can be attached to multiple EC2 instances running on the Nitro hypervisor.
    *   EBS volumes are backed up by taking snapshots, which are stored in S3.

*   Module 03-01-04: Instance Store
    *   Understood what an Instance Store is.
    *   Understood the differences between EBS and Instance Store.
    *   Understood the relationship between Instance Store and EC2.
    *   Use cases for Instance Store: for applications requiring extremely high performance (up to millions of IOPS), such as:
        *   Swap
        *   Paging
        *   Buffer / Cache
        *   Logs