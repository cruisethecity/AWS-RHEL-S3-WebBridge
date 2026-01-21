# AWS-RHEL-S3-WebBridge 
This project demonstrates a secure, automated "Bridge" between cloud storage and compute. I deployed a Red Hat Enterprise Linux (RHEL 9) web server on AWS and integrated it with Amazon S3 for dynamic content delivery.

## Phase 3 Milestones
* **Cloud Infrastructure:** Provisioned RHEL 9 on EC2 with customized Security Groups.
* **Web Engineering:** Installed and hardened Apache (`httpd`) services.
* **Data Integration:** Automated the synchronization of web assets from S3 to `/var/www/html/` using AWS CLI.

---

##  Technical Verification (Proof of Work)

### 1. Networking & Security
Configured Inbound Rules to allow Port 80 (HTTP) for public access while maintaining Port 22 (SSH) for private administration.
![Security Groups](images/image_aaa93b.png)

### 2. S3-to-EC2 Bridge
The terminal proof of the `aws s3 cp` command successfully pulling the `index.html` file into the RHEL web directory.
![Proof of Transfer](images/Proof%20of%20Transfer.PNG)

### 3. Service Health
Verification that the Apache service is active and responding with an `HTTP 200 OK` status.
![Apache Verification](images/Apache%20verification.PNG)

### 4. Live Environment
The final deployment: A live website reachable via Public IP, serving content hosted in S3.
![Live Website](images/System%20Online%20webpage.PNG)
