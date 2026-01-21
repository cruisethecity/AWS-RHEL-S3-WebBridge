AWS-RHEL-S3-WebBridge
A Cloud Engineering Portfolio Project

This project demonstrates a secure, high-availability "Bridge" between cloud storage and compute. I deployed a Red Hat Enterprise Linux (RHEL 9) web server on AWS EC2 and integrated it with Amazon S3 for dynamic, automated content delivery.

Project Architecture & Milestones
Infrastructure: Provisioned a hardened RHEL 9 instance on AWS EC2.

Networking: Configured custom Security Groups to balance public accessibility with private security.

Web Engineering: Deployed and managed the Apache (httpd) service.

Data Integration: Utilized the AWS CLI to synchronize assets from S3 directly to the server's live web directory.

Technical Verification (Proof of Work)
1. Cloud Networking & Security
I configured Inbound Rules to bridge the gap between private management and public access. As shown below, Port 80 (HTTP) is open to the world, while Port 22 (SSH) remains restricted to a specific administrative IP.

2. The S3-to-EC2 Bridge
This terminal log captures the exact moment the "Bridge" was established. Using the aws s3 cp command, I pulled the index.html file from my secure bucket into the /var/www/html/ directory.

3. Service Health & Handshake
I verified that the Apache service was not only running but actively serving the correct headers. The HTTP/1.1 200 OK status proves a healthy connection between the server and the browser.

4. Final Live Environment
The successful deployment: A live website reachable via Public IP, serving content hosted in secure cloud storage.

Challenges & Troubleshooting (The "DevOps" Mindset)
No cloud deployment is without friction. During this project, I encountered and resolved several critical "Connection Refused" and "Timeout" errors:

The Inbound Traffic Block: Initially, the website would not load because the default AWS Security Group blocked all traffic except SSH. I diagnosed this as a Connection Timeout and resolved it by manually authoring an Inbound Rule for Port 80 (HTTP).

The "Service Not Found" Error: After copying the files, the server returned a Connection Refused error. I discovered that while the server was running, the httpd software was not yet installed. I utilized yum to install the service and systemctl to enable it on boot.

The S3 Permission Gap: I initially encountered a 403 Forbidden error when trying to sync files. I corrected this by verifying my AWS CLI credentials and ensuring the EC2 instance had the proper permissions to "read" from the S3 bucket.

Future Phases
Phase 4: Implementing IAM Roles to replace manual access keys for better security.

Phase 5: Automating this entire setup using Terraform or a User Data script.
