# ICT171 Cloud Server Project

**Student Name:** Muhammad Shavaiz
**Student ID:** 35332358

**Public IP Address:** 4.230.142.25
**Domain Name:** shavaiz.cloud

***

## 1. Project Overview

This project demonstrates the deployment of a cloud-based web server using an Infrastructure as a Service (IaaS) model.
I created a Linux virtual machine on Microsoft Azure, installed Nginx, configured a firewall, deployed a portfolio website, and attached a custom domain using DNS.

The server is publicly accessible via both its IP address and domain name.

**Technologies used:**
* Microsoft Azure Virtual Machine (Ubuntu 22.04 LTS)
* SSH remote administration
* Nginx web server
* UFW firewall
* DNS A-record (GoDaddy)
* Bash scripting
* GitHub version control

***

## 2. Architecture Overview

Client (Browser)
│
▼
DNS: shavaiz.cloud → Public IP: 4.230.142.25
│
▼
Azure Virtual Machine (Ubuntu 22.04)
│
▼
Nginx Web Server
│
▼
/var/www/html/index.html

**Key components:**
* **DNS:** Domain → IP mapping using an A-record
* **Azure VM:** IaaS Linux server hosting the web application
* **Firewall:** UFW on Linux + Azure Network Security Group
* **Nginx:** Web server serving HTML files
* **Script:** Automated system checks and backup

***

## 3. Azure Virtual Machine Setup

### VM Configuration

* **Resource group:** rg-ict171
* **VM name:** ict171-vm
* **Region:** (closest Azure region)
* **Image:** Ubuntu Server 22.04 LTS
* **Size:** Standard B1s (1 vCPU, 1 GiB RAM)
* **Authentication:** Password
* **Username:** azureuser
* **Inbound ports allowed:** SSH (22), HTTP (80)

### SSH Access

Use this command to connect:
ssh azureuser@4.230.142.25

***

## 4. Server Configuration

### 4.1 Update System and Install Utilities

sudo apt update && sudo apt upgrade -y
sudo apt install -y ufw git curl

### 4.2 Install Nginx Web Server

sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx

**Verify Nginx Status:**
systemctl status nginx

***

## 5. Firewall Configuration (UFW)

sudo ufw allow OpenSSH
sudo ufw allow 'Nginx HTTP'
sudo ufw --force enable
sudo ufw status

**Firewall now allows:**
* SSH (22)
* HTTP (80)

All other traffic is blocked.

***

## 6. Website Deployment

### Replace Default Page

cd /var/www/html
sudo mv index.nginx-debian.html index.backup.html
sudo nano index.html

### Custom HTML (Portfolio Website)

<!DOCTYPE html>
<html>
<head>
<title>ICT171 Cloud Server Project</title>
<style>
body { font-family: Arial; padding:40px; line-height:1.6; }
h1 { color:#333; }
footer { margin-top:50px; color:#777; }
</style>
</head>
<body>

<h1>ICT171 Cloud Server Project</h1>
<h3>Muhammad Shavaiz – 35332358</h3>

<p>This website is hosted on a Microsoft Azure virtual machine running Ubuntu Server and Nginx.</p>

<h3>Skills Demonstrated:</h3>
<ul>
<li>Deploying an IaaS cloud server</li>
<li>Installing & configuring Nginx</li>
<li>Firewall configuration (UFW + Azure NSG)</li>
<li>DNS management</li>
<li>Bash scripting for automation</li>
<li>Git & GitHub version control</li>
</ul>

<footer>
Public IP: 4.230.142.25 — Domain: shavaiz.cloud
</footer>

</body>
</html>

The website is live at: http://shavaiz.cloud

***

## 7. DNS Configuration (GoDaddy)

I purchased the domain shavaiz.cloud and configured DNS using the GoDaddy DNS manager.

| Type | Name | Value | TTL |
| :--- | :--- | :--- | :--- |
| **A-Record** (Main Domain) | A | @ | 4.230.142.25 | Default |
| **CNAME** (WWW → Root Domain) | CNAME | www | shavaiz.cloud | Default |

After DNS propagation, both:
* http://shavaiz.cloud
* http://www.shavaiz.cloud

work correctly.

***

## 8. Bash Script (Automation Component)

### Script Path
scripts/server_check_and_backup.sh

### Purpose of the Script
* Check if Nginx is running
* Display firewall rules
* Create a timestamped backup of /var/www/html

### Script Code

#!/usr/bin/env bash

echo "===== ICT171 Server Report ====="
echo "Student: Muhammad Shavaiz (35332358)"
echo "Public IP: 4.230.142.25"
echo "Date: $(date)"
echo

echo "[1] Checking Nginx service..."
if systemctl is-active --quiet nginx; then
    echo "Nginx is running."
else
    echo "Nginx is NOT running. Starting it now..."
    sudo systemctl start nginx
fi
echo

echo "[2] Checking UFW firewall status..."
sudo ufw status
echo

echo "[3] Creating website backup..."
BACKUP_DIR="$HOME/backups"
mkdir -p "$BACKUP_DIR"
sudo tar -czf "$BACKUP_DIR/web_$(date +%F_%T).tar.gz" /var/www/html
sudo chown $USER:$USER $BACKUP_DIR/*
echo "Backup saved to: $BACKUP_DIR"
echo

echo "===== Script Completed Successfully ====="

### How to Run

chmod +x ~/scripts/server_check_and_backup.sh
~/scripts/server_check_and_backup.sh

***

## 9. Testing & Verification

* **✔ Website Test**
    * http://4.230.142.25 loads correctly
    * http://shavaiz.cloud loads correctly
* **✔ DNS Test**
    * ping shavaiz.cloud resolves to 4.230.142.25
* **✔ Firewall Test**
    * sudo ufw status shows allowed: OpenSSH, Nginx HTTP
* **✔ Script Test**
    * Running the script generates a backup in: /home/azureuser/backups/

All tests confirmed the server is functioning as expected.

***

## 10. Version Control (GitHub)

Repository structure:

ict171-cloud-server-project/
│
├── README.md
├── scripts/
│   └── server_check_and_backup.sh
├── docs/
│   └── screenshots (optional)
└── website/
    └── index.html

GitHub is used to store documentation, scripts, and evidence of deployment.

***

## 11. Video Demonstration

The video includes:

1. Azure Portal showing the running VM
2. SSH login
3. Installing and verifying Nginx
4. Firewall configuration
5. Live website demonstration (shavaiz.cloud)
6. Running the automation script
7. Backup verification

Video Link: (to be added)
