# LAMP-Application-Hosting-Student-Registration-System
# LAMP Application Hosting – Student Registration System

## Project Overview

This project demonstrates the deployment of a PHP-based Student Registration System on Amazon Web Services (AWS) using the **LAMP architecture**.

The application allows users to register students by entering their name, email, course, and phone number. The information is stored in an **Amazon RDS MySQL database**.

The project follows the architecture:

**User → Apache → PHP → Amazon EC2 → Amazon RDS MySQL**

This project is based on the LAMP Application Hosting project specification, which uses EC2, RDS, Linux, Apache, PHP, and MySQL.

---

## Objectives

* Deploy a PHP web application on AWS.
* Configure an Ubuntu EC2 instance as a web server.
* Install and configure Apache.
* Install and configure PHP.
* Create an Amazon RDS MySQL database.
* Connect the PHP application with RDS.
* Store student registration information in MySQL.
* Demonstrate communication between the application and database layers.

---

## AWS Services and Technologies

* **Amazon EC2** – Hosts the PHP web application.
* **Amazon RDS** – Hosts the MySQL database.
* **Ubuntu Linux** – Operating system for the EC2 instance.
* **Apache2** – Web server.
* **PHP 8.5.4** – Server-side programming language.
* **MySQL 8.4.9** – Database management system.
* **HTML/CSS** – Frontend interface.
* **SSH** – Used to connect to the EC2 instance.

---

## System Architecture

```text
                    Internet
                       |
                       | HTTP : 80
                       ↓
              ┌─────────────────┐
              │   Ubuntu EC2    │
              │                 │
              │    Apache2      │
              │       ↓         │
              │      PHP        │
              │       ↓         │
              │ Student App     │
              └────────┬────────┘
                       |
                       | MySQL : 3306
                       ↓
              ┌─────────────────┐
              │   Amazon RDS    │
              │     MySQL       │
              │                 │
              │   student_db    │
              │   students      │
              └─────────────────┘
```

---

## Application Features

The Student Registration System provides:

* Student name entry
* Email entry
* Course entry
* Phone number entry
* Student registration
* Display of registered students
* Automatic student ID generation
* Database storage using Amazon RDS MySQL
* Automatic registration timestamp

---

## Database Structure

### Database

```text
student_db
```

### Table

```text
students
```

### Columns

| Column     | Data Type    | Description                       |
| ---------- | ------------ | --------------------------------- |
| id         | INT          | Primary key and auto-increment ID |
| name       | VARCHAR(100) | Student name                      |
| email      | VARCHAR(100) | Student email                     |
| course     | VARCHAR(100) | Student course                    |
| phone      | VARCHAR(20)  | Student phone number              |
| created_at | TIMESTAMP    | Registration date and time        |

---

## Implementation Steps

### 1. Launch EC2 Instance

An Ubuntu EC2 instance was launched on AWS.

The instance was configured with:

* SSH – Port 22
* HTTP – Port 80

The EC2 instance provides the server environment for the application.

### 2. Connect to EC2

The instance was accessed using SSH:

```bash
ssh -i "truved.pem" ubuntu@EC2_PUBLIC_IP
```

### 3. Update Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

### 4. Install Apache, PHP and MySQL Support

```bash
sudo apt install apache2 php libapache2-mod-php php-mysql -y
```

Apache was enabled and started:

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

Apache status was verified using:

```bash
sudo systemctl status apache2
```

### 5. Test PHP

A PHP information page was created:

```text
/var/www/html/info.php
```

The PHP installation was verified through the browser.

The deployed environment uses **PHP 8.5.4**.

### 6. Create Amazon RDS MySQL Database

An Amazon RDS MySQL database was created.

The database was configured with:

```text
Database: student_db
Table: students
```

### 7. Connect EC2 to RDS

The MySQL client was installed on EC2:

```bash
sudo apt install mysql-client -y
```

The RDS database was accessed using:

```bash
mysql -h RDS_ENDPOINT -u admin -p
```

### 8. Create Database

```sql
CREATE DATABASE student_db;
```

The database was selected:

```sql
USE student_db;
```

### 9. Create Students Table

```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    course VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 10. Deploy PHP Application

The main application was created at:

```text
/var/www/html/index.php
```

The PHP application connects to RDS using the MySQLi extension.

The application performs:

1. Database connection
2. Form submission
3. Student data insertion
4. Retrieval of registered students
5. Display of student records

### 11. Restart Apache

```bash
sudo systemctl restart apache2
```

### 12. Access the Application

The application can be accessed through the EC2 public IP:

```text
http://EC2_PUBLIC_IP
```

---

## Project Workflow

```text
1. User opens the website
              ↓
2. Apache receives the request
              ↓
3. PHP processes the request
              ↓
4. Student fills the registration form
              ↓
5. PHP sends data to MySQL
              ↓
6. Amazon RDS stores the student record
              ↓
7. PHP retrieves the records
              ↓
8. Registered students are displayed
```

---

## Testing

The application was tested by registering a sample student.

Example:

```text
Name: Rahul Sharma
Email: rahul@example.com
Course: Cloud Computing
Phone: 9876543210
```

After submission, the application displays the registered student in the student table.

The database can also be verified using:

```sql
USE student_db;

SELECT * FROM students;
```

---

## Security Configuration

The EC2 Security Group allows:

```text
SSH   → Port 22
HTTP  → Port 80
```

The RDS Security Group allows:

```text
MySQL → Port 3306
```

Port 3306 should be restricted to the EC2 security group rather than being publicly accessible.

Database passwords should not be stored in GitHub or included in this README.

---

## Screenshots

The project report should include screenshots demonstrating:

1. EC2 instance running
2. Successful SSH connection
3. Apache service running
4. Apache2 default page
5. PHP information page
6. RDS database available
7. RDS connectivity configuration
8. Successful MySQL connection
9. `students` table structure
10. Student Registration System
11. Successful student registration
12. Student record stored in RDS

---

## Project Result

The project successfully demonstrates a **LAMP application hosted on AWS**.

The PHP Student Registration System runs on an Ubuntu EC2 instance using Apache and communicates with an Amazon RDS MySQL database. Student registration data is successfully stored and retrieved from the database.

---

## Conclusion

The project demonstrates how a traditional web application can be deployed using AWS cloud services. EC2 provides the application server, Apache handles HTTP requests, PHP processes the application logic, and Amazon RDS provides a managed MySQL database.

This architecture separates the application and database layers and provides a practical example of cloud-based application hosting.

---

## Future Enhancements

The application can be extended with:

* Student login
* Admin login
* Edit student records
* Delete student records
* Search students
* Course filtering
* Student profile pages
* Pagination
* Improved UI
* HTTPS using SSL/TLS
* Domain name configuration
* Application Load Balancer
* Automated deployment using CI/CD

---

## Author

**Project:** LAMP Application Hosting
**Application:** Student Registration System
**Platform:** Amazon Web Services (AWS)
**Database:** Amazon RDS MySQL
**Server:** Ubuntu EC2
**Web Server:** Apache2
**Backend:** PHP
