# ICT171 Cloud Server Project

**Student Name:** Muhammad Shavaiz  
**Student ID:** 35332358  

**Public IP Address:** `4.230.142.25`  
**Domain Name:** `shavaiz.cloud`  

---

## 1. Project Overview

This project demonstrates the deployment of a cloud-based web server using an Infrastructure as a Service (IaaS) model.  
I created a Linux virtual machine on Microsoft Azure, installed Nginx, configured a firewall, deployed a portfolio website, and attached a custom domain using DNS.

The server is publicly accessible via both its IP address and domain name.

**Technologies used:**

- Microsoft Azure Virtual Machine (Ubuntu 22.04 LTS)
- SSH remote administration
- Nginx web server
- UFW firewall
- DNS A-record
- Bash scripting
- GitHub version control

---

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


Key components:

- **DNS**: Domain → IP mapping using A-record  
- **Azure VM**: IaaS server running Ubuntu  
- **Firewall**: UFW + Azure Network Security Group  
- **Nginx**: Serves portfolio website  
- **Script**: Automated maintenance and backup  

---

## 3. Azure Virtual Machine Setup

### VM Configuration

- **Resource group:** rg-ict171  
- **VM name:** ict171-vm  
- **Region:** (closest Azure region)  
- **Image:** Ubuntu Server 22.04 LTS  
- **Size:** Standard B1s (1 vCPU, 1 GiB RAM)  
- **Authentication:** Password  
- **Username:** azureuser  
- **Inbound ports allowed:** SSH (22), HTTP (80)  

### SSH Access

```bash
ssh azureuser@4.230.142.25


---

## 4. Server Configuration

### 4.1 System Update

After accessing the VM via SSH, I updated the package list and installed required utilities:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y ufw git curl

sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx

systemctl status nginx

http://4.230.142.25

sudo ufw allow OpenSSH
sudo ufw allow 'Nginx HTTP'
sudo ufw --force enable
sudo ufw status

