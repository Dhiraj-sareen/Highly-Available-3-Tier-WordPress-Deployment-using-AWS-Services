# Highly-Available-3-Tier-WordPress-Deployment-using-AWS-Services

This project focuses on deploying a WordPress website using a traditional 3-tier architecture on AWS. Instead of putting everything on a single server, the system is split into three layers: the presentation layer, the application layer, and the database layer.

The main idea behind this project was to simulate how an actual production-grade web application is deployed in the cloud. By separating concerns and distributing components across multiple services, we reduce single points of failure and make the system easier to scale and maintain. The setup uses AWS services like VPC, EC2, RDS, EFS, and ALB to build a system where users can access a WordPress website through a load balancer, while the backend and database remain protected inside private subnets.

# Features

This project includes several important features that make it closer to a real-world deployment:

- Multi-AZ deployment to improve availability and fault tolerance
- Clear separation between public and private subnets
- Application Load Balancer to distribute incoming traffic
- EC2 instances running WordPress in private subnets
- Amazon RDS (MySQL) for managed and reliable database storage
- Elastic File System (EFS) for shared storage across instances
- NAT Gateways to allow secure outbound internet access
- Security Groups to control traffic between different layers
- Bastion host setup for secure SSH access to private instances
- Scalable design that can be extended using Auto Scaling

# Architecture / How It Works

![Architecture Diagram](Result/Architecture%20Diagram.png)

The architecture is designed in a way that separates concerns and keeps sensitive components secure. At the base level, a VPC (Virtual Private Cloud) is created with the CIDR block 10.0.0.0/16. This acts as the network boundary for the entire project. Inside the VPC, multiple subnets are created across two availability zones to ensure high availability.

- 2 Public Subnets (for ALB and NAT Gateways)
- 2 Private App Subnets (for EC2 instances)
- 2 Private DB Subnets (for RDS)

The Internet Gateway (IGW) is attached to the VPC to allow resources in public subnets to communicate with the internet. Meanwhile, private subnets do not have direct internet access. Instead, they use NAT Gateways placed in public subnets to access external resources securely (like downloading packages or updates).

The Application Load Balancer (ALB) sits in the public subnets and acts as the entry point for users. When someone opens the website, the request hits the ALB, which then forwards it to one of the EC2 instances in the private subnets.

The application layer consists of EC2 instances running Apache, PHP, and WordPress. These instances are not directly exposed to the internet, which improves security. Instead, they only accept traffic from the ALB.

To make sure all EC2 instances serve the same content, EFS (Elastic File System) is used. It is mounted on all EC2 instances so that uploaded files, themes, and plugins are shared across servers.

The database layer uses Amazon RDS (MySQL), which is deployed in private subnets. It is not publicly accessible and can only be accessed by the application layer through a security group rule.

Security Groups act like firewalls between layers:

- ALB → accepts traffic from the internet
- EC2 → accepts traffic only from ALB
- RDS → accepts traffic only from EC2
- EFS → allows NFS access from EC2

This layered design ensures that even if one part is exposed, the rest of the system remains protected.

# Setup Instructions

**#1: Networking Setup -**

Create a **VPC (10.0.0.0/16)** with DNS hostnames enabled, then set up subnets across multiple AZs for availability.

![Architecture Diagram](Result/vpc.png)

* **2 public subnets**
* **4 private subnets** (app + DB)
* Attach **Internet Gateway (IGW)**
* Route tables: Public → IGW, Private → NAT
This forms the basic, secure network foundation.

![Architecture Diagram](Result/subnets%-%1.png)





