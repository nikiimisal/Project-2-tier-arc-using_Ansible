# Two-Tier Architecture using Ansible

## 📌 Overview
This project demonstrates the implementation of a **Two-Tier Architecture** using **Ansible automation**.

It focuses on configuring and deploying **application and database servers** using a **single Ansible playbook**, following real-world DevOps practices.  
The project is beginner-friendly and suitable for interview preparation.

Key objectives of this project:
- Automate multi-host server configuration
- Use Ansible inventory for host management
- Deploy application and database services
- Understand real-world two-tier architecture

Ansible uses an **agentless architecture**, which means:
- No software installation is required on target servers
- Communication happens over SSH
- Infrastructure configuration is written in simple YAML files
  
 <p align="center">
  <img src="" width="500" alt="Initialize Repository Screenshot">
</p>

---

## 🏗 What is Two-Tier Architecture?

A Two-Tier Architecture divides an application into **two layers**:

### 1️⃣ Application Tier (App Server)
- Hosts application services
- Handles user requests
- Runs:
  - Nginx
  - PHP
  - PHP-FPM

### 2️⃣ Database Tier (DB Server)
- Stores application data
- Runs MariaDB
- Isolated from the application logic
  
This separation provides:
- 🔐 Better security
- ⚙ Easier management
- 📈 Scalability for future upgrades


### ✅ Benefits
- Improved security
- Better separation of concerns
- Easier management
- Scalable for future enhancements
  
---

## 🏛 Architecture Flow

```
Client (Browser)
        |
        v
App Server (Nginx + PHP)
        |
        v
Database Server (MariaDB)
```

---

## 📁 Infrastructure Provisioning (Terraform – Reference) ( Optional )

The EC2 instances used in this project were created via the **AWS Management Console**.  
However, for **best practices**, infrastructure should be provisioned using **Terraform**.

For reference, a Terraform-based two-tier architecture is documented here:  
👉 https://github.com/nikiimisal/Project-2-tier-arc-using_terraform

### Terraform Project Structure ( For - Creating 3 instances infracture )

```
2-tier-project/
├── main.tf        # Core infrastructure code
├── variables.tf   # Input variables
├── outputs.tf     # Output values
└── README.md      # Documentation
```

> ⚠️ Note: Terraform is **not mandatory** for this project.  
> Ansible is the **primary focus**.

---

## 📁 Ansible Project Structure

```
2-tier-ansible-project/
├── inventory.ini        # Target server IPs & SSH configuration
├── deploy.yml           # Single Ansible playbook
└── README.md            # Project documentation
```

---

## 📋 Inventory File (inventory.ini)

The inventory file defines target hosts and SSH access details.

```
[app-server]
172.31.46.159 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/server1.pem

[db-server]
172.31.42.122 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/server1.pem
```

## 📋 2-tier-arc.yml file

👉[Click here](https://github.com/nikiimisal/Project-2-tier-arc-using_Ansible/blob/main/2-tier-arc.yml)


---

## ⚙️ Ansible Playbook Explanation

### 🟡 Ansible Control Server
- Ansible is installed on the control node
- Uses SSH to connect to target servers
- No agent required on managed nodes
- Executes the playbook and manages automation
  
### 🟢 App Server Tasks
- Install Nginx, PHP, PHP-FPM
- Start & enable services
- Deploy PHP info page

### 🔵 Database Server Tasks
- Install MariaDB
- Start & enable database service
- Create database automatically

   <p align="center">
  <img src="" width="500" alt="Initialize Repository Screenshot">
</p>


---

## 🚀 How to Run the Project

- Upload the private key from your local machine to the Linux terminal to enable secure SSH access to remote servers.

   <p align="center">
  <img src="" width="500" alt="Initialize Repository Screenshot">
</p>

- Create 2 files `.ini` & `.yml`
- Then run this command's

```
ansible-playbook deploy.yml -i inventory.ini --syntax-check
```

```
ansible-playbook deploy.yml -i inventory.ini
```


| **Terminal**    | **Terminal**          |
|--------------------------------|------------------------------------|
| ![VS]() | ![AWS]() |

---

## 🌐 Verification

### App Server
Open browser and enter:
```
http://<app-server-public-ip>
```
You should see the **PHP Info Page**.

 <p align="center">
  <img src="" width="500" alt="Initialize Repository Screenshot">
</p>

### Database Server
```
mysql -u root
SHOW DATABASES;
```
 <p align="center">
  <img src="" width="500" alt="Initialize Repository Screenshot">
</p>

---

## 🎯 Key Ansible Concepts Used
- Inventory and host groups
- Variables
- Loops
- Ansible modules:
  - dnf
  - systemd
  - copy
  - shell
- Multi-play playbook structure
  
---

## 🧠 Simple Explanation
“This project demonstrates a two-tier architecture using Ansible where the application server and database server are configured separately using inventory groups and deployed using a single playbook.”

---

## 🔮 Future Enhancements
- Convert to Ansible Roles
- Secure DB with users/passwords
- Connect PHP app to DB
- Use templates & handlers
- Integrate with Terraform

---

## ✅ Conclusion
This project provides hands-on experience with:
- Ansible automation
- Multi-server deployment
- Real-world DevOps architecture

---

## 👨‍💻 Author
**Nikhil Misal**  
Building real-world DevOps automation using **Ansible & Terraform**
