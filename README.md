


<h1 align="center">Internship Project Assignments & Implementations</h1>

<p align="center">
Cloud • DevOps • Kubernetes • Automation • Monitoring • Backup
</p>

---

## 📌 Overview

This repository contains practical solutions developed during internship projects.

The assignments focus on real-world cloud architecture, secure deployments, infrastructure automation, monitoring, containerization, and backup strategies.

---

## 📄 Project scenario

> To review detailed scenarios, challenges faced, and complete project explanations,  
> 👉 **[Click Here](https://github.com/nikiimisal/Internship--Project-s/blob/main/Internship_Project's.pdf)**

---

## 📂 Project Navigation

- 🚀 [Project 1 – Java Application Deployment with Reverse Proxy on AWS](./Project-1-Java-Deployment)
- 💾 [Project 2 – AWS Backup Plan for EC2 and RDS](./Project-2-AWS-Backup)
- 📊 [Project 3 – Data Ingestion (S3 → RDS → Glue Fallback) using Docker(Python Application)](./Project-3-S3-RDS-Glue)
- 📈 [Project 4 – Deploy Prometheus & Grafana using Terraform & Helm](./Project-4-Monitoring-Terraform)
- ☸️ [Project 5 – Deploying & Managing Microservices in Kubernetes](./Project-5-Kubernetes-Microservices)

---

## 🚀 Key Highlights

- Real-world problem statements  
- Secure cloud architecture design  
- Infrastructure as Code (Terraform)  
- Containerization & orchestration (Docker & Kubernetes)  
- Monitoring & observability setup  
- Backup and disaster recovery strategies  

---

## 🛠 Tools & Technologies

- AWS (EC2, RDS, S3, Glue, Backup)  
- Docker  
- Kubernetes  
- Terraform  
- Helm  
- Linux  

---


## 🔐 Architecture Focus

These implementations emphasize:

- Secure networking & access control  
- Scalable deployments  
- High availability concepts  
- Production-like environment setup  
- Automation and reliability engineering  

---

## 🌐 Connect with Me

<div align="center">

  <!-- 🌐 FIRST ROW -->
  <p>
    <a href="https://www.youtube.com/@nikhilmisal8027" target="_blank">
      <img src="https://img.shields.io/badge/YouTube-Subscribe-FF0000?style=for-the-badge&logo=youtube&logoColor=white&labelColor=0D1117&color=FF0000" alt="YouTube" />
    </a>
    <a href="https://www.linkedin.com/in/nikhilmisal/" target="_blank">
      <img src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0D1117&color=0077B5" alt="LinkedIn" />
    </a>&nbsp;
    <a href="https://github.com/nikiimisal" target="_blank">
      <img src="https://img.shields.io/badge/GitHub-Follow-333333?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117&color=6e40c9" alt="GitHub" />
    </a>&nbsp;
    <a href="https://www.leetcode.com/" target="_blank">
      <img src="https://img.shields.io/badge/LeetCode-Practice-FFA116?style=for-the-badge&logo=leetcode&logoColor=white&labelColor=0D1117&color=FCA311" alt="LeetCode" />
    </a>&nbsp;
    <a href="https://nikiimisal.github.io/Portfollio.in/" target="_blank">
      <img src="https://img.shields.io/badge/Portfolio-Explore-00C9FF?style=for-the-badge&logo=react&logoColor=61DAFB&labelColor=0D1117&color=92FE9D" alt="Portfolio" />
    </a>
  </p>

  <!-- ✨ SECOND ROW -->
  <p>
    <a href="https://medium.com/@nik0misal" target="_blank">
      <img src="https://img.shields.io/badge/Medium-Read-000000?style=for-the-badge&logo=medium&logoColor=white&labelColor=0D1117&color=6e40c9" alt="Medium" />
    </a>&nbsp;
    <a href="mailto:nik0misal@gmail.com">
      <img src="https://img.shields.io/badge/Email-Contact_Me-D14836?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0D1117&color=ff512f" alt="Email" />
    </a>&nbsp;
    <a href="https://x.com/nikiimisal" target="_blank">
      <img src="https://img.shields.io/badge/Twitter-Follow-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white&labelColor=0D1117&color=0f9b0f" alt="Twitter" />
    </a>
  </p>

</div>


---
---
---


#  🚀 Project: Java App Deployment with Reverse Proxy on AWS














# 🚀 STEP 1 – Launch EC2 Instances

## 1️⃣ Backend Server (Java + Tomcat)

**Name:** `backend-server`
**OS:** Amazon Linux 2  
**Instance Type:** t2.micro  
**Key Pair:** Create or select existing  

### 🔐 Security Group (Backend SG)

**Allow:**
- **SSH (22)** → Your IP
- **Custom TCP (8080)** → ONLY Proxy SG<br>
  >so that for create first `Proxy SG`

❌ **Do NOT allow 8080 to 0.0.0.0/0**


---

## 2️⃣ Reverse Proxy Server

Launch another EC2 instance

**Name:** `proxy-server`  
**OS:** Amazon Linux 2  

### 🔐 Security Group (`Proxy SG`)

**Allow:**
- **SSH (22)** → Your IP
- **HTTP (80)** → 0.0.0.0/0

---


# ✅ STEP 2 – Install Java & Tomcat (Backend EC2)

### 🔐 SSH into Backend EC2

```bash
sudo yum update -y
sudo yum install java-17-amazon-corretto -y
```

### 📦 Install Tomcat

```bash
sudo yum install tomcat -y
sudo systemctl start tomcat
sudo systemctl enable tomcat
```


## ❗ If Tomcat Installation Fails

If you get:

```
No match for argument: tomcat
```

Then install Tomcat manually:

```bash
cd /opt
# Change directory to /opt where we will install Tomcat

sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.85/bin/apache-tomcat-9.0.85.tar.gz
# Download Tomcat compressed file from Apache archive repository

sudo tar -xvzf apache-tomcat-9.0.85.tar.gz
# Extract the downloaded .tar.gz file
# x = extract
# v = verbose (shows progress)
# z = unzip (.gz format)
# f = file

sudo mv apache-tomcat-9.0.85 tomcat
# Rename the extracted folder to 'tomcat' for easier access

sudo chmod -R 755 /opt/tomcat
# Give read and execute permissions recursively to all Tomcat files

cd /opt/tomcat/bin
# Move to Tomcat bin directory where startup scripts are stored

sudo ./startup.sh
# Start the Tomcat server
# If successful, it will show "Tomcat started"
```

---

### 🔎 Verify Tomcat

in terminal:

```
curl http://localhost:8080
```

---

# ✅ STEP 3 – Deploy student.war

### 📂 Move to Tomcat Webapps Directory

```bash
cd /opt/tomcat/webapps/                      # we are using this path because we are download tomcat manually
sudo wget <student.war download link>
```
```
cd /usr/share/tomcat/webapps/                # if you are using yum store to install tomcat use this path
```

### 🔄 Restart Tomcat

#### 👉 If Tomcat installed manually:

```bash
cd /opt/tomcat/bin
sudo ./shutdown.sh
sudo ./startup.sh
```

#### 👉 If Tomcat installed via yum:

```bash
sudo systemctl restart tomcat
```

### 🔎 Verify Deployment (Internal Check)

```
curl http://localhost:8080/student/
```
If successful, you should see the **Student Registration Form HTML page**.

---

### 📁 Validate WAR Extraction (Optional)

```bash
cd /opt/tomcat/webapps/
ls
```

Expected Output:

```
student.war
student/
```

The presence of the `student/` directory confirms:

- WAR file extracted successfully  
- Application context is active  
- Deployment completed successfully  

---

# ✅ STEP 4 – Setup RDS MySQL

### 🗄️ Create Database

Go to:
AWS Console → RDS → Create Database

**creation method**:Easy create
**Engine:** MySQL  
**Template:** Free Tier  
**DB Name:** `studentdb` 
**Master Username:** `admin`
**Password:** `rootroot`  
**Public Access:** ❌ NO  
**VPC:** Same as EC2  

---

### 🔐 Security Group Configuration

**Allow:**
- **MySQL (3306)** → Backend EC2 Security Group Only  

❌ Do NOT allow 3306 to 0.0.0.0/0


---

# ✅ STEP 5 – Create Database & Table

### 🔗 Connect from Backend EC2

```bash
sudo yum install mysql -y
mysql -h <RDS-endpoint> -u admin -p
```

### 🗄️ Create Database

```sql
CREATE DATABASE studentdb;
USE studentdb;
```

### 📋 Create Table

```sql
CREATE TABLE students (
    id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100),
    course VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    address VARCHAR(255),
    age INT,
    qual VARCHAR(100),
    percent FLOAT,
    yop INT,
    PRIMARY KEY (id)
);
```

---

# ✅ STEP 6 – Add MySQL Connector

### 📦 Download MySQL Connector

```bash
cd /opt/tomcat/lib
sudo wget <mysql-connector.jar link>
```

### 🔄 Restart Tomcat

if you u install manually:
```bash
cd /opt/tomcat/bin
sudo ./shutdown.sh
sudo ./startup.sh
curl http://localhost:8080/student/
```


```bash
sudo systemctl restart tomcat
curl http://localhost:8080/student/
```


---


# ✅ STEP 7 – Configure Reverse Proxy (Nginx)

### 🔗 SSH into Proxy EC2

```bash
sudo yum install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

### ⚙️ Edit Nginx Configuration

```bash
sudo nano /etc/nginx/nginx.conf
```

Inside `server` block, add:

```nginx
 # Proxy for student app
    location /student/ {
        proxy_pass http://172.31.31.215:8080/student/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
```

### 🔄 Restart Nginx

```bash
sudo systemctl restart nginx
```

---

# ✅ STEP 8 – Block Direct Backend Access

**Backend Security Group:**

❌ Remove **8080** access from **0.0.0.0/0**  
✅ Allow **8080** only from **Proxy Security Group**

---

# ✅ STEP 9 – Final Access URL

Now access your application via:

```
http://<Proxy-Public-IP>/student
```

✔️ Works only through the proxy  
✔️ Backend remains private


---
---
---































