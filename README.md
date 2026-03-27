


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

- 🚀 [Project 1 – Java Application Deployment with Reverse Proxy on AWS](#example-0)
- 💾 [Project 2 – AWS Backup Plan for EC2 and RDS](#example-1)
- 📊 [Project 3 – Data Ingestion (S3 → RDS → Glue Fallback) using Docker(Python Application)](#example-2)
- 📈 [Project 4 – Deploy Prometheus & Grafana using Terraform & Helm](#example-3)
- ☸️ [Project 5 – Deploying & Managing Microservices in Kubernetes](#example-4)

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

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


---


<a id="example-0"></a>


#  🚀 Project 1: Java App Deployment with Reverse Proxy on AWS

---

<br>
<br>



## 🚀 STEP 1 – Launch EC2 Instances

### 1️⃣ Backend Server (Java + Tomcat)

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

### 2️⃣ Reverse Proxy Server

Launch another EC2 instance

**Name:** `proxy-server`  
**OS:** Amazon Linux 2  

### 🔐 Security Group (`Proxy SG`)

**Allow:**
- **SSH (22)** → Your IP
- **HTTP (80)** → 0.0.0.0/0



| **Instance's**    | **Security Group**          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-03%20155508.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-03%20155358.png?raw=true) |


---


## ✅ STEP 2 – Install Java & Tomcat (Backend EC2)

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


### ❗ If Tomcat Installation Fails

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

## ✅ STEP 3 – Deploy student.war

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

## ✅ STEP 4 – Setup RDS MySQL

### 🗄️ Create Database

Go to:
AWS Console → RDS → Create Database

**creation method**:Easy create
**Engine:** MySQL  
**Template:** Free Tier  
**DB Name:** `root` 
**Master Username:** `admin`
**Password:** `rootroot`  
**Public Access:** ❌ NO  
**VPC:** Same as EC2  

---

### 🔐 Security Group Configuration

**Allow:**
- **MySQL (3306)** → Backend EC2 Security Group Only  

❌ Do NOT allow 3306 to 0.0.0.0/0



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-21%20102202.png?raw=true" width="800" alt="Initialize Repository Screenshot">
</p>



---

## ✅ STEP 5 – Create Database & Table

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

## ✅ STEP 6 – Add MySQL Connector

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


## ✅ STEP 7 – Configure Reverse Proxy (Nginx)

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

## ✅ STEP 8 – Block Direct Backend Access

**Backend Security Group:**

❌ Remove **8080** access from **0.0.0.0/0**  
✅ Allow **8080** only from **Proxy Security Group**

---

## ✅ STEP 9 – Final Access URL

Now access your application via:

```
http://<Proxy-Public-IP>/student
```

✔️ Works only through the proxy  
✔️ Backend remains private


| **Browser**    | ****          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-21%20073403.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-21%20110355.png?raw=true) |



### 📸 Screenshot of Stored Registration Data


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-1/Screenshot%202026-03-21%20110135.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---

<br>

## 📊 Summary Report



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


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


---

<a id="example-1"></a>

# 🚀 Project 2: AWS Backup Plan for EC2 and RDS

---

<br>
<br>



## 📌 Project Overview

This project demonstrates how to configure **automated backups and recovery** for AWS resources using **AWS Backup**.

The infrastructure includes:

- **Amazon EC2 instance** running a web server
- **Amazon RDS database** storing sample data
- **AWS Backup Plan** protecting both EC2 and RDS resources

The goal is to create a **centralized backup strategy** and validate backup jobs and recovery points.

---

### 🎯 Objective

- Launch an **EC2 instance** with a web server and sample data  
- Launch an **RDS database** with test records  
- Configure **AWS Backup Vault**  
- Create a **Backup Plan**  
- Assign **EC2 and RDS resources** to the backup plan  
- Trigger **on-demand backup**  
- Validate **backup jobs and recovery points**

---

### 🏗️ Architecture

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

### 🛠️ Technologies Used

- **Amazon EC2**
- **Amazon RDS (MySQL)**
- **AWS Backup**
- **Nginx Web Server**
- **MySQL Client**
- **AWS Console**

---

<br>


## 🚀 STEP 1 – Launch EC2 Instance

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20164323.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

## 🔐 STEP 2 – Connect to EC2

SSH into the instance:

```bash
ssh -i key.pem ec2-user@<EC2-Public-IP>
```

---

## 🌐 STEP 3 – Install Web Server (Nginx)

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

## 📄 STEP 4 – Create Sample Web Data

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

## 🔎 Verify Web Server

Open in browser:

```
http://<EC2-Public-IP>
```

You should see the **sample web page**.


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20163734.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---

## 🗄️ STEP 5 – Launch RDS Database

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215036.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---

## 🔗 STEP 6 – Connect to RDS from EC2

Install MySQL client

```bash
sudo yum install mariadb105 -y
```

Connect to database

```bash
mysql -h <RDS-ENDPOINT> -u admin -p
```

---

## 🗃️ STEP 7 – Create Test Database and Table

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215147.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

## 💾 STEP 8 – Open AWS Backup Service

Navigate to:

`AWS Console → AWS Backup`

---

## 🗄️ STEP 9 – Create Backup Vault

Go to:

`Backup Vaults → Create Backup Vault`

Configuration:

| Setting | Value |
|------|------|
| Vault Name | `ProjectBackupVault` |
| Encryption | `Default` |

Click **Create Backup Vault**.



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215314.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

## 📋 STEP 10 – Create Backup Plan

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215353.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>






---

## 🔗 STEP 11 – Assign Resources to Backup Plan

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215609.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>






---

## ▶️ STEP 12 – Trigger On-Demand Backup

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
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215707.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>





---

## ✅ STEP 13 – Validate Backup Jobs

Go to:

`AWS Backup → Backup Jobs`

Check:

```
Status = Completed
```



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20215735.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

## 🚀 STEP 14 – Verify Recovery Points

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
<img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-2/Screenshot%202026-03-09%20220044.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>





---

## ♻️ STEP 15 – Restore Backup and Verify Original Data

AWS Backup does **not allow direct viewing of raw data** inside a backup.

To view the **original stored data** (for example: `name`, `email`), you must **restore the resource from the backup**.

---

### 🔁 Restore RDS Database from Backup

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

### 🔗 Connect to Restored RDS Database

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

### 🖥️ (Optional) Restore EC2 Instance from Backup

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

## ⚠️ Issues Faced

Possible issues during implementation:

- RDS connection failure due to **security group configuration**
- Backup job delay during first execution
- IAM role permission issues

These were resolved by verifying **security groups**, **RDS endpoint**, and **IAM permissions**.

---

## 📌 Conclusion

This project demonstrates how to implement a **centralized backup solution using AWS Backup** to protect AWS resources such as **EC2 instances and RDS databases**.

Automated backups ensure **data protection**, **disaster recovery**, and **high availability**.

---

## 👨‍💻 Author

**Nikhil Misal**

AWS Cloud Project



---
---
---



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>



---

<a id="example-2"></a>


# 🚀 Project 3: Data Ingestion from S3 to RDS with Glue Fallback

---

<br>
<br>

## 📌 Objective

Develop a Dockerized Python application that automates the process of:

- Reading data from an Amazon S3 bucket  
- Pushing it to an RDS (MySQL-compatible) database  
- Automatically falling back to AWS Glue if the RDS database is unavailable or the push operation fails  

This project helps integrate multiple AWS services (S3, RDS, Glue), work with data pipelines, and use Docker for packaging and deployment.

---

## 🏗️ Architecture

```
Normal Flow:
S3 → Python → RDS ✅

Failure Flow:
S3 → Python → ❌ RDS → ✅ Glue
```

👉 This is a real-world fault-tolerant pipeline 🔥

---


<br>



## 📁 Step 1: Prepare Project Files

Create a folder and inside it create:

```
project-folder/
│── data.csv    # Sample dataset
│── app.py      # Python script (S3 → RDS → Glue fallback)
│── Dockerfile
│── requirements.txt
│── .env
```

[click to see file's](https://github.com/nikiimisal/Internship__Project__3__-Raw-material/tree/main) 

You can:
- Create files directly in terminal  
- OR clone a repo and edit  
- OR create locally and upload to EC2  

>I have created this files in directly in terminal


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20221106.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---

## 🔐 Step 2: IAM User (Permission System)

Go to → ***AWS** → **IAM** → **Users** → **Create User**

Configuration Fill:
- Name: `project-user`
- Enable: ✅ Programmatic access  

Attach Permissions:
- `AmazonS3FullAccess`  
- `AmazonRDSFullAccess`  
- `AWSGlueConsoleFullAccess`

Go to Security Credentials → Access Keys → Create  

Save:

```
AWS_ACCESS_KEY_ID=XXXX
AWS_SECRET_ACCESS_KEY=XXXX
```

👉 These will be used inside Docker


| **IAM-Role**    | **Access keys**          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20222054.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20221928.png?raw=true) |



---

## ☁️ Step 3: Set up Amazon S3

1. Open AWS Console → S3  
2. Create bucket (e.g., `my-data-bucket-277`)  
3. Upload `data.csv`  
4. Note the bucket name and object key (`data.csv`) for environment variables.



| **Bucket**    | **Object**          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-21%20175357.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-21%20175405.png?raw=true) |


  
---

## 🗄️ Step 4: Set up Amazon RDS (MySQL)

Go to AWS Console → RDS → Create database

Select:
- Engine: MySQL  
- Version: 8.0  
- Free tier  

Configure:
- DB Identifier: `my-rds`  
- Database Name: `mydb`  
- Username: `admin`  
- Password: `password123`  
- Public access: Enabled  

Note the endpoint:
```
my-rds.xxxxx.region.rds.amazonaws.com
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20222309.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---

## 🧾 Step 4a: Create Table in RDS

```SQL
CREATE DATABASE mydb;

USE mydb;

CREATE TABLE mytable (
id INT PRIMARY KEY,
name VARCHAR(100),
age INT,
city VARCHAR(100)
);
```
>For this, we’ll need to launch a server instance — we can do that later.

---

## 🧠 Step 5: Set up AWS Glue (Fallback)

Go to AWS Glue → Data Catalog

- Create database: `fallback_db`  
- Do NOT create tables manually  

👉 Python script will create tables automatically if RDS fails.



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20115306.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---

## 💻 Step 6: Launch EC2 Instance

Go to EC2 → Launch Instance

- Amazon Linux 2 / 2023  
- Instance type: `t2.micro `

Enable:
- SSH (port 22)  

Download `.pem` key

Connect:
```Bash
ssh -i "your-key.pem" ec2-user@your-ec2-ip
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20221543.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>


---

## 🐳 Step 7: Install Docker

```Bash
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
```

Reconnect SSH so the user is added to the Docker group.

---

## 🏗️ Step 8: Build Docker Image

```Bash
docker build -t s3-rds-glue-app .
```
This creates a Docker image with your Python script and dependencies.

---

## ▶️ Step 9: Run Docker Container

```Bash
docker run --env-file .env s3-rds-glue-app
```

---

## ⚙️ Expected Behavior

- Reads CSV from S3  
- Uploads to RDS  

### If RDS works:
- Data inserted successfully
- To see inserted data for that see step 10


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20132428.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>

---

### If RDS fails:
- Error occurs  
- Glue fallback triggered  
- Table created in Glue
- For that see  step 11

---

## 🔍 Step 10: Verification

### Check RDS:

```Bash
SELECT * FROM mytable;
```


---


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20132504.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>

---

### Check Glue:

- Go to Glue → Tables → `my_glue_table`  
- Columns match CSV  

### Optional (Athena):

```SQL
SELECT * FROM my_glue_table;
```


---

## 🧪 Step 11: Test Glue Fallback (Optional)

Edit `.env`:

```
RDS_PASS=wrongpassword
```

Run again:

```Bash
docker run --env-file .env s3-rds-glue-app
```

Output:

```
📤 Uploading data to RDS...
❌ RDS upload failed
⚠️ Falling back to Glue...
✅ Glue table created successfully
```



---


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20132531.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---
Verify Glue table:

Go to Glue → Tables → my_glue_table

Columns reflect CSV headers: id, name, age, city

✅ This step confirms the fallback mechanism works.


---

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-3/Screenshot%202026-03-22%20121556.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>

---

## 📜 Step 12: Docker Logs

```Bash
docker ps                      # find running container
docker logs <container_id>
```
Logs will show:

- RDS success OR
- Glue fallback triggered

---



## 🧹 Step 13: Cleanup

```
docker stop <container_id>
```

---




# 📄 Summary Report: Data Ingestion Pipeline (S3 → RDS → Glue Fallback)

## 1. Repository
Python script and Dockerfile are stored in GitHub:  
[Click here](https://github.com/nikiimisal/Internship__Project__3__-Raw-material)

## 2. Data Flow
Fault-tolerant pipeline: reads CSV from **S3**, inserts into **RDS MySQL**, falls back to **AWS Glue** if RDS fails.

- **Normal Flow:** S3 → Python → RDS ✅  
- **Failure Flow:** S3 → Python → ❌ RDS → AWS Glue ✅  

**Implementation:** pandas parses CSV, SQLAlchemy + PyMySQL inserts into RDS, boto3 triggers Glue fallback.

---

## 3. AWS Services Used
- **S3:** Stores raw CSV files  
- **RDS (MySQL):** Main database  
- **Glue:** Fallback table creation  
- **IAM:** Permissions & credentials  
- **EC2:** Hosts Docker container

---

## 4. Docker Setup
- **Base Image:** Python 3.9  
- **Dependencies:** boto3, pandas, sqlalchemy, pymysql  
- **Execution:** Script runs automatically on container start  
- **Env Variables:** `.env` file contains AWS credentials, S3 & RDS info  

**Commands:**
```
docker build -t s3-rds-glue-app .
docker run --env-file .env s3-rds-glue-app
```

---

## 5. Challenges & Solutions
| Challenge                     | Solution |
|--------------------------------|---------|
| RDS connection failure         | Fallback to Glue using try-except |
| Dependency management          | Docker + requirements.txt ensures consistency |
| AWS permissions                | IAM user with proper access (S3, RDS, Glue) |
| Testing fallback               | Intentionally wrong RDS password to trigger Glue |

---

## ✅ Conclusion
This project implements a **scalable, fault-tolerant data pipeline** using **AWS services and Docker**, ensuring reliable data ingestion and automatic fallback handling.

---
---
---





<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>




---


<a id="example-3"></a>


# Project 4: Deploy Prometheus and Grafana on Kubernetes Cluster using Terraform & Helm 

---


<br>
<br>



## 📌 PROJECT OVERVIEW

This project deploys a complete monitoring stack using Prometheus and Grafana on an AWS EC2 Ubuntu instance with Kubernetes. Deployment is automated using Terraform and Helm, making it reproducible and easy to manage.

---

## 🔹 OBJECTIVES

- ☸️ **Set up Kubernetes with containerd on EC2**
- 📊 **Deploy Prometheus** for metrics collection
- 📈 **Deploy Grafana** for dashboards
- ⚡ **Automate deployments** with Terraform + Helm
- 🌐 **Access dashboards via browser:**
  - Prometheus → `http://<EC2-Public-IP>:9090`
  - Grafana → `http://<EC2-Public-IP>:3000`
    
---

   
 
  >I used this way for problem-solving or say project deployment, but you can use other methods if you prefer.


---

##  🔹 Architecture

```
EC2 (Ubuntu)
   └── containerd
        └── Kubernetes Cluster
             ├── Prometheus (Monitoring & Metrics)
             └── Grafana (Dashboard & Visualization)
```

---

    
## PROJECT STRUCTURE

Create a folder `monitoring-project`:

```
monitoring-project/
├── provider.tf
├── namespace.tf
├── prometheus.tf
├── grafana.tf
├── variables.tf
├── outputs.tf
```


---


<br>



## 🔹 STEP 0: PREREQUISITES

Make sure your environment has:

- Terraform installed → `terraform -v` 
- kubectl installed & configured → `kubectl get nodes` 
- Helm installed → `helm version` 
- A Kubernetes cluster ready (your EC2 node as a single-node cluster is fine)
- Enough RAM (at least 4GB) for Prometheus 📊 + Grafana 📈

---





## 🔹 STEP 1: LAUNCH EC2 INSTANCE

AWS → EC2 → Launch

- **Name:** `monitoring-server`
- **AMI:** `Ubuntu 22.04`
- **Instance Type:** `t3.medium` (minimum) / `t3.large` (recommended)
- **Key Pair:** `.pem`
- **Security Group:**
  - `22 → SSH`
  - `3000 → Grafana` 
  - `9090 → Prometheus` 
  - `6443 → Kubernetes API` 

> In this project, we are not launching separate servers for the master and worker nodes. Both the control plane (master) and worker components run on the same server.



| **Instance**    | **Security Group**          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20071954.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-23%20102707.png?raw=true) |

---

## 🔹 STEP 2: Connect to EC2

Use SSH to connect to your instance:

```bash
ssh -i your-key.pem ubuntu@<EC2-Public-IP>
```

---

##  🔹 STEP 3: Create Kubernetes Setup Script

Create a script file for Kubernetes setup:

```
sudo nano k8s-common.sh
```
- IF you using ubuntu : [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material/blob/main/k8s-common.sh)
- Or For Amazon : [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material/blob/main/k8s-common.sh%20%20(1))


>We are using Ubuntu, so commands are Ubuntu-specific. For Amazon Linux, some commands may differ.
>Make sure the OS supports a command before running it.

---

##  🔹 STEP 4: Run Setup Script

```
sudo chmod +x k8s-common.sh
sudo ./k8s-common.sh
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20090606.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


---

##  🔹 STEP 5: Initialize Kubernetes

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20090637.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---

##  🔹 STEP 6: Configure kubectl

```Bash
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown ubuntu:ubuntu $HOME/.kube/config
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20090808.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---


## 🔹 STEP 7: Install Network Plugin (Flannel)

```Bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```



---

##  🔹 STEP 8: Allow Pods on Master

```Bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```

---

##  🔹 STEP 9: Verify Cluster

```
kubectl get nodes
```
STATUS should be: Ready ✔

---

##  🔹 STEP 10: Install Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20090843.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---

##  🔹 STEP 11: Install Terraform

```Bash
sudo apt install -y gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform -y
```



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20091015.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

##  🔹 STEP 12: Create Project Folder

```
mkdir monitoring-project
cd monitoring-project
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20091212.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

##  🔹 STEP 13: Create Terraform Files

```Bash
touch provider.tf namespace.tf prometheus.tf grafana.tf variables.tf outputs.tf
```
Paste your prepared Terraform + Helm code into these files.

>To see files [click here](https://github.com/nikiimisal/Internship__Project-4__Raw-material)

---

##  🔹 STEP 14: Run Terraform

```Bash
terraform init
terraform plan   # if you wan see your plane
terraform apply --auto-approve
```

- Terraform will deploy:

  - Monitoring namespace
  - Prometheus
  - Grafana

---

##   🔹 STEP 15: Verify Pods

```Bash
kubectl get pods -n monitoring
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20082842.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>





---

##  🔹 STEP 16: Access Prometheus


```Bash
kubectl port-forward svc/prometheus-server 9090:80 -n monitoring --address 0.0.0.0
```

If you want to run it on the backend, use this command.
```Bash
nohup kubectl port-forward svc/prometheus-server 9090:80 -n monitoring --address 0.0.0.0 > prometheus_pf.log 2>&1 &
```
If you want to stop a background process:
```Bash
pkill -f "port-forward"          # finds and stops any running process whose full command contains "port-forward
```
```Bash
ps -ef | grep kubectl       #   -> verify 
ps aux                      #  → to list all running processes
kill <PID>                  #   → to stop a process using its Process ID
kill -9 <PID>               #   → to forcefully stop a process
pkill <process_name>        #   → to stop a process by its name
```
Open browser:

```
http://<EC2-Public-IP>:9090
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20091418.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20074539.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---

##  🔹 STEP 17: Access Grafana

```
kubectl port-forward svc/grafana 3000:80 -n monitoring --address 0.0.0.0
```

If you want to run it on the backend, use this command.
```Bash
nohup kubectl port-forward svc/grafana 3000:80 -n monitoring --address 0.0.0.0 > grafana_pf.log 2>&1 &
```

If you want to stop a background process:
```Bash
pkill -f "port-forward"          # finds and stops any running process whose full command contains "port-forward
```

Open browser:
```
http://<EC2-Public-IP>:3000
```



<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20091443.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



| **Browser**    | ****          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20080743.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20080820.png?raw=true) |



| **Browser**    | ****          |
|--------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20081659.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20082540.png?raw=true) |



---

##  🔹 STEP 18: Get Grafana Password

```Bash
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode
```

Username: `admin`<br>
Password: output of the above command


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-4/Screenshot%202026-03-24%20091545.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



---


##  ✅ FINAL FLOW

```
EC2 → containerd → kubeadm → Kubernetes → Helm → Terraform → Prometheus → Grafana
```

---
---

## 📝 SHORT REPORT

### Infrastructure Components Used
- **EC2:** Ubuntu 22.04 
- **Kubernetes Cluster:** kubeadm
- **Container Runtime:** containerd
- **Deployment Automation:** Helm & Terraform
- **Monitoring Stack:** Prometheus 📊 + Grafana 📈

---


- **Steps to deploy and connect the monitoring stack:**
  
1. Launch EC2 instance and configure Security Group
2. Connect via SSH
3. Run the Kubernetes setup script (`k8s-common.sh`)
4. Initialize Kubernetes cluster (`kubeadm init`)
5. Configure kubectl
6. Install network plugin (Flannel) and allow pods on master
7. Install Helm and Terraform
8. Create project folder and Terraform files
9. Deploy Prometheus and Grafana via Terraform
10. Access Prometheus (`http://<EC2-Public-IP>:9090`) and Grafana (`http://<EC2-Public-IP>:3000`)

---

- **Benefits of using Terraform and Helm together:**
  
  - Automates deployment of Kubernetes resources
  - Ensures **repeatable, consistent environments**
  - Simplifies management of Helm charts with **version control**
  - Reduces manual errors during updates or redeployments


---
---
---



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>




---



<a id="example-4"></a>


# 🚀 Project 5: Deploying Microservices in a Cloud-Native Environment

---


<br>
<br>



## 📌 Objective

This project demonstrates how to:

* Containerize microservices using Docker
* Deploy them on a Kubernetes cluster
* Implement service discovery and load balancing
* Enable auto-scaling using HPA
* Use persistent storage with PV and PVC
* Simulate a production-like cloud-native deployment

---

## 🏗️ Architecture

### Flow:

Client → Kubernetes Service → Microservices → Persistent Storage

### Internal Communication:

* user-service ↔ product-service ↔ order-service

### Kubernetes Handles:

* Pod management
* Networking
* Load balancing
* Scaling

---

## 📁 Project Structure

```
project/
│
├── user/
│   ├── app.py
│   ├── Dockerfile
│
├── product/
│   ├── app.py
│   ├── Dockerfile
│
├── order/
│   ├── app.py
│   ├── Dockerfile
│
├── k8s/
│   ├── user-deployment.yaml
│   ├── product-deployment.yaml
│   ├── order-deployment.yaml
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   ├── storage.yaml
│
└── README.md
```

---


<br>



## ☁️ Step 1: Launch EC2 Instance

Go to → AWS → EC2

### Configuration:

* OS: Ubuntu 22.04
* Instance: t2.micro
* Security Group:

  * 22 (SSH)
  * 80 (HTTP)
  * 30000–32767 (NodePort)

### Connect:

```bash
ssh -i "key.pem" ubuntu@your-ip
```




| **Instance**    | **Security Group**          |
|------------------------------------|----------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20111221.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20111053.png?raw=true) |




---

## ⚙️ Step 2: Install Required Tools

### Update system

```bash
sudo apt update && sudo apt upgrade -y
```

### Install Docker

```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
```

Reconnect:

```bash
exit
ssh -i "key.pem" ubuntu@your-ip
```



###  Install containerd

```Bash
sudo apt install -y containerd
```
🔥 IMPORTANT FIX
```Bash
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
```

Edit:

```Bash
sudo nano /etc/containerd/config.toml
```

Find:
```
SystemdCgroup = false
```
👉 Press:
```
CTRL + W
```

- Search `SystemdCgroup`


Change to:
```
SystemdCgroup = true
```
Save & restart:
```Bash
sudo systemctl restart containerd
```




### Install Kubernetes (kubeadm)

```bash
sudo apt install -y apt-transport-https curl gpg

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | \
gpg --dearmor | sudo tee /etc/apt/keyrings/kubernetes-apt-keyring.gpg > /dev/null

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | \
sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Disable swap

```bash
sudo swapoff -a
sudo modprobe br_netfilter
```

###  System Configuration


***📌 Description***

This step enables required Linux kernel settings for Kubernetes networking.

```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
```

```Bash
sudo sysctl --system
```

👉 Why?

Enables Kubernetes networking
Pod communication proper hote


---

## ☸️ Step 3: Initialize Kubernetes

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

### Configure kubectl

```bash
mkdir -p $HOME/.kube
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

🔥 IMPORTANT (Single Node Fix)

```Bash
kubectl taint nodes --all node-role.kubernetes.io/control-plane-
```


### Install Network Plugin

```bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### Verify

```bash
kubectl get nodes
kubectl get pods -n kube-system
```

👉 Wait until Node = Ready

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20105039.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>



---

## 📁 Step 4: Create Project Files

```bash
mkdir -p ~/project/{user,product,order,k8s}
cd ~/project
```

👉 What this does:

Creates this structure:
```
project/
 ├── user/
 ├── product/
 ├── order/
 └── k8s/
```
👉 Each folder = one microservice<br>
👉 `k8s`/ = Kubernetes YAML files


---

## 🐳 Step 5: Microservice Code

### user-service/app.py

```Bash
from flask import Flask
import requests

app = Flask(__name__)

@app.route('/')
def home():
    try:
        res = requests.get("http://product-service:5000")
        return "User Service + " + res.text
    except:
        return "User Service Running (Product not reachable)"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

### product-service/app.py

```Bash
cd ~/project/product
nano app.py
```

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Product Service Running"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

### order-service/app.py  (with storage)

```Bash
cd ~/project/order
nano app.py
```

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    with open("/data/orders.txt", "a") as f:
        f.write("New Order\n")
    return "Order Stored"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

## 🐳 Step 6: Dockerfile (Same for all)

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install flask requests
CMD ["python", "app.py"]
```

---

## 🐳 Step 7: Build & Push Images

> This step is for who do not already have a Docker account.

###  Step 7A: Create DockerHub Account (ONE TIME)   

🌐 ***Go to***:

https://hub.docker.com/

***Do this***:

- Click ***Sign Up**
- Enter:
- Username (example: `nikiimisal`)
   - Email
   - Password
- Click Create Account

DockerHub is a cloud registry where Docker images are stored and shared.





<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20111641.png?raw=true" width="500" alt="Initialize Repository Screenshot">
</p>






---


###  Step 7B: Login from Terminal


```
docker login -u YOUR_USERNAME
```
👉 Then: `Enter password`

This step connects your local system to your DockerHub account.


---

###  Step 7C: Set Username

```
export DOCKER_USERNAME=nikiimisal
```

>👉 Now you can reuse $DOCKER_USERNAME everywhere

###  Step 7D: Build & Push Docker Images

👉 Make sure you are in project root:

```Bash
cd ~/project
```

```Bash
docker build -t $DOCKER_USERNAME/user ./user
docker build -t $DOCKER_USERNAME/product ./product
docker build -t $DOCKER_USERNAME/order ./order
```

```Bash
docker push $DOCKER_USERNAME/user
docker push $DOCKER_USERNAME/product
docker push $DOCKER_USERNAME/order
```

Verify Images :

```Bash
docker images
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20105241.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20111142.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>



>Each command builds a Docker image from the Dockerfile and tags it using your DockerHub username for pushing to the remote registry.

---

## ☸️ Step 8: Kubernetes Deployments

###  Storage (for order-service)

```
cd ~/project/k8s
nano storage.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```


```Bash
kubectl apply -f storage.yaml
```


###  Deployments (3 services)


👉 1. user-deployment.yaml

```
nano user-deployment.yaml
```

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 2
  selector:
    matchLabels:
      app: user
  template:
    metadata:
      labels:
        app: user
    spec:
      containers:
      - name: user
        image: nikiimisal/user:latest
        ports:
        - containerPort: 5000

        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "200m"

        livenessProbe:
          httpGet:
            path: /
            port: 5000
          initialDelaySeconds: 5
          periodSeconds: 10
```

👉 2. product-deployment.yaml

```
nano product-deployment.yaml
```

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: product-service
spec:
  replicas: 2
  selector:
    matchLabels:
      app: product
  template:
    metadata:
      labels:
        app: product
    spec:
      containers:
      - name: product
        image: nikiimisal/product:latest
        ports:
        - containerPort: 5000

        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "200m"

        livenessProbe:
          httpGet:
            path: /
            port: 5000
          initialDelaySeconds: 5
          periodSeconds: 10
```

👉 3. order-deployment.yaml (with storage)

```
nano order-deployment.yaml
```

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: order
  template:
    metadata:
      labels:
        app: order
    spec:
      containers:
      - name: order
        image: nikiimisal/order:latest
        ports:
        - containerPort: 5000

        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "200m"

        livenessProbe:
          httpGet:
            path: /
            port: 5000
          initialDelaySeconds: 5
          periodSeconds: 10

        volumeMounts:
        - mountPath: "/data"
          name: storage

      volumes:
      - name: storage
        persistentVolumeClaim:
          claimName: pvc
```






---

## 🌐 Step 9: Services (Expose to Internet)

`user-service`

```
nano user-service.yaml
```

```YAML
apiVersion: v1
kind: Service
metadata:
  name: user-service
spec:
  type: NodePort
  selector:
    app: user
  ports:
  - port: 5000
    targetPort: 5000
    nodePort: 30007
```

👉 order-service

```
nano order-service.yaml
```
```YAML
apiVersion: v1
kind: Service
metadata:
  name: order-service
spec:
  type: NodePort
  selector:
    app: order
  ports:
  - port: 5000
    targetPort: 5000
    nodePort: 30008
```

👉 product-service 

```
nano product-service.yaml
```

```YAML
apiVersion: v1
kind: Service
metadata:
  name: product-service
spec:
  type: NodePort
  selector:
    app: product
  ports:
  - port: 5000
    targetPort: 5000
    nodePort: 30009
```


👉  Scaling (HPA)

```
nano hpa.yaml
```

```YAML
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: product-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: product-service
  minReplicas: 2
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

Add Metrics Server (IMPORTANT for HPA actually working) :

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Test HPA :

```
kubectl run -i --tty load-generator --image=busybox -- /bin/sh
```

```
kubectl apply -f hpa.yaml
```





###  Apply Everything


👉 Make sure you are inside k8s folder:

```
kubectl apply -f .
```
Verify
```
kubectl get pods
```
```
kubectl get svc
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20105507.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>


```
kubectl get hpa
```


<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20105713.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>

```
kubectl patch deployment metrics-server -n kube-system \
--type='json' \
-p='[{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-insecure-tls"},{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-preferred-address-types=InternalIP"}]'
```

<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20102148.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>








---

## 🌐 Access Service

```
http://EC2-IP:30007 → User Service
http://EC2-IP:30008 → Order Service
http://EC2-IP:30009 → Product Service
```

| **User Service**    | **Order Service**          | **Product Service**          |
|--------------------------------|------------------------------------|------------------------------------|
| ![VS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20120110.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20120122.png?raw=true) | ![AWS](https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20120129.png?raw=true) |



---

## 📸 Step 14: Screenshots

Take screenshots of:

* Pods running
* Services
* HPA scaling
* Browser output
* PV working






<p align="center">
  <img src="https://github.com/nikiimisal/Internship--Project-s/blob/main/img/proj-5/Screenshot%202026-03-26%20110522.png?raw=true" width="700" alt="Initialize Repository Screenshot">
</p>




---

## ✅ Final Result

* Microservices deployed on Kubernetes
* Load balancing working
* Auto scaling enabled
* Persistent storage implemented

---

## Report: Cloud-Native Microservices Deployment


### Cluster Setup

A Kubernetes cluster was created on an AWS EC2 (Ubuntu 22.04) instance using kubeadm. Docker and containerd were installed and configured. Swap was disabled, and required kernel settings were enabled for networking. The cluster was initialized, kubectl configured, and Flannel CNI was installed. Control-plane taint was removed for single-node scheduling.

---

### Deployment & Testing

Three Flask-based microservices (user, product, order) were containerized using Docker and pushed to DockerHub. Kubernetes Deployments and Services (NodePort) were created to run and expose them. Persistent Volume and PVC were used for order-service storage.

HPA was configured for product-service based on CPU usage. Metrics Server was installed to enable autoscaling. Services were tested via browser and load generation using BusyBox.

---

### Tools & Technologies

AWS EC2, Docker, containerd, Kubernetes (kubeadm), Python Flask, Flannel CNI, DockerHub, HPA, Metrics Server, PV & PVC.

---

### Challenges & Solutions

* Pods not scheduling → Removed control-plane taint
* Container runtime issue → Fixed containerd config
* HPA not working → Installed & patched Metrics Server
* Service not accessible → Used NodePort & opened ports
* Storage issue → Configured PV & PVC correctly

---

### Conclusion

Successfully deployed a scalable microservices architecture with Kubernetes, including load balancing, autoscaling, and persistent storage, simulating a real-world cloud-native environment.


---
---
---




<br>
<br>

