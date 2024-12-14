# Save the current README content into a file for download
file_path = "/mnt/data/README_Infrastructure_Setup.md"

content = """# README: Infrastructure Setup and Configuration

## Overview
This document outlines the steps required to set up and configure the necessary infrastructure and servers for the project.

---

## Steps to Launch Infrastructure

### 1. Launch Two Servers
- **WebServer**: Hosts the Nginx web server and serves PHP requests.
- **AppServer**: Manages the database connection and application logic.

### 2. Create AWS Resources
- **RDS Instance**:
  - Launch an Amazon RDS instance for MySQL.
  - Ensure the AppServer's security group is added to the RDS security group for access.
- **S3 Bucket**:
  - Create an S3 bucket with ACL (Access Control List) enabled.
- **CloudFront Distribution**:
  - Configure a CloudFront distribution for the S3 bucket to serve static files globally.

---

## Server Configurations

### WebServer Configuration

1. **Install LEMP Stack**:
   - Install **Linux**, **Nginx**, **MySQL**, and **PHP** on the WebServer.

2. **Update Nginx Configuration**:
   - Edit the Nginx configuration file to handle PHP requests:

     ```nginx
     location ~ \\.php$ {
         proxy_pass http://<AppServer-IP>;
         proxy_set_header Host $host;
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header X-Forwarded-Proto $scheme;
     }
     ```

3. **Restart Nginx**:
   - Restart the Nginx service to apply changes.

### AppServer Configuration

1. **Install MySQL**:
   - Install MySQL on the AppServer.
   - Connect to the RDS instance and create the required database.

2. **Set Up Folder Permissions**:
   - Create an `uploads` folder:
     ```bash
     mkdir /path/to/uploads
     chmod 777 /path/to/uploads
     ```

3. **Install AWS SDK and Composer**:
   - Install Composer:
     ```bash
     curl -sS https://getcomposer.org/installer | php
     mv composer.phar /usr/local/bin/composer
     ```
   - Use Composer to install the AWS SDK:
     ```bash
     composer require aws/aws-sdk-php
     ```

---

## Notes
- Ensure all security groups, IAM roles, and permissions
