
#  AWS Java Reverse Proxy Deployment

Deploying a Java Web Application on AWS using --Nginx Reverse Proxy--, --Apache Tomcat--, and --AWS RDS MySQL--.

---

##  Project Overview

This project demonstrates how to deploy a --Java-based web application-- in a production-like environment using AWS services.
The architecture ensures --scalability, security, and separation of concerns-- by introducing a reverse proxy layer.

---

##  Architecture

```
User (Browser)
      ↓
Nginx (Reverse Proxy)
      ↓
Apache Tomcat (Application Server)
      ↓
AWS RDS MySQL (Database)
```

---

##  Technologies Used

-  AWS EC2 (Ubuntu Server)
-  Nginx (Reverse Proxy)
-  Apache Tomcat 9
-  Java (JSP / Servlet)
-  AWS RDS MySQL
-  Security Groups & Key Pairs

---

##  Features

-  Student Registration Form
-  Store Data in MySQL Database
-  View Student Records
-  Edit Existing Records
- Delete Records
- Reverse Proxy Routing via Nginx

---

##  Deployment Steps

###  1. Launch EC2 Instance

- Launch Ubuntu EC2 instance
- Allow ports:

  - 22 (SSH)
  - 80 (HTTP)
  - 8080 (Tomcat)

---

###  2. Install Required Packages

```bash
sudo apt update
sudo apt install nginx openjdk-11-jdk -y
```

---

###  3. Install Apache Tomcat

```bash
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.85/bin/apache-tomcat-9.0.85.tar.gz
tar -xvzf apache-tomcat-9.0.85.tar.gz
cd apache-tomcat-9.0.85/bin
chmod +x -.sh
./startup.sh
```

---

###  4. Configure Nginx Reverse Proxy

```bash
sudo nano /etc/nginx/sites-available/default
```

Replace with:

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

###  5. Setup AWS RDS MySQL

- Create RDS MySQL instance
- Allow EC2 security group access
- Note endpoint, username, password

---

###  6. Configure Database in Application

Update your Java DB connection:

```java
String url = "jdbc:mysql://<RDS-ENDPOINT>:3306/studentdb";
String user = "admin";
String password = "password";
```

---

###  7. Deploy WAR File

- Copy `.war` file to Tomcat:

```bash
cp your-app.war apache-tomcat-9.0.85/webapps/
```

- Restart Tomcat:

```bash
./shutdown.sh
./startup.sh
```

---

##  Application Screenshots

###  Student Registration Form

<img width="1064" height="614" src="https://github.com/user-attachments/assets/7b2c6447-ab35-4694-9559-8124d12850f2" />

###  Registration Successful Page

<img width="1919" height="1021" src="https://github.com/user-attachments/assets/fab7e1c6-0eaf-46e9-ac47-491e72d7601f" />

###  Students List

<img width="1868" height="798" src="https://github.com/user-attachments/assets/f4f1dd6f-06a5-428a-8bdd-b3c227b4efd0" />

---

##  Security Best Practices

- Use --Security Groups-- to restrict access
- Enable --only required ports--
- Store DB credentials securely (use environment variables)
- Disable root login on EC2

---

##  Future Enhancements

-  Add HTTPS using SSL (Let's Encrypt)
-  Integrate Monitoring (Prometheus + Grafana)
-  Add Load Balancer (AWS ALB)
-  Containerize using Docker
-  Deploy on Kubernetes

---

##  Learning Outcomes

- AWS EC2 & RDS setup
- Reverse Proxy concept using Nginx
- Java Web App deployment on Tomcat
- Database connectivity (JDBC)
- Production-level architecture basics

---
##  Author

Ritu Patil

---
