---
title: "Week 2 Worklog"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Complete Module 2
* Understand the lesson content and prepare for labs to gain deeper practical knowledge and real-world application

### Tasks to be deployed this week:
| Day | Task                                                                                                                                     | Start Date | End Date   | Reference                                                                                                      |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | -------------------------------------------------------------------------------------------------------------- |
| Mon | -Study Module 02 - 01                                                                                                                    | 2025-09-15 | 2025-09-15 | [Module 02 - 01](https://www.youtube.com/watch?v=O9Ac_vGHquM&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| Tue | -Study Module 02 - 02                                                                                                                    | 2025-09-16 | 2025-09-16 | [Module 02 - 02](https://www.youtube.com/watch?v=BPuD1l2hEQ4&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=26) |
| Wed | -Study Module 02 - 03                                                                                                                    | 2025-09-17 | 2025-09-17 | [Module 02 - 03](https://www.youtube.com/watch?v=CXU8D3kyxIc&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=27) |
| Thu | Learn more about VPC services <br>&emsp;+ VPC <br>&emsp;+ Subnet <br>&emsp;+ Route Table <br>&emsp;+ Elastic IP <br> &emsp;+ Nat Gateway | 2025-09-18 | 2025-09-18 |                                                                                                                |
| Fri | I have an engagement on this day                                                                                                         | 2025-09-19 | 2025-09-19 |                                                                                                                |

### Week 2 Achievements:


*   Researched, learned, and gained a comprehensive understanding of VPC (Virtual Private Cloud).
    *   Understood that the primary purpose of a VPC is to isolate environments.

*   Learned more about subnets:
    *   Differentiated between Public and Private Subnets.
    *   Understood that a VPC allows the creation of multiple virtual networks, which can be divided into smaller networks called subnets.
    *   Learned about the five IP addresses reserved by AWS in each subnet.

*   Studied Route Tables:
    *   Understood the function of a route table.
    *   Learned the difference between a Default Route Table and a Custom Route Table.
    *   Understood the basic principle that a Custom Route Table must be configured to allow instances to connect to the internet.

*   Understood Elastic Network Interfaces (ENIs):
    *   Grasped the basic concept of an ENI: when an instance is launched in a VPC, its network resource address is not attached directly to the instance, but to a virtual network interface called an ENI.
    *   An ENI is a virtual network interface that can be detached from one EC2 instance and attached to another.

*   Understood Elastic IP Addresses (EIPs):
    *   Recognized that an EIP is a static, public IPv4 address.
    *   Noted that an unassociated EIP incurs a charge, highlighting the need to manage EIPs carefully to avoid unnecessary costs.

*   Understood VPC Endpoints:
    *   Learned the fundamental concepts.
    *   Understood the two types of Endpoints:
        *   Interface Endpoints
        *   Gateway Endpoints

*   Understood Internet Gateways (IGW) and NAT Gateways:
    *   Grasped the basic concept of an Internet Gateway: it enables instances in a public subnet to connect to the internet.
    *   Understood the purpose of a NAT Gateway.
    *   Identified the key differences between a NAT Gateway and an Internet Gateway:
        *   A NAT Gateway only allows outbound traffic and blocks unsolicited inbound connections from the internet.
        *   When configuring a custom route table:
            *   For an **Internet Gateway**, a route is created with a destination of `0.0.0.0/0` and a target of the IGW's ID.
            *   For a **NAT Gateway**, a route with a destination of `0.0.0.0/0` is placed in a private subnet's route table, with the NAT Gateway itself as the target. This enables instances in the private subnet to access the internet.

*   Understood Security Groups (SG) and Network Access Control Lists (NACLs):
    *   **SG** is a **stateful** firewall that applies rules to Elastic Network Interfaces. By default, it **denies all inbound traffic** and **allows all outbound traffic**.
    *   **NACL** is a **stateless** firewall that applies rules at the subnet level. By default, it **allows all inbound and outbound traffic**.

*   Gained a basic understanding of VPC Flow Logs:
    *   Understood it's a feature that captures information about the IP traffic going to and from network interfaces in your VPC.
    *   Noted that it does not capture the actual packet contents.

*   Understood VPC Peering and Transit Gateway:
    *   Understood VPC Peering as a feature that connects two or more VPCs, allowing resources to communicate directly for enhanced security.
    *   Understood Transit Gateway as a service used to connect VPCs and on-premises networks through a **central hub**.

*   Understood VPN and Direct Connect:
    *   Learned the concept of a Site-to-Site VPN, which is suitable for hybrid environments and requires configuring two endpoints:
        *   Virtual Private Gateway
        *   Customer Gateway
    *   Understood Direct Connect as a service that establishes a dedicated private connection from a data center to AWS, with scalable bandwidth.

*   Understood Elastic Load Balancing (ELB):
    *   Recognized it as a managed load balancing service by AWS.
    *   Supports HTTP, HTTPS, TCP, and SSL (Secure TCP) protocols.
    *   Has its own DNS name.
    *   Understood the health check feature and the different types of load balancers:
        *   Application Load Balancer (ALB)
        *   Network Load Balancer (NLB)
        *   Classic Load Balancer (CLB)
        *   Gateway Load Balancer (GWLB)
    *   Learned about the Sticky Sessions feature.