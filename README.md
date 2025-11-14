ICT171 Cloud Server Project

Student Name: Muhammad Shavaiz
Student ID: 35332358
Public IP Address: 4.230.142.25
Domain Name: shavaiz.cloud

1. Project Overview
This project demonstrates the deployment of a cloud-based web server using an IaaS model. A Linux VM was created on Microsoft Azure, Nginx was installed, a firewall was configured, a custom website was deployed, and a domain name was attached via DNS.

Technologies used:
- Microsoft Azure Virtual Machine (Ubuntu 22.04 LTS)
- SSH
- Nginx web server
- UFW firewall
- GoDaddy DNS
- Bash scripting
- GitHub version control

2. Architecture Overview
Client (Browser)
DNS: shavaiz.cloud → Public IP: 4.230.142.25
Azure Virtual Machine (Ubuntu 22.04)
Nginx Web Server
/var/www/html/index.html

Key components:
DNS, Azure VM, Firewall, Nginx, Automation Script.

3. Azure Virtual Machine Setup
VM Configuration:
Resource group: rg-ict171
VM name: ict171-vm
Image: Ubuntu Server 22.04 LTS
Size: Standard B1s
Ports: SSH (22), HTTP (80)

SSH Access:
ssh azureuser@4.230.142.25

4. Server Configuration
System Update:
sudo apt update && sudo apt upgrade -y
sudo apt install -y ufw git curl

Install Nginx:
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx

5. Firewall Configuration
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx HTTP'
sudo ufw --force enable
sudo ufw status

6. Website Deployment
Replace default page and create custom index.html.

7. DNS Configuration (GoDaddy)
A-Record:
@ → 4.230.142.25

CNAME:
www → shavaiz.cloud

8. Bash Script (Automation Component)

Path: scripts/server_check_and_backup.sh

Script:
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
echo "Backup saved."
echo "===== Script Completed Successfully ====="

9. Testing & Verification
- Website loads on IP and domain
- DNS resolves correctly
- Firewall rules correct
- Script generates backup files

10. Version Control (GitHub)
Repository includes README, script, website files, and screenshots folder.

11. Video Demonstration
Video shows:
Azure VM, SSH login, Nginx install, firewall, website, script execution, backup output.


