# MariaDB Database Server

MariaDB Database Server installation and configuration on Debian 13.

This project is part of my Infrastructure Portfolio developed during my Industrial Internship (PKL).

---

# Overview

The purpose of this project is to build a relational database server that will later be used by a dynamic PHP website.

The database stores project information and certificates displayed on the portfolio website.

---

# Technology

- Debian 13
- MariaDB
- SQL

---

# Features

- MariaDB Installation
- Database Creation
- User Management
- Privilege Management
- Table Creation
- Data Manipulation
- Database Connection for PHP

---

# Installation

## Update Repository

```bash
sudo apt update
```

---

## Install MariaDB

```bash
sudo apt install mariadb-server -y
```

---

## Enable Service

```bash
sudo systemctl enable mariadb

sudo systemctl start mariadb
```

---

## Check Service

```bash
sudo systemctl status mariadb
```

---

## Secure Installation

```bash
sudo mysql_secure_installation
```

Configuration used:

- Remove anonymous users : Yes
- Disallow root login remotely : Yes
- Remove test database : Yes
- Reload privilege tables : Yes

---

# Database Configuration

Login into MariaDB.

```bash
sudo mysql
```

Create Database.

```sql
CREATE DATABASE portfolio_db;
```

---

## Create User

```sql
CREATE USER 'webuser'@'localhost'
IDENTIFIED BY 'Password123!';
```

---

## Grant Privileges

```sql
GRANT ALL PRIVILEGES
ON portfolio_db.*
TO 'webuser'@'localhost';

FLUSH PRIVILEGES;
```

---

# Tables

## projects

```sql
CREATE TABLE projects(

id INT AUTO_INCREMENT PRIMARY KEY,

project_name VARCHAR(100),

category VARCHAR(100),

technology VARCHAR(200),

status VARCHAR(50),

description TEXT,

created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);
```

---

## certificates

```sql
CREATE TABLE certificates(

id INT AUTO_INCREMENT PRIMARY KEY,

certificate_name VARCHAR(150),

issuer VARCHAR(100),

category VARCHAR(100),

issue_date DATE,

verification_url VARCHAR(255),

image VARCHAR(255)

);
```

---

# Sample Data

```sql
INSERT INTO projects
(project_name,category,technology,status,description)
VALUES
(
'DNS Server',
'Infrastructure',
'Debian 13, BIND9',
'Completed',
'Local DNS Server using BIND9.'
);
```

---

# Database Structure

```
portfolio_db
│
├── projects
│
└── certificates
```

---

# Verification

Show databases.

```sql
SHOW DATABASES;
```

Show tables.

```sql
SHOW TABLES;
```

Display projects.

```sql
SELECT * FROM projects;
```

Display certificates.

```sql
SELECT * FROM certificates;
```

---

# Future Development

- phpMyAdmin
- Backup & Restore
- Database Replication
- Docker MariaDB

---

# Author

Maulana Aldi Pradana

SMK Negeri 2 Surakarta

Infrastructure Portfolio
