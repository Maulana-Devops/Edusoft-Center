# Nginx Web Server - Infrastructure Portfolio

Membangun web server menggunakan **Nginx** pada **Debian 13** sebagai dasar website portofolio selama kegiatan Praktik Kerja Lapangan (PKL).

---

## Project Information

| Information | Detail |
|------------|--------|
| Project | Nginx Web Server |
| Operating System | Debian GNU/Linux 13 |
| Web Server | Nginx |
| DNS | BIND9 |
| Type | Static Website |
| Status | Completed |

---

# Project Objective

- Menginstal dan mengonfigurasi Nginx sebagai web server.
- Membuat website portofolio sederhana.
- Menghubungkan website dengan DNS lokal.
- Menyiapkan fondasi untuk pengembangan proyek selanjutnya.

---

# Features

- Static Website
- HTML & CSS
- Local DNS Access
- Nginx Configuration
- Responsive Layout
- Portfolio Dashboard

---

# Directory Structure

```text
/var/www/portofolio
│
├── index.html
│
├── css
│   └── style.css
│
├── js
│   └── script.js
│
├── images
│
├── projects
│   ├── dns-server.html
│   └── web-server.html
│
├── certificates.html
├── learning.html
├── about.html
└── contact.html
```

---

# Installation

## Update Repository

```bash
apt update
```

## Install Nginx

```bash
apt install nginx -y
```

## Check Service

```bash
systemctl status nginx
```

---

# Create Website Directory

```bash
mkdir -p /var/www/portofolio
```

```bash
cd /var/www/portofolio
```

---

# Create Project Structure

```bash
mkdir css
mkdir js
mkdir images
mkdir projects
```

```bash
touch index.html
touch css/style.css
touch js/script.js
touch projects/dns-server.html
touch projects/web-server.html
```

---

# Configure Permissions

```bash
chown -R www-data:www-data /var/www/portofolio
```

```bash
chmod -R 755 /var/www/portofolio
```

---

# Configure Nginx

Edit configuration:

```bash
nano /etc/nginx/sites-available/default
```

Example configuration:

```nginx
server {

    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/portofolio;

    index index.html;

    server_name _;

    location / {

        try_files $uri $uri/ =404;

    }

}
```

---

# Test Configuration

```bash
nginx -t
```

Expected output

```text
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Restart service

```bash
systemctl restart nginx
```

---

# Access Website

Using IP Address

```
http://192.168.1.19
```

Using Local DNS

```
http://server.pkl.local
```

---

# Website Preview


```
<img width="1277" height="550" alt="image" src="https://github.com/user-attachments/assets/361350bb-720d-4587-b961-711bc6046742" />

```

---

# Source Code

## HTML

```html
<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Maulana Aldi Pradana | Infrastructure Portfolio</title>

    <link rel="stylesheet" href="css/style.css">

</head>

<body>

<!-- ================= HEADER ================= -->

<header>

    <div class="container">

        <div class="logo">

            <div class="logo-box">
                M
            </div>

            <div>

                <h1>Maulana Aldi Pradana</h1>

                <p class="subtitle">
                    Infrastructure Portfolio
                </p>

            </div>

        </div>

        <p class="description">

            Building reliable infrastructure, documenting every project, and continuously improving through industrial practice.

        </p>

        <div class="hero-button">

            <a href="projects.html" class="button">

                View Projects

            </a>

            <a href="certificates.html" class="button secondary">

                Certificates

            </a>

        </div>

    </div>

</header>

<!-- ================= NAVBAR ================= -->

<nav>

    <a href="index.html">Home</a>

    <a href="projects.html">Projects</a>

    <a href="certificates.html">Certificates</a>

    <a href="learning.html">Learning</a>

    <a href="about.html">About</a>

    <a href="contact.html">Contact</a>

</nav>

<!-- ================= STATS ================= -->

<section class="cards">

    <div class="card">

        <h2>Projects</h2>

        <span>02</span>

        <p>Completed</p>

    </div>

    <div class="card">

        <h2>Certificates</h2>

        <span>00</span>

        <p>Collected</p>

    </div>

    <div class="card">

        <h2>Current Week</h2>

        <span>04</span>

        <p>Industrial Internship</p>

    </div>

    <div class="card">

        <h2>Repositories</h2>

        <span>02</span>

        <p>GitHub</p>

    </div>

</section>

<!-- ================= DASHBOARD ================= -->

<div class="dashboard">

<!-- STATUS -->

<section class="status">

<h2>Infrastructure Status</h2>

<ul>

<li>

Debian 13

<span class="badge online">

ONLINE

</span>

</li>

<li>

BIND9 DNS Server

<span class="badge online">

ONLINE

</span>

</li>

<li>

Nginx Web Server

<span class="badge online">

ONLINE

</span>

</li>

<li>

MariaDB

<span class="badge warning">

SETUP

</span>

</li>

<li>

Docker

<span class="badge offline">

PLANNED

</span>

</li>

<li>

Kubernetes

<span class="badge offline">

PLANNED

</span>

</li>

<li>

Cloud

<span class="badge offline">

PLANNED

</span>

</li>

<li>

Security

<span class="badge offline">

PLANNED

</span>

</li>

</ul>

</section>

<!-- PROGRESS -->

<section class="progress">

<h2>Learning Progress</h2>

<div class="bar">

<div class="label">

<span>Linux</span>

<span>100%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:100%;"></div>

</div>

</div>

<div class="bar">

<div class="label">

<span>Networking</span>

<span>95%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:95%;"></div>

</div>

</div>

<div class="bar">

<div class="label">

<span>DNS</span>

<span>100%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:100%;"></div>

</div>

</div>

<div class="bar">

<div class="label">

<span>Nginx</span>

<span>70%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:70%;"></div>

</div>

</div>

<div class="bar">

<div class="label">

<span>Database</span>

<span>20%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:20%;"></div>

</div>

</div>

<div class="bar">

<div class="label">

<span>Docker</span>

<span>0%</span>

</div>

<div class="progress-bg">

<div class="progress-fill" style="width:0%;"></div>

</div>

</div>

</section>

</div>

<!-- ================= PROJECT ================= -->

<section>

<h2>Featured Projects</h2>

<div class="project-grid">

<div class="project-card">

<h3>DNS Server</h3>

<p>

Local DNS Server using Debian 13 and BIND9.

</p>

<div class="badge complete">

COMPLETED

</div>

<a href="projects/dns-server.html" class="button">

Details

</a>

</div>

<div class="project-card">

<h3>Infrastructure Portfolio</h3>

<p>

Static Portfolio Website powered by Nginx.

</p>

<div class="badge warning">

IN PROGRESS

</div>

<a href="projects/web-server.html" class="button">

Details

</a>

</div>

</div>

</section>

<!-- ================= ACTIVITY ================= -->

<section class="activity">

<h2>Recent Activity</h2>

<table>

<tr>

<th>Date</th>

<th>Activity</th>

<th>Status</th>

</tr>

<tr>

<td>22 Jul 2026</td>

<td>DNS Server Deployment</td>

<td>

<span class="badge complete">

DONE

</span>

</td>

</tr>

<tr>

<td>23 Jul 2026</td>

<td>Portfolio Website</td>

<td>

<span class="badge warning">

ONGOING

</span>

</td>

</tr>

<tr>

<td>24 Jul 2026</td>

<td>Database Server</td>

<td>

<span class="badge offline">

NEXT

</span>

</td>

</tr>

</table>

</section>

<footer>

<p>

Infrastructure Portfolio

</p>

<p>

Powered by Debian 13 | Nginx | GitHub

</p>

<p>

© 2026 Maulana Aldi Pradana

</p>

</footer>

</body>

</html>
```

---

## CSS

```css
/* =======================================================
   Infrastructure Portfolio
   Author : Maulana Aldi Pradana
======================================================= */

:root{
    --bg:#0F172A;
    --card:#1E293B;
    --navbar:#111827;
    --primary:#3B82F6;
    --primary-hover:#2563EB;
    --success:#22C55E;
    --warning:#FACC15;
    --danger:#EF4444;
    --text:#F8FAFC;
    --secondary:#94A3B8;
    --border:#334155;
}

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html{
    scroll-behavior:smooth;
}

body{
    background:var(--bg);
    color:var(--text);
    font-family:Arial, Helvetica, sans-serif;
    line-height:1.6;
}

/* =======================================================
   CONTAINER
======================================================= */

.container{
    width:90%;
    max-width:1200px;
    margin:auto;
}

/* =======================================================
   HEADER
======================================================= */

header{

    background:linear-gradient(135deg,#1E293B,#0F172A);

    text-align:center;

    padding:80px 20px;

    border-bottom:1px solid var(--border);

}

header h1{

    font-size:42px;

    margin-bottom:15px;

}

.subtitle{

    color:var(--secondary);

    font-size:18px;

}

.description{

    max-width:700px;

    margin:20px auto;

    color:#CBD5E1;

}

.hero-button{

    margin-top:35px;

    display:flex;

    justify-content:center;

    gap:20px;

    flex-wrap:wrap;

}

/* =======================================================
   BUTTON
======================================================= */

.button{

    text-decoration:none;

    background:var(--primary);

    color:white;

    padding:12px 24px;

    border-radius:8px;

    transition:.3s;

    font-weight:bold;

}

.button:hover{

    background:var(--primary-hover);

}

.secondary{

    background:transparent;

    border:2px solid var(--primary);

}

.secondary:hover{

    background:var(--primary);

}

/* =======================================================
   NAVBAR
======================================================= */

nav{

    background:var(--navbar);

    display:flex;

    justify-content:center;

    gap:35px;

    padding:18px;

    position:sticky;

    top:0;

    z-index:999;

    border-bottom:1px solid var(--border);

}

nav a{

    color:white;

    text-decoration:none;

    transition:.3s;

    font-weight:bold;

}

nav a:hover{

    color:var(--primary);

}

/* =======================================================
   SECTION
======================================================= */

section{

    width:90%;

    max-width:1200px;

    margin:45px auto;

}

section h2{

    margin-bottom:25px;

}

/* =======================================================
   DASHBOARD CARDS
======================================================= */

.cards{

    display:grid;

    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));

    gap:20px;

}

.card{

    background:var(--card);

    border:1px solid var(--border);

    border-radius:15px;

    padding:30px;

    text-align:center;

    transition:.3s;

}

.card:hover{

    transform:translateY(-6px);

    border-color:var(--primary);

    box-shadow:0 10px 25px rgba(0,0,0,.35);

}

.card span{

    display:block;

    margin:15px 0;

    font-size:36px;

    font-weight:bold;

    color:var(--primary);

}

.card p{

    color:var(--secondary);

}

/* =======================================================
   TWO COLUMN DASHBOARD
======================================================= */

.dashboard{

    width:90%;

    max-width:1200px;

    margin:40px auto;

    display:grid;

    grid-template-columns:1fr 1fr;

    gap:25px;

}

/* =======================================================
   STATUS
======================================================= */

.status{

    background:var(--card);

    border:1px solid var(--border);

    border-radius:15px;

    padding:30px;

}

.status ul{

    list-style:none;

}

.status li{

    padding:12px 0;

    border-bottom:1px solid rgba(255,255,255,.05);

}

/* =======================================================
   PROGRESS
======================================================= */

.progress{

    background:var(--card);

    border:1px solid var(--border);

    border-radius:15px;

    padding:30px;

}

.bar{

    margin:22px 0;

}

.bar p{

    margin-bottom:8px;

}

.progress-bg{

    background:#334155;

    height:16px;

    border-radius:50px;

    overflow:hidden;

}

.progress-fill{

    height:100%;

    background:linear-gradient(90deg,#3B82F6,#2563EB);

    border-radius:50px;

}

/* =======================================================
   PROJECT GRID
======================================================= */

.project-grid{

    display:grid;

    grid-template-columns:repeat(auto-fit,minmax(300px,1fr));

    gap:20px;

}

.project-card{

    background:var(--card);

    border:1px solid var(--border);

    border-radius:15px;

    padding:25px;

    transition:.3s;

}

.project-card:hover{

    transform:translateY(-5px);

    border-color:var(--primary);

}

.project-card h3{

    margin-bottom:12px;

}

.project-card p{

    margin-bottom:15px;

}

.done{

    color:var(--success);

    font-weight:bold;

}

.progressing{

    color:var(--warning);

    font-weight:bold;

}

/* =======================================================
   FOOTER
======================================================= */

footer{

    background:var(--navbar);

    text-align:center;

    padding:35px;

    margin-top:60px;

    border-top:1px solid var(--border);

}

footer p{

    color:var(--secondary);

    margin:6px 0;

}

/* =======================================================
   SCROLLBAR
======================================================= */

::-webkit-scrollbar{

    width:10px;

}

::-webkit-scrollbar-track{

    background:#0f172a;

}

::-webkit-scrollbar-thumb{

    background:#334155;

    border-radius:10px;

}

::-webkit-scrollbar-thumb:hover{

    background:#475569;

}

/* =======================================================
   RESPONSIVE
======================================================= */

@media(max-width:900px){

    .dashboard{

        grid-template-columns:1fr;

    }

}

@media(max-width:768px){

    header h1{

        font-size:30px;

    }

    nav{

        flex-wrap:wrap;

        gap:18px;

    }

    section{

        width:95%;

    }

    .hero-button{

        flex-direction:column;

        align-items:center;

    }

}

/* =======================================================
   LOGO
======================================================= */

.logo{
    display:flex;
    justify-content:center;
    align-items:center;
    gap:20px;
    margin-bottom:20px;
}

.logo-box{
    width:70px;
    height:70px;
    background:var(--primary);
    border-radius:15px;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:30px;
    font-weight:bold;
    color:white;
    box-shadow:0 0 20px rgba(59,130,246,.35);
}

/* =======================================================
   BADGE
======================================================= */

.badge{
    display:inline-block;
    padding:6px 14px;
    border-radius:20px;
    font-size:12px;
    font-weight:bold;
    letter-spacing:.5px;
}

.online{
    background:rgba(34,197,94,.15);
    color:var(--success);
    border:1px solid var(--success);
}

.warning{
    background:rgba(250,204,21,.15);
    color:var(--warning);
    border:1px solid var(--warning);
}

.offline{
    background:rgba(148,163,184,.15);
    color:var(--secondary);
    border:1px solid var(--secondary);
}

.complete{
    background:rgba(59,130,246,.15);
    color:var(--primary);
    border:1px solid var(--primary);
}

/* =======================================================
   STATUS LIST
======================================================= */

.status li{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:14px 0;
    border-bottom:1px solid rgba(255,255,255,.08);
}

.status li:last-child{
    border-bottom:none;
}

/* =======================================================
   PROGRESS LABEL
======================================================= */

.label{
    display:flex;
    justify-content:space-between;
    margin-bottom:8px;
    font-size:14px;
}

/* =======================================================
   PROJECT BUTTON
======================================================= */

.project-card .button{
    margin-top:15px;
    display:inline-block;
}

/* =======================================================
   ACTIVITY TABLE
======================================================= */

.activity{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:15px;
    padding:30px;
}

.activity table{
    width:100%;
    border-collapse:collapse;
}

.activity th{
    text-align:left;
    padding:14px;
    color:var(--primary);
    border-bottom:2px solid var(--border);
}

.activity td{
    padding:15px 14px;
    border-bottom:1px solid rgba(255,255,255,.06);
}

.activity tr:last-child td{
    border-bottom:none;
}

.activity tr:hover{
    background:rgba(255,255,255,.03);
}

/* =======================================================
   HOVER EFFECT
======================================================= */

.card,
.project-card,
.status,
.progress,
.activity{
    transition:.3s;
}

.status:hover,
.progress:hover,
.activity:hover{
    transform:translateY(-5px);
    border-color:var(--primary);
    box-shadow:0 10px 25px rgba(0,0,0,.35);
}

/* =======================================================
   RESPONSIVE TABLE
======================================================= */

@media(max-width:768px){

.activity{
    overflow-x:auto;
}

.activity table{
    min-width:600px;
}

.logo{
    flex-direction:column;
}

.logo-box{
    width:60px;
    height:60px;
    font-size:26px;
}

}
```

---

# Project Result

- Successfully installed Nginx on Debian 13.
- Successfully configured Document Root.
- Successfully deployed a static portfolio website.
- Website accessible through IP Address.
- Website accessible through Local DNS.
- Ready for future integration with Database, Docker, Kubernetes, Cloud, and Security projects.

---

# Next Roadmap

- [x] Debian Installation
- [x] DNS Server (BIND9)
- [x] Nginx Web Server
- [ ] Database Server
- [ ] Docker
- [ ] Kubernetes
- [ ] Monitoring
- [ ] Reverse Proxy
- [ ] Cloud Deployment
- [ ] Security Hardening

---

# Author

**Maulana Aldi Pradana**

Infrastructure • System Administrator • DevOps Learning

Industrial Internship Project 2026
