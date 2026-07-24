# Infrastructure Portfolio Website

A dynamic infrastructure portfolio website built using **Debian 13**, **Nginx**, **PHP 8.4**, and **MariaDB**.

This project was developed during my Industrial Internship (PKL) as part of my learning journey in Infrastructure Engineering, System Administration, and Web Development.

---

## Preview

### Dashboard

- Infrastructure Overview
- Learning Progress
- Featured Projects
- Recent Activity

### Dynamic Features

- Dynamic Project List
- Dynamic Certificate List
- Dynamic Statistics Dashboard
- MariaDB Integration
- PHP Dynamic Rendering

---

# Technology Stack

| Technology | Description |
|------------|-------------|
| Debian 13 | Operating System |
| Nginx | Web Server |
| PHP 8.4 | Backend |
| MariaDB | Database |
| HTML5 | Frontend |
| CSS3 | Styling |

---

# Current Features

## Dashboard

- Dynamic Project Counter
- Dynamic Certificate Counter
- Infrastructure Status
- Learning Progress
- Recent Activity

## Projects

- Display all projects from MariaDB
- Project status
- Technology used
- Project description

## Certificates

- Display certificates from database
- Issue date
- Issuer
- Dynamic data rendering

---

# Database Structure

## projects

| Column | Type |
|---------|------|
| id | INT |
| project_name | VARCHAR |
| category | VARCHAR |
| technology | VARCHAR |
| status | VARCHAR |
| description | TEXT |
| created_at | TIMESTAMP |

---

## certificates

| Column | Type |
|---------|------|
| id | INT |
| certificate_name | VARCHAR |
| issuer | VARCHAR |
| category | VARCHAR |
| issue_date | DATE |
| verification_url | VARCHAR |
| image | VARCHAR |

---

# Project Structure

```
portfolio/
│
├── index.php
├── projects.php
├── certificates.php
├── learning.php
├── about.php
├── contact.php
│
├── config/
│   └── database.php
│
├── assets/
│   ├── css/
│   ├── images/
│   └── js/
│
└── uploads/
```

---

# Installation

## Clone Repository

```bash
git clone https://github.com/yourusername/infrastructure-portfolio.git
```

---

## Install Packages

```bash
sudo apt update

sudo apt install nginx mariadb-server php php-fpm php-mysql
```

---

## Configure MariaDB

```sql
CREATE DATABASE portfolio_db;
```

Import your SQL file.

---

## Configure PHP

Enable PHP-FPM in Nginx.

Example:

```nginx
location ~ \.php$ {

include snippets/fastcgi-php.conf;

fastcgi_pass unix:/run/php/php8.4-fpm.sock;

}
```

Restart services.

```bash
sudo systemctl restart nginx

sudo systemctl restart php8.4-fpm
```

---

# Dynamic Features

This website reads data directly from MariaDB.

Adding a new project:

```sql
INSERT INTO projects(...)
```

↓

Automatically appears on:

- Dashboard
- Projects Page
- Recent Activity

No HTML modification required.

---

# Screenshots

## Dashboard

```
(Add Screenshot Here)
```

---

## Projects

```
(Add Screenshot Here)
```

---

## Certificates

```
(Add Screenshot Here)
```

---

# Learning Objectives

This project was created to practice:

- Linux Administration
- Nginx Configuration
- PHP Programming
- MariaDB
- Dynamic Website Development
- Infrastructure Documentation

---

# Future Roadmap

## Version 2

- Dynamic Projects
- Dynamic Certificates

Completed

---

## Version 3

- Authentication System
- Admin Dashboard
- CRUD Projects
- CRUD Certificates
- Upload Images

---

## Version 4

- Docker Deployment
- Docker Compose
- Reverse Proxy
- Grafana Monitoring

---

## Version 5

- CI/CD Pipeline
- GitHub Actions
- Cloud Deployment
- HTTPS
- Security Hardening

---

# Author

**Maulana Aldi Pradana**

Infrastructure Engineering Student

SMK Negeri 2 Surakarta

Industrial Internship 2026

---

# License

This project is created for educational purposes and personal portfolio.

```

## Saya juga menyarankan beberapa tambahan untuk repository GitHub

Supaya repository-mu terlihat lebih profesional, tambahkan file dan folder berikut:

```text
portfolio/
├── README.md
├── LICENSE
├── .gitignore
├── database/
│   └── portfolio_db.sql
├── docs/
│   ├── screenshots/
│   ├── architecture.png
│   └── deployment.md
├── assets/
├── config/
├── uploads/
└── index.php
```

Dengan struktur ini, siapa pun yang membuka repository akan langsung mendapatkan:
- Dokumentasi proyek (`README.md`)
- Skrip database (`database/portfolio_db.sql`)
- Screenshot aplikasi (`docs/screenshots/`)
- Diagram arsitektur (`docs/architecture.png`)
- Panduan deployment (`docs/deployment.md`)

Ini membuat repositori tidak hanya berisi kode, tetapi juga dokumentasi yang lengkap dan mudah dipahami, sehingga memberikan kesan yang lebih profesional bagi pembimbing PKL maupun perekrut yang melihat portofoliomu. 
