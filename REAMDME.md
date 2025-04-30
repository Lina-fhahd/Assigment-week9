AWS Week-9 Assignment – Static Website Deployment

Prepared by: Lina

Services Used

• Amazon S3 – For hosting static website files

• EC2 with Launch Template – To install NGINX and pull content

• Auto Scaling Group (ASG) – To maintain availability

• Application Load Balancer (ALB) – For distributing HTTP traffic

• IAM Role – To grant EC2 permission to access S3

Deployment Summary

• S3 Bucket: lina-clarusway-assets

• Files uploaded: index.html, logo.png, image1.png

• Static website hosting enabled

• Public read access configured via Bucket Policy

• Launch Template: clarusway-launch-template

• Configured with User Data to install NGINX and fetch files from S3

• Auto Scaling Group: clarusway-asg

• Desired capacity: 2 | Min: 1 | Max: 3

• Linked to the Launch Template

• Application Load Balancer

• Port: 80 (HTTP)

• Connected to Target Group: clarusway

• Automatically registers EC2 instances from ASG

Issue Faced

The website was not loading because the Application Load Balancer (ALB) showed an Unhealthy status for the EC2 instances.

Root Cause

The problem was due to a misconfigured Health Check in the ALB and missing content (images) in the S3 bucket, which caused NGINX to serve incomplete or faulty responses.

Solution

1. Health Check Configuration:

• Corrected the health check path in the ALB settings (e.g., /index.html or /) to ensure it targeted a valid resource.

• Verified that port 80 was open and accessible.

2. S3 Content Update:

• Uploaded all required static files (index.html, images) to ensure complete content delivery via NGINX.

3. Security Groups:

• Confirmed that the security groups for both ALB and EC2 allowed inbound traffic on port 80.

4. NGINX Configuration:

• Ensured that the NGINX service was active and properly serving files from the correct directory.

After applying these fixes, the EC2 instances turned Healthy, and the website became accessible without issues.

