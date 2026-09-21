# Organizational Portfolio Platform

## Project Overview

Organizational Portfolio Platform adalah platform website yang dirancang sebagai fondasi reusable untuk organisasi seperti Rohis, komunitas, dan organisasi pelajar.

Platform ini dikembangkan dengan pendekatan:

* Modular Monolith
* Layered Architecture
* Domain-Driven Design secara pragmatis
* Static-first dan SSR untuk kebutuhan website
* Separation of Concerns
* Test-driven validation pada domain dan application layer
* Infrastructure abstraction untuk persistence dan external services

Fokus versi awal adalah menyediakan platform portfolio organisasi yang ringan, maintainable, responsive, dan dapat digunakan kembali untuk organisasi yang berbeda.

---

## 1. Requirements & Domain Design

Tahap awal digunakan untuk menentukan kebutuhan platform sebelum menentukan implementasi teknis.

### Fitur utama V1

* Organization Profile
* Vision & Mission
* Organization Structure
* Divisions
* Members
* Programs / Activities
* Documentation / Media
* Articles / Information
* Search
* Contact

### Domain entities

```text
Organization
Division
Member
Program
Committee Assignment
Media
Article
Contact Message
```

Beberapa business rules juga telah ditentukan, antara lain:

* Member memiliki satu Division pada V1.
* Member dapat memiliki beberapa Committee Assignment dalam Program yang berbeda.
* Organizational Role dan Committee Role dipisahkan.
* Program memiliki Primary Division.
* Media dibuat provider-agnostic.
* Gallery tidak dibuat sebagai entity tersendiri, tetapi merupakan presentation/query terhadap Media.
* Contact Message tidak membutuhkan Visitor entity.

Lifecycle juga telah ditentukan untuk Program dan Article.

Program:

```text
DRAFT
   ↓
PUBLISHED
   ├──→ COMPLETED
   └──→ CANCELLED
              ↓
           ARCHIVED
```

Article:

```text
DRAFT
   ↓
PUBLISHED
   ↓
ARCHIVED
```

---

## 2. Architecture & Technology

Arsitektur yang dipilih adalah Modular Monolith dengan Layered Architecture.

Struktur dependency utama:

```text
Presentation
      ↓
Application
      ↓
Domain
```

Infrastructure berfungsi sebagai implementasi terhadap abstraction yang dibutuhkan oleh application/domain.

### Technology baseline

```text
Architecture       : Modular Monolith
Frontend           : Astro
Backend            : Python + FastAPI
Application        : Use-case oriented
Domain             : Framework independent
ORM                : SQLAlchemy
Database           : PostgreSQL
Migration          : Alembic
API                : REST /api/v1
Rendering          : Static-first + SSR/dynamic
Client JS          : Minimal / Progressive Enhancement
Media              : S3-compatible abstraction
Search             : PostgreSQL-based
```

Beberapa teknologi sengaja belum digunakan pada V1 seperti Redis, Kafka, Kubernetes, GraphQL, microservices, AI chatbot, n8n automation, dan complex RBAC.

---

## 3. Repository Bootstrap

Repository dibuat dari awal dengan struktur modular:

```text
portofolio-organisasi/
├── web/
├── server/
├── core/
│   ├── domain/
│   └── application/
├── infrastructure/
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── docs/
├── .env.example
├── .gitignore
└── pyproject.toml
```

Environment dasar:

```text
Python 3.12.14
Python venv
FastAPI 0.141.1
Pydantic 2.13.5
Uvicorn 0.53.0
Astro 5.14.1
```

Backend awal menyediakan:

```text
GET /health
GET /api/v1/health
```

Keduanya telah diverifikasi dapat memberikan HTTP 200.

---

## 4. Web Foundation

Frontend dibuat menggunakan Astro dengan pendekatan reusable components.

Foundation yang telah dibuat meliputi:

* Base Layout
* Header
* Navigation
* Footer
* Skip Link
* Responsive layout
* Accessibility foundation
* Button component
* Card component
* Section component
* Global CSS

Halaman V1 yang telah dibuat:

```text
/
 /about
 /members
 /divisions
 /programs
 /documentation
 /articles
 /contact
```

Seluruh halaman menggunakan synthetic/demo data sehingga platform tidak bergantung pada data organisasi tertentu.

---

## 5. Domain Layer

Domain layer dikembangkan secara terpisah dari framework dan infrastructure.

Entity yang telah dibuat:

```text
Organization
Division
Member
Program
Media
Article
Contact Message
Committee Assignment
```

Beberapa contoh business validation yang sudah diterapkan:

### Organization

Nama organisasi wajib tersedia dan tidak boleh kosong.

### Division

Nama Division wajib tersedia.

### Member

Member wajib memiliki:

```text
name
division_id
organizational_role
```

### Program

Program wajib memiliki title dan status.

Program yang akan dipublish wajib memiliki:

```text
primary_division_id
description
```

Lifecycle Program juga divalidasi oleh domain.

### Media

Media wajib memiliki:

```text
media_type
provider
reference
```

Image media wajib memiliki `alt_text`.

### Article

Article memiliki lifecycle:

```text
DRAFT → PUBLISHED → ARCHIVED
```

Article yang dipublish wajib memiliki content.

### Contact Message

Contact Message memiliki:

```text
name
email
message
created_at
```

Email divalidasi dan timestamp dibuat oleh sistem.

### Committee Assignment

Committee Assignment memiliki:

```text
member_id
program_id
committee_role
```

Kombinasi ketiganya digunakan sebagai logical identity.

---

## 6. Application Layer

Application layer menggunakan pendekatan use-case oriented.

Repository abstraction dibuat pada application layer, sedangkan implementasinya akan berada di infrastructure.

Contoh:

```text
OrganizationRepository
        ↓
GetOrganization

DivisionRepository
        ↓
GetDivisions

MemberRepository
        ↓
GetMembers

ProgramRepository
        ↓
GetPrograms

MediaRepository
        ↓
GetMedia

ArticleRepository
        ↓
GetArticles

ContactMessageRepository
        ↓
CreateContactMessage

CommitteeAssignmentRepository
        ↓
GetCommitteeAssignments
```

Dengan pendekatan ini, application layer tidak bergantung langsung pada SQLAlchemy atau PostgreSQL.

---

## 7. Testing

Testing dilakukan secara bertahap setelah setiap domain/application slice.

Progress test berkembang dari test health awal hingga seluruh domain dan application layer.

Sebelum masuk persistence:

```text
66 tests passed
```

Setelah implementasi persistence configuration:

```text
70 tests passed
```

Setelah implementasi SQLAlchemy persistence boundary:

```text
78 tests passed
```

Ruff juga telah digunakan untuk memastikan kualitas dan konsistensi kode.

---

## 8. Persistence Layer

Tahap persistence dimulai setelah domain dan application layer selesai.

### M6.1 — Persistence Configuration

Dibuat configuration boundary:

```text
infrastructure/configuration/
├── __init__.py
└── settings.py
```

Configuration saat ini menangani:

```text
APP_ENV
DATABASE_URL
```

Selain itu disiapkan konfigurasi untuk:

```text
Object Storage
Email Provider
```

tanpa memasukkan credential asli ke repository.

Commit:

```text
7757fe3 feat: add persistence configuration boundary
```

---

## 9. SQLAlchemy Engine & Session Boundary

### M6.2

SQLAlchemy ditambahkan sebagai dependency:

```text
sqlalchemy==2.0.54
```

Persistence database boundary dibuat di:

```text
infrastructure/persistence/database.py
```

Boundary tersebut bertanggung jawab terhadap:

* SQLAlchemy engine
* session factory
* configuration-driven database URL
* lazy database initialization
* testability

Import module tidak langsung membuat koneksi database.

Database connection dibuat secara lazy oleh SQLAlchemy ketika benar-benar diperlukan.

Unit tests menggunakan SQLite in-memory sehingga tahap ini tidak membutuhkan PostgreSQL server aktif.

Commit:

```text
4cf6ece feat: add sqlalchemy persistence boundary
```

Validation:

```text
78 passed
Ruff: All checks passed
```

---

## 10. Current Architecture

Kondisi architecture saat ini:

```text
                 WEB
                  │
                  ▼
            Presentation
                  │
                  ▼
             Application
                  │
                  ▼
               Domain
                  ▲
                  │
          Infrastructure
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
    Persistence          External
    SQLAlchemy            Services
        │
        ▼
    PostgreSQL
```

Persistence boundary saat ini sudah tersedia, tetapi ORM model dan repository implementation untuk entity belum dibuat.

---

## 11. Current Progress

```text
M0  Requirements & Domain Design       ✅
M1  Architecture & Technology          ✅
M2  Repository & Bootstrap Contract    ✅
M3  Repository Bootstrap               ✅
M4  Organization Domain                 ✅
M5  Web Foundation & Pages             ✅
M5.5 Domain + Application Layer        ✅
M6.1 Persistence Configuration         ✅
M6.2 SQLAlchemy Engine + Session       ✅
M6.3 Organization Persistence          ⏭️
```

### Next planned step

M6.3 akan mengimplementasikan persistence untuk `Organization`:

```text
Organization Domain
        ↓
OrganizationRepository abstraction
        ↓
SQLAlchemy ORM Model
        ↓
Repository Implementation
        ↓
PostgreSQL
```

Testing akan menggunakan SQLite in-memory agar persistence logic dapat diverifikasi tanpa membutuhkan PostgreSQL server pada unit/infrastructure test.

---

## Git Commit Progress

Beberapa milestone utama:

```text
3449180 chore: bootstrap organizational portfolio platform
667e35a feat: add organization domain
b4a8fa7 feat: add organization application use case
1092d22 feat: add division domain and application use case
035dd3b feat: add member domain and application use case
6aff54b feat: add program domain and application use case
9cfd0a3 feat: add media domain and application use case
6d36c79 feat: add article domain and application use case
50d04b7 feat: add contact message domain and application use case
a8985f6 feat: add committee assignment domain and application use case
7757fe3 feat: add persistence configuration boundary
4cf6ece feat: add sqlalchemy persistence boundary
```

Current branch:

```text
main
```

Working tree terakhir:

```text
clean
```

## Summary

Sampai tahap M6.2, platform sudah memiliki fondasi architecture, frontend, domain model, application use cases, automated tests, configuration boundary, serta SQLAlchemy persistence boundary.

Tahap berikutnya adalah mulai menghubungkan domain dengan persistence melalui Organization ORM model dan repository implementation tanpa mengorbankan dependency boundary antara Domain, Application, dan Infrastructure.
