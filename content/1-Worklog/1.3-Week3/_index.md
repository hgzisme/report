---
title: "Week 3 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---


### Week 3 Goals:
*   Continue to study and learn more about AWS services
*   Learn about the EC2 service
*   Complete Lab 03

### Tasks for this week:
| Day | Task                                                                                                                                                                                                                                                                                                                                                 | Start Date | End Date   | Reference                                                                                                       |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | --------------------------------------------------------------------------------------------------------------- |
| Mon | - Complete Lab 03:<br>&emsp;+ Create VPC<br>&emsp;+ Create Route Table<br>&emsp;+ Create Security Group<br>&emsp;+ Create Subnet<br>&emsp;+ Understand Network Access Control Lists (NACLs)<br>&emsp;+ Create EC2 Instances<br>&emsp;+ Test connectivity<br>&emsp;+ Create NAT Gateway<br>&emsp;+ Create an Endpoint to connect with the NAT Gateway | 22/09/2025 | 22/09/2025 | [Lab03](https://000003.awsstudygroup.com/)                                                                      |
| Tue | - Study Module 03-01-01: Instance Types                                                                                                                                                                                                                                                                                                              | 23/09/2025 | 23/09/2025 | [Module 03-01-01](https://www.youtube.com/watch?v=e7XeKdOVq40&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=73) |
| Wed | - Study Module 03-01-02: AMI / Backup / Key Pair                                                                                                                                                                                                                                                                                                     | 24/09/2025 | 24/09/2025 | [Module 03-01-02](https://www.youtube.com/watch?v=yAR6QRT3N1k&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=74) |
| Thu | - Study Module 03-01-03: Elastic Block Store                                                                                                                                                                                                                                                                                                         | 25/09/2025 | 25/09/2025 | [Module 03-01-03](https://www.youtube.com/watch?v=hKr_TfGP7NY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=75) |
| Fri | - Study Module 03-01-04: Instance Store                                                                                                                                                                                                                                                                                                              | 26/09/2025 | 26/09/2025 | [Module 03-01-04](https://www.youtube.com/watch?v=6IHNDJ85aoQ&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=76) |

### Week 3 Achievements:
*   Completed Lab 03, with the following achievements:
    *   Learned how to create a VPC and subnets
    *   Configured Route Tables, Security Groups, and learned about NACLs
    *   Successfully created an EC2 Instance and tested connectivity
        *   Used MobaXterm for connection
    *   Created a NAT Gateway and a connecting Endpoint
        *   Also tested the Endpoint's connectivity

*   Module 03-01-01: Instance Types
    *   Understood what an Instance Type is
    *   Understood the components of an EC2 Instance
    *   Hardware Node
        *   Has a Placement Option feature
        *   Hypervisor
        *   PV: Paravirtualization
        *   HVM: Hardware Virtual Machine
        *   KVM: Nitro
        *   AZ (Availability Zone)

*   Module 03-01-02: AMI / Backup / Key Pair
    *   Understood what an AMI (Amazon Machine Image) is
    *   Understood how to back up EC2 Instances by creating Snapshots
    *   Learned what a Key Pair is and its purpose

*   Module 03-01-03: Elastic Block Store (EBS)
    *   Understood what EBS is
    *   Understood how EBS and EC2 are connected
    *   Learned that EBS has two disk types: HDD and SSD
    *   Researched the reasons why EBS can achieve 99.999% high availability
    *   Learned about EBS-Optimized Instances
    *   EBS Multi-Attach feature: An EBS volume can be attached to multiple EC2 instances running on the Nitro Hypervisor
    *   Learned to back up EBS by taking snapshots to S3

*   Module 03-01-04: Instance Store
    *   Understood what an Instance Store is
    *   Understood the differences between EBS and Instance Store
    *   Understood the relationship between Instance Store and EC2
    *   Instance Store use cases: for scenarios requiring extremely high performance, up to millions of IOPS:
        *   Swap
        *   Paging
        *   Buffer / Cache
        *   Logs