# WordPress Deployment with Ansible

## Overview
This project automates the deployment of WordPress using **Ansible** with the following technologies:
- **Apache** as the web server
- **MariaDB** as the database server
- **PHP** with required extensions for WordPress

The playbook deploys and configures the following:
- MariaDB with a WordPress database and user
- Apache server to host WordPress
- PHP with necessary extensions to run WordPress

## Prerequisites

Before running the Ansible playbook, ensure you have the following:

1. **Ansible** installed on your control machine.
2. **EC2 instance or any Linux-based server** for deployment.
3. The target machine (client) should have **SSH** access from the Ansible control machine.
4. **Apache**, **MariaDB**, and **PHP** are to be installed on the target machine.

## Project Structure

Here is the structure of the project directory:
![diagram-export-4-9-2025-8_55_23-PM](https://github.com/user-attachments/assets/00359b0c-3144-4ec4-bb9c-f8138fed9335)


## Setup Instructions

### Step 1: Clone the Project

Clone this project to your local machine or directly onto your control node:
```bash
git clone git@github.com:IBRAHIMRAMADANABDU/ansible-project.git
cd ansible-project/
```
Step 2: Update the Inventory File
Update the inventory.ini file with the details of your target servers. For example:
```bash
[web]
wordpress  ansible_host=3.91.232.150 ansible_user=ec2-user mariadb_root_password="rootpass" mariadb_wp_db="wordpress" mariadb_wp_user="wpuser" mariadb_wp_password="wppassword"
```
This inventory file contains the host details for your WordPress instance(s).

Step 3: Modify the Variables (Optional)
You can modify variables in the playbook.yaml or within the roles themselves. Some variables to consider modifying:

mariadb_root_password: The root password for MariaDB

mariadb_wp_user: WordPress database user

mariadb_wp_password: Password for the WordPress database user

mariadb_wp_db: The name of the WordPress database

You can define these variables directly in the playbook or use group_vars and host_vars for a more structured approach.
Step 4: Run the Ansible Playbook
Run the playbook to deploy WordPress:
```bash
ansible-playbook -i inventory.ini playbook.yaml
This will install and configure Apache, MariaDB, and PHP, then download and set up WordPress.
```
Step 5: Verify the Deployment
Once the playbook runs successfully, open your web browser and navigate to the target server's IP or domain name:
```bash
http://<your-server-ip>/wordpress
You should see the WordPress setup page where you can complete the installation.
```
Step 6: Admin Access
To access the WordPress admin panel, navigate to:
```bash
http://<your-server-ip>/wordpress/wp-admin
Log in using the credentials you created during setup.
```
Role Descriptions
1. Apache Role
Installs Apache (httpd package).

Configures Apache to serve WordPress from /var/www/html/wordpress.

Ensures Apache is started and enabled to run on boot.

2. MariaDB Role
Installs MariaDB and starts the service.

Secures the MariaDB root user by setting a password.

Creates a database for WordPress.

Creates a WordPress database user and grants the necessary permissions.

3. WordPress Role
Downloads the latest WordPress package.

Extracts the WordPress package to /var/www/html/wordpress.

Sets the correct permissions for WordPress files.

Configures wp-config.php to connect to the MariaDB database.
