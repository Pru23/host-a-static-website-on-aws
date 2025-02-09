![Alt text](/Host-a-Static-Website_on_AWS.png)
# Host a Static Website on AWS

## Project Overview
This project demonstrates how to host a static HTML web application on AWS, utilizing various AWS resources to ensure security, scalability, and reliability. The deployment follows best practices, leveraging a multi-tier architecture.

## Architecture Diagram
A reference architecture diagram for this project is available in the project's GitHub repository.

## AWS Services Used
The following AWS services and resources were utilized in this project:

1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones for high availability.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups**: Implemented as network firewalls to control inbound and outbound traffic.
4. **Multi-AZ Deployment**: Enhances system reliability and fault tolerance.
5. **Public Subnets**: Used for infrastructure components such as the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Ensures secure connections to assets within both public and private subnets.
7. **Private Subnets**: Hosts web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Allows instances in private subnets to access the Internet securely.
9. **EC2 Instances**: Hosts the static website.
10. **Application Load Balancer (ALB)**: Distributes web traffic evenly across EC2 instances within an Auto Scaling Group.
11. **Auto Scaling Group (ASG)**: Ensures availability, scalability, fault tolerance, and elasticity of web servers.
12. **GitHub**: Used for version control and collaboration on web files.
13. **AWS Certificate Manager**: Secures application communications.
14. **Amazon Simple Notification Service (SNS)**: Provides alerts for Auto Scaling Group activities.
15. **Amazon Route 53**: Manages domain registration and DNS records.

## Deployment Steps
Follow these steps to deploy the static website:

### 1. Setup AWS Infrastructure
- Configure a **VPC** with public and private subnets.
- Deploy an **Internet Gateway** for external connectivity.
- Establish **Security Groups** for network security.
- Deploy **EC2 Instances** in private subnets.
- Set up an **Auto Scaling Group** to manage EC2 instances.
- Deploy an **Application Load Balancer (ALB)** to handle traffic distribution.
- Configure **Route 53** for domain registration and DNS routing.
- Implement **AWS Certificate Manager** for HTTPS security.
- Enable **SNS** for Auto Scaling alerts.

### 2. Install and Configure Apache Web Server
On each EC2 instance, execute the following script to install and configure the web server:

```bash
#!/bin/bash
# Switch to the root user
sudo su

# Update all installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Start the Apache service
systemctl start httpd
systemctl enable httpd

# Install Git
yum install git -y

# Navigate to Apache web root and clone the repository
cd /var/www/html
git clone https://github.com/Pru23/host-a-static-website-on-aws.git

# Copy all files from the cloned repository to the web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Clean up unnecessary files
rm -rf host-a-static-website-on-aws
```

### 3. Accessing the Website
After deployment, the website will be accessible via the domain registered in **Route 53** or through the **ALB's public DNS**.

## Project Repository
All necessary files, including deployment scripts and architecture diagrams, are available in the [GitHub Repository](https://github.com/Pru23/host-a-static-website-on-aws).

## Conclusion
This project effectively demonstrates how to deploy a static web application on AWS using best practices in cloud infrastructure, security, and automation. By leveraging AWS services like EC2, ALB, Auto Scaling, and Route 53, the solution ensures high availability, scalability, and security for hosting static websites.




