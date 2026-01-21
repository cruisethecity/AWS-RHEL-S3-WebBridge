AWS-RHEL-S3-WebBridge
Cloud Engineering Portfolio Project

This project demonstrates a secure, high-availability bridge between cloud storage and compute resources. I deployed a Red Hat Enterprise Linux (RHEL 9) web server on AWS EC2 and integrated it with Amazon S3 for dynamic content delivery.

Project Architecture and Milestones
Infrastructure: Provisioned a hardened RHEL 9 instance on AWS EC2.

Networking: Configured custom Security Groups to balance public accessibility with private security.

Web Engineering: Deployed and managed the Apache (httpd) service.

Data Integration: Utilized the AWS CLI to synchronize assets from S3 directly to the server's live web directory.

Technical Verification (Proof of Work)
1. Cloud Networking and Security
I configured Inbound Rules to bridge the gap between private management and public access. As shown in the architectural summary, Port 80 (HTTP) is open to the world, while Port 22 (SSH) remains restricted to a specific administrative IP for server hardening.

2. The S3-to-EC2 Bridge
This terminal log captures the exact moment the bridge was established. Using the aws s3 cp command, I pulled the index.html file from my secure bucket (kw21-rhel-logs-2026) into the /var/www/html/ directory.

3. Service Health and Handshake
I verified that the Apache service was active and responding with an HTTP/1.1 200 OK status. This ensures that the server software is correctly configured to handle incoming requests from the internet.

4. Final Live Environment
The successful deployment: A live website reachable via Public IPv4 (18.208.212.99), serving content hosted in secure cloud storage.

Challenges and Troubleshooting (The DevOps Mindset)
During this project, I encountered and resolved several critical errors that required a systematic troubleshooting approach:

Inbound Traffic Block: Initially, the website failed to load due to a Connection Timeout. I diagnosed this as a networking issue and resolved it by authoring a new Inbound Rule for Port 80 (HTTP) within the AWS Security Group.

Service Not Found Error: After copying the files, the server returned a Connection Refused error. I discovered that the httpd package was not yet installed on the RHEL instance. I utilized the yum package manager to install the service and systemctl to enable it on boot.

S3 Permission Gap: I encountered a 403 Forbidden error when trying to sync files. I corrected this by verifying my AWS CLI credentials and ensuring the EC2 instance had the proper permissions to read from the S3 bucket.

Future Phases
Phase 4: Implementing IAM Roles to replace manual access keys for improved security posture.

Phase 5: Automating this entire infrastructure setup using Terraform or User Data scripts
