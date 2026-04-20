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






