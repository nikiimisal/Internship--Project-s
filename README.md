


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

### 🔗 Configure Database Connection (JNDI)

📍 Create directory (if not exists):
```Bash
mkdir -p /opt/tomcat/webapps/student/META-INF
```
📍 Create file:
```Bash
sudo nano /opt/tomcat/webapps/student/META-INF/context.xml
```
📄 Add configuration:
```XML
<Context>
    <Resource name="jdbc/TestDB"
              auth="Container"
              type="javax.sql.DataSource"
              username="admin"
              password="rootroot"
              driverClassName="com.mysql.jdbc.Driver"
              url="jdbc:mysql://<RDS-endpoint>:3306/studentdb"/>
</Context>
```

>👉 Replace <RDS-endpoint> with your actual RDS endpoint


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

<br>

## 📊 Summary Report

### 📸 Screenshot of Stored Registration Data

<img here>

###  Explanation of traffic flow: Proxy → Backend 

1. User sends request to Proxy Server (Nginx) via HTTP (port 80)
2. Nginx forwards the request to Backend Server (Tomcat) on port 8080
3. Tomcat processes the request and interacts with the application
4. Application connects to Amazon RDS (MySQL) using JNDI DataSource
5. Response flows back from Backend → Proxy → User

---

### Tools and Services Used

- AWS EC2 (Backend & Proxy servers)
- AWS RDS (MySQL Database)
- Apache Tomcat (Application Server)
- Nginx (Reverse Proxy)
- Java (JDK 17)
- MySQL Connector (JDBC Driver)
- Linux (Amazon Linux 2)

---

### Challenges Encountered and Troubleshooting

During deployment, the application UI was accessible, but form data was not being stored in the database.

#### Issue: Database Connection Failure

Initially, it was assumed that the database configuration was hardcoded in `.class` files using:

```
jdbc:mysql://localhost:3306/studentdb
```
However, after further debugging, it was found that the application was using a JNDI DataSource:
```
jdbc/TestDB
```
Since the required JNDI configuration was missing in Tomcat, the application was unable to connect to the Amazon RDS database.

As a result:
- Database connection failed  
- Form submissions were not saved  

---

#### Troubleshooting & Solution

- “The original student.war did not successfully connect to the database. To resolve this, the WAR file was extracted, necessary configuration changes were made (including database connection handling), and the application was repackaged and redeployed on Tomcat. This ensured successful communication with the Amazon RDS instance.”
  
Result:
- Application successfully connected to Amazon RDS  
- Form data stored correctly in the database  
- End-to-end functionality achieved  

Key Learning:
- Importance of identifying actual connection type (JDBC vs JNDI)  
- Compiled .class files cannot be modified directly  
- External configuration and WAR-level changes are essential in real-world deployments  



---
---
---




# 🚀 Project: AWS Backup Plan for EC2 and RDS

## 📌 Project Overview

This project demonstrates how to configure **automated backups and recovery** for AWS resources using **AWS Backup**.

The infrastructure includes:

- **Amazon EC2 instance** running a web server
- **Amazon RDS database** storing sample data
- **AWS Backup Plan** protecting both EC2 and RDS resources

The goal is to create a **centralized backup strategy** and validate backup jobs and recovery points.

---

# 🎯 Objective

- Launch an **EC2 instance** with a web server and sample data  
- Launch an **RDS database** with test records  
- Configure **AWS Backup Vault**  
- Create a **Backup Plan**  
- Assign **EC2 and RDS resources** to the backup plan  
- Trigger **on-demand backup**  
- Validate **backup jobs and recovery points**

---

# 🏗️ Architecture

```
EC2 Instance (Web Server)
        │
        │
   AWS Backup Plan
        │
        │
RDS Database (MySQL)
```

Both **EC2 and RDS resources** are protected using the **AWS Backup service**.

---

# 🛠️ Technologies Used

- **Amazon EC2**
- **Amazon RDS (MySQL)**
- **AWS Backup**
- **Nginx Web Server**
- **MySQL Client**
- **AWS Console**

---

# 🚀 STEP 1 – Launch EC2 Instance

Go to:

`AWS Console → EC2 → Launch Instance`

### Instance Configuration

| Setting | Value |
|------|------|
| Name | `backup-ec2` |
| AMI | `Amazon Linux 2` |
| Instance Type | `t2.micro` |
| Storage | `8GB` |
| Key Pair | `Create new or use existing` |

### Security Group

Allow:

- `SSH (22)` → **Your IP**
- `HTTP (80)` → **0.0.0.0/0**

Launch the instance.




<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20164323.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>




---

# 🔐 STEP 2 – Connect to EC2

SSH into the instance:

```bash
ssh -i key.pem ec2-user@<EC2-Public-IP>
```

---

# 🌐 STEP 3 – Install Web Server (Nginx)

Update system packages

```bash
sudo yum update -y
```

Install **Nginx**

```bash
sudo yum install nginx -y
```

Start Nginx

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

# 📄 STEP 4 – Create Sample Web Data

Navigate to web directory

```bash
cd /usr/share/nginx/html
```

Edit the web page

```bash
sudo nano index.html
```

Add sample content

```html
<h1>AWS Backup Project</h1>
<p>This data is stored on EC2 and will be protected by AWS Backup.</p>
```

---

# 🔎 Verify Web Server

Open in browser:

```
http://<EC2-Public-IP>
```

You should see the **sample web page**.


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20163734.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>



---

# 🗄️ STEP 5 – Launch RDS Database

Go to:

`AWS Console → RDS → Create Database`

### Database Configuration

| Setting | Value |
|------|------|
| Engine | `MySQL` |
| Template | `Dev/Test` |
|Availability and durability|  `Multi-AZ DB (2 instances)` |
| DB Instance Identifier | `backup-db` |
| Master Username | `admin` |
| Password | `rootroot` |
| Instance Class | `db.t3.micro` |
| Storage | `20GB` |
| Public Access | `Yes` |

>Public Access `yes` only for this project. In development environments, public access is usually set to `No`.

Click **Create Database**.

Wait until status becomes **Available**.


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215036.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

# 🔗 STEP 6 – Connect to RDS from EC2

Install MySQL client

```bash
sudo yum install mariadb105 -y
```

Connect to database

```bash
mysql -h <RDS-ENDPOINT> -u admin -p
```

---

# 🗃️ STEP 7 – Create Test Database and Table

Create database

```sql
CREATE DATABASE backupdb;
USE backupdb;
```

Create table

```sql
CREATE TABLE users (
id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(50),
email VARCHAR(100)
);
```

Insert sample data

```sql
INSERT INTO users (name,email)
VALUES ('Nikhil','nikhil@test.com');
```

Verify records

```sql
SELECT * FROM users;
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215147.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>




---

# 💾 STEP 8 – Open AWS Backup Service

Navigate to:

`AWS Console → AWS Backup`

---

# 🗄️ STEP 9 – Create Backup Vault

Go to:

`Backup Vaults → Create Backup Vault`

Configuration:

| Setting | Value |
|------|------|
| Vault Name | `ProjectBackupVault` |
| Encryption | `Default` |

Click **Create Backup Vault**.



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215314.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>




---

# 📋 STEP 10 – Create Backup Plan

Go to:

`Backup Plans → Create Backup Plan`

Choose:

`Build a new plan`

### Backup Rule Configuration

| Setting | Value |
|------|------|
| Plan Name | `EC2-RDS-BackupPlan` |
| Rule Name | `DailyBackup` |
| Backup Vault | `ProjectBackupVault` |
| Backup Frequency | `Daily` |
| Start Window | `60 Minutes` |
| Completion Window | `180 Minutes` |
| Retention Period | `7 Days` |

Click **Create Plan**.




<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215353.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>






---

# 🔗 STEP 11 – Assign Resources to Backup Plan

Click:

- `EC2-RDS-BackupPlan` ==> Scroll Down ==> click the checkbox `Resource assignments` ==> and then click `Assign Resources`

Configuration:

| Setting            | Value                           |
| ------------------ | ------------------------------- |
| Assignment Name    | EC2-RDS-BackupPlan              |
| IAM Role           | Default role                    |
| Resource Selection | Include specific resource types |
| Resources Selected | EC2 Instance, RDS Database      |




Click **Assign Resources**.





<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215609.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>






---

# ▶️ STEP 12 – Trigger On-Demand Backup

Go to:

`AWS Backup → Protected Resources`

Select resource and click:

`Create On-demand Backup`

Configuration:



| Setting | Value |
|------|------|
| Resource type | `EC2` , `RDS` |
| Select EC2-instance id | `backup-ec2` `backup-db` | 
| Backup window |  `Create Backup Now` |
| retention period | `7-Days` |
| Backup vault | `ProjectBackupVault` |
| IAM Role | `Default Role` |


Click **Create Backup**.

> Make shure After completing the backup for EC2, repeat the same steps for the RDS database as well


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215707.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>





---

# ✅ STEP 13 – Validate Backup Jobs

Go to:

`AWS Backup → Backup Jobs`

Check:

```
Status = Completed
```



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215735.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>




---

# 🚀 STEP 14 – Verify Recovery Points

If you want to verify whether the **backup has been successfully created**, you can view the **Recovery Points** stored inside the Backup Vault.

Go to:

`AWS Console → AWS Backup → Backup Vaults`

Open the vault created earlier:

`ProjectBackupVault`

Inside the vault you will see **Recovery Points**.

Recovery points represent the **stored backups of AWS resources**.

You should see recovery points for:

- **EC2 Instance**
- **RDS Database**

Click on a recovery point to view details such as:

| Detail | Description |
|------|------|
| Resource ID | EC2 Instance ID or RDS DB Identifier |
| Resource Type | EC2 / RDS |
| Backup Vault | ProjectBackupVault |
| Backup Creation Time | Time when backup was created |
| Status | Completed |

This confirms that the **backup was successfully created and stored in the backup vault**.



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20220044.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>





---

# ♻️ STEP 15 – Restore Backup and Verify Original Data

AWS Backup does **not allow direct viewing of raw data** inside a backup.

To view the **original stored data** (for example: `name`, `email`), you must **restore the resource from the backup**.

---

## 🔁 Restore RDS Database from Backup

Go to:

`AWS Console → AWS Backup → Backup Vaults → ProjectBackupVault`

Steps:

1. Open **Recovery Points**
2. Select the **RDS Database recovery point**
3. Click **Restore**

### Restore Configuration

| Setting | Value |
|------|------|
| Restore Type | Restore as new DB |
| DB Identifier | `backup-db-restore` |
| Instance Class | Same as original |
| VPC & Subnet | Same as original |
| Public Access | Yes |

Click **Restore**.

Wait until the database status becomes **Available**.

---

## 🔗 Connect to Restored RDS Database

Connect from EC2:

```bash
mysql -h <RESTORED-RDS-ENDPOINT> -u admin -p
```
Verify the database records:
```SQL
USE backupdb;
SELECT * FROM users;
```
You should see the original stored data:
```
+----+--------+------------------+
| id | name   | email            |
+----+--------+------------------+
|  1 | Nikhil | nikhil@test.com  |
+----+--------+------------------+
```
📸 Take a screenshot of the restored database output.

---

## 🖥️ (Optional) Restore EC2 Instance from Backup

You can also restore the **EC2 instance** from the backup.

Go to:

`AWS Backup → Backup Vaults → ProjectBackupVault`

### Steps

1. Select the **EC2 recovery point**
2. Click **Restore**
3. Restore as a **New EC2 Instance**

After the instance is launched, verify the stored web data:

```bash
cat /usr/share/nginx/html/index.html
```
You should see the same HTML content that was stored earlier.

📌 Important Note

>AWS Backup stores data in an encrypted backup format.
>The raw data cannot be viewed directly from the backup vault.
>To access the original data, the resource must be restored from a recovery point.

---
---

**📌 Second Important Note:**

After completing the project, make sure to delete all the AWS resources that were created (such as EC2 instances, RDS databases, backup plans, and backup vaults). If these resources are left running, AWS may continue to charge for their usage.




---
---

# ⚠️ Issues Faced

Possible issues during implementation:

- RDS connection failure due to **security group configuration**
- Backup job delay during first execution
- IAM role permission issues

These were resolved by verifying **security groups**, **RDS endpoint**, and **IAM permissions**.

---

# 📌 Conclusion

This project demonstrates how to implement a **centralized backup solution using AWS Backup** to protect AWS resources such as **EC2 instances and RDS databases**.

Automated backups ensure **data protection**, **disaster recovery**, and **high availability**.

---

# 👨‍💻 Author

**Nikhil Misal**

AWS Cloud Project



---
---
---




























