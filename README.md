# Two-Tier Architecture using Ansible

## 📌 Overview
This project implements a **Two-Tier Architecture** using **Ansible automation**.
It demonstrates how to configure and deploy **application and database servers** using a **single Ansible playbook**.

The project is beginner-friendly and interview-oriented, focusing on:
- Multi-host automation
- Inventory management
- Service deployment
- Real-world 2-tier architecture concept

Ansible enables **agentless automation**, meaning:
- No software required on target servers
- Uses SSH for communication
- Simple YAML-based configuration

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

## 📁 Project Structure

```
2-tier-ansible-project/
├── inventory.ini        # Target server IPs & SSH details
├── deploy.yml           # Single Ansible playbook
└── README.md            # Project documentation
```

---

## 📋 Inventory File (inventory.ini)

```
[app-server]
172.31.46.159 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/server1.pem

[db-server]
172.31.42.122 ansible_user=ec2-user ansible_ssh_private_key_file=/home/ec2-user/server1.pem
```

## 📋 2-tier-arc.yml file

```

# deployment of 2-tier app using single ansible script
---
# appserver
- name: installation of appserver
  hosts: app-server
  become: yes
  vars:
   packages:
    - nginx
    - php
    - php-fpm
   services:
    - nginx
    - php-fpm
   web_file_path: /usr/share/nginx/html/index.php
  tasks:
  # install nginx, php
  - name: install nginx, php, php-fpm
    ansible.builtin.dnf:
      name: "{{packages}}"
      state: present
  # start and enable nginx, php
  - name: start and enable nginx, php-fpm
    ansible.builtin.systemd_service:
      name: "{{item}}"
      state: started
      enabled: true
    loop: "{{services}}"
  # deployment of php page
  - name: deploy php on nginx
    ansible.builtin.copy:
      dest: "{{web_file_path}}"
      content: |
       <?php
       phpinfo();
       ?>
#dbserver
- name: installation on dbserver
  hosts: db-server
  become: yes
  vars:
   db_pkg: mariadb105-server
   db_service: mariadb
   db_name: FCT
  tasks:
  # install mariadb
  - name: install mariadb
    ansible.builtin.dnf:
      name: "{{db_pkg}}"
      state: present
  # start mariadb
  - name: start and enable maraidb
    ansible.builtin.systemd_service:
      name: "{{db_service}}"
      state: started
      enabled: true
  # create databse
  - name: create a  mysql database
    ansible.builtin.shell: |
      mysql -u root -e "CREATE DATABASE IF NOT EXISTS {{ db_name }};"
     


```
---

## ⚙️ Ansible Playbook Explanation

### 🟢 App Server Tasks
- Install Nginx, PHP, PHP-FPM
- Start & enable services
- Deploy PHP info page

### 🔵 Database Server Tasks
- Install MariaDB
- Start & enable database service
- Create database automatically

---

## 🚀 How to Run the Project

```
ansible-playbook -i inventory.ini deploy.yml
```

---

## 🌐 Verification

### App Server
Open browser and enter:
```
http://<app-server-public-ip>
```
You should see the **PHP Info Page**.

### Database Server
```
mysql -u root
SHOW DATABASES;
```

---

## 🎯 Key Ansible Concepts Used
- Inventory & host groups
- Variables
- Loops
- Modules (dnf, systemd, copy, shell)
- Multi-play playbook

---

## 🧠 Simple Interview Explanation
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
