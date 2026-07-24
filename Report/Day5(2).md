# PHP Installation

PHP 8.4 installation and integration with Nginx on Debian 13.

This project is part of my Infrastructure Portfolio developed during Industrial Internship (PKL).

---

# Overview

PHP is used to create dynamic web applications.

This project integrates PHP with Nginx and MariaDB to build a dynamic infrastructure portfolio.

---

# Technology

- Debian 13
- Nginx
- PHP 8.4
- PHP-FPM
- MariaDB

---

# Features

- PHP Installation
- PHP-FPM
- Nginx Integration
- MariaDB Connection
- Dynamic Website

---

# Installation

## Update Repository

```bash
sudo apt update
```

---

## Install PHP

```bash
sudo apt install php php-fpm php-mysql -y
```

---

## Verify PHP Version

```bash
php -v
```

Example output:

```text
PHP 8.4.x
```

---

## Check PHP-FPM

```bash
sudo systemctl status php8.4-fpm
```

---

## Enable PHP-FPM

```bash
sudo systemctl enable php8.4-fpm

sudo systemctl start php8.4-fpm
```

---

# Configure Nginx

Edit default configuration.

```bash
sudo nano /etc/nginx/sites-available/default
```

Enable PHP processing.

```nginx
location ~ \.php$ {

include snippets/fastcgi-php.conf;

fastcgi_pass unix:/run/php/php8.4-fpm.sock;

}
```

---

## Test Configuration

```bash
sudo nginx -t
```

---

## Restart Services

```bash
sudo systemctl restart nginx

sudo systemctl restart php8.4-fpm
```

---

# Test PHP

Create test file.

```bash
sudo nano /var/www/portfolio/info.php
```

Content:

```php
<?php

phpinfo();

?>
```

Open browser.

```
http://SERVER_IP/info.php
```

If the PHP Information page appears, PHP is successfully configured.

---

# Dynamic Website

Current website uses:

- PHP
- HTML
- CSS
- MariaDB

Example connection.

```php
<?php

$conn = mysqli_connect(
"localhost",
"webuser",
"Password123!",
"portfolio_db"
);

?>
```

---

# Folder Structure

```
portfolio/
│
├── index.php
├── projects.php
├── certificates.php
│
├── config
│   └── database.php
│
├── assets
│
└── uploads
```

---

# Verification

Check PHP.

```bash
php -v
```

Check loaded modules.

```bash
php -m
```

Check PHP-FPM.

```bash
systemctl status php8.4-fpm
```

---

# Future Development

- Login Authentication
- Admin Dashboard
- CRUD Projects
- CRUD Certificates
- Image Upload
- Session Management

---

# Author

Maulana Aldi Pradana

SMK Negeri 2 Surakarta

Infrastructure Portfolio
