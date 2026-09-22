# M6 — Persistence & Database Integration

## Status

**Completed**

M6 merupakan tahap implementasi persistence layer dan integrasi database untuk Organizational Portfolio Platform.

Tujuan utama milestone ini adalah membangun boundary persistence yang tetap terpisah dari domain dan application layer, menyediakan repository berbasis SQLAlchemy, menggunakan PostgreSQL sebagai target database, serta memastikan schema database dikelola melalui Alembic.

---

## 1. Objectives

M6 memiliki tujuan:

* Menambahkan configuration boundary untuk persistence.
* Menambahkan SQLAlchemy sebagai ORM/persistence layer.
* Mengimplementasikan persistence untuk seluruh domain entity V1.
* Memisahkan repository abstraction dari implementasi persistence.
* Menambahkan database migration menggunakan Alembic.
* Menyediakan integration test terhadap PostgreSQL nyata.
* Memastikan domain object tidak bocor sebagai ORM object.
* Memastikan unit test tetap dapat berjalan tanpa PostgreSQL.

---

## 2. Persistence Architecture

Boundary persistence yang digunakan:

```text
Presentation
      ↓
Application
      ↓
Domain
      ↓
Repository Abstraction
      ↓
SQLAlchemy Repository
      ↓
PostgreSQL
```

Database schema dikelola secara terpisah:

```text
SQLAlchemy Models
       ↓
     Alembic
       ↓
PostgreSQL Schema
```

Domain layer tetap framework-independent.

Domain tidak bergantung langsung pada:

* FastAPI
* SQLAlchemy
* PostgreSQL
* Alembic
* environment variables
* storage provider
* email provider

Repository implementation berada di infrastructure layer dan bertugas melakukan mapping:

```text
Domain Entity ↔ ORM Model
```

Dengan demikian persistence technology dapat berubah tanpa mengubah domain model.

---

# 3. M6.1 — Persistence Configuration

Ditambahkan configuration boundary:

```text
infrastructure/configuration/
├── __init__.py
└── settings.py
```

Configuration menggunakan environment variables dan tidak menyimpan credential di source code.

Configuration utama:

```text
APP_ENV
DATABASE_URL
```

`DATABASE_URL` digunakan sebagai sumber konfigurasi database untuk persistence dan Alembic.

Tidak digunakan `pydantic-settings` agar configuration boundary tetap sederhana dan tidak menambah dependency yang belum diperlukan.

### Verification

```text
70 passed
Ruff: passed
```

Commit:

```text
7757fe3 feat: add persistence configuration boundary
```

---

# 4. M6.2 — SQLAlchemy Persistence Boundary

SQLAlchemy `2.0.54` ditambahkan sebagai persistence dependency.

Database abstraction dibuat untuk:

* lazy engine creation
* session factory
* test database override
* database access melalui infrastructure layer

SQLAlchemy tidak diperkenalkan ke domain atau application layer.

### Verification

```text
78 passed
Ruff: passed
```

Commit:

```text
4cf6ece feat: add sqlalchemy persistence boundary
```

---

# 5. M6.3 — Organization Persistence

Ditambahkan:

```text
organization_model.py
organization_repository.py
test_organization_repository.py
```

Database table:

```text
organizations
```

Field utama:

```text
id
name
description
history
vision
mission
location
contact
social_media
```

`social_media` disimpan sebagai JSON.

Repository melakukan mapping antara ORM model dan domain `Organization`.

### Verification

```text
85 passed
Ruff: passed
```

Commit:

```text
d68a052 feat: add organization persistence
```

---

# 6. M6.4 — Division Persistence

Ditambahkan persistence untuk `Division`.

Database table:

```text
divisions
```

Field:

```text
id
name
description
```

Tidak dibuat `organization_id` maupun foreign key tambahan karena field tersebut belum menjadi bagian dari domain contract pada tahap ini.

Hal ini menjaga agar database schema tidak menginventasikan relationship yang belum ditentukan oleh domain.

### Verification

```text
92 passed
Ruff: passed
```

Commit:

```text
f7f0b0e feat: add division persistence
```

---

# 7. M6.5 — Member Persistence

Database table:

```text
members
```

Field:

```text
id
name
division_id
organizational_role
description
```

`division_id` diperlakukan sebagai opaque identifier sesuai domain model saat ini dan tidak dibuat foreign key yang belum ditentukan.

### Verification

```text
100 passed
Ruff: passed
```

Commit:

```text
1c9285a feat: add member persistence
```

---

# 8. M6.6 — Program Persistence

Database table:

```text
programs
```

Field:

```text
id
title
status
primary_division_id
description
```

Status domain dipertahankan menggunakan:

```text
DRAFT
PUBLISHED
COMPLETED
CANCELLED
ARCHIVED
```

Repository melakukan reconstruction dari database value menjadi `ProgramStatus`.

### Verification

```text
113 passed
Ruff: passed
```

Commit:

```text
ebe974c feat: add program persistence
```

---

# 9. M6.7 — Committee Assignment Persistence

Database table:

```text
committee_assignments
```

Field:

```text
id
member_id
program_id
committee_role
```

Ditambahkan composite unique constraint:

```text
(member_id, program_id, committee_role)
```

Tujuannya memastikan satu anggota tidak dapat memiliki committee role yang sama dua kali pada program yang sama.

Role berbeda pada program yang sama tetap diperbolehkan.

### Verification

Pengujian mencakup:

* persistence round-trip
* duplicate assignment rejection
* multiple roles
* composite uniqueness

### Commit

```text
093b3ad feat: add committee assignment persistence
```

---

# 10. M6.8 — Media Persistence

Database table:

```text
media
```

Field:

```text
id
media_type
provider
reference
alt_text
```

Media tetap provider-agnostic.

Persistence layer tidak mengunci platform tertentu seperti YouTube, Google Drive, S3, atau provider lainnya.

### Verification

```text
133 passed
Ruff: passed
```

Commit:

```text
ac0d9b6 feat: add media persistence
```

---

# 11. M6.9 — Article Persistence

Database table:

```text
articles
```

Field:

```text
id
title
status
content
```

Status:

```text
DRAFT
PUBLISHED
ARCHIVED
```

Repository melakukan reconstruction dari database value menjadi `ArticleStatus`.

Aturan domain seperti kebutuhan content ketika artikel dipublish tetap berada di domain layer.

### Verification

```text
144 passed
Ruff: passed
```

Commit:

```text
fcb9c57 feat: add article persistence
```

---

# 12. M6.10 — Contact Message Persistence

Database table:

```text
contact_messages
```

Field:

```text
id
name
email
message
created_at
```

`created_at` berasal dari domain object dan dipersist sebagai timezone-aware datetime.

Tidak ditambahkan:

* visitor entity
* authentication
* notification
* workflow status
* admin system

Karena fitur tersebut belum menjadi bagian dari V1 scope.

SQLite memiliki perbedaan dalam mempertahankan timezone information sehingga repository menangani restoration ke UTC untuk menjaga timezone-aware behavior pada domain object.

### Verification

```text
154 tests
Ruff: passed
```

Commit:

```text
8d5696a feat: add contact message persistence
```

---

# 13. M6.11 — Alembic Migration Foundation

Alembic `1.20.0` ditambahkan sebagai migration tool.

Migration menggunakan shared SQLAlchemy metadata sebagai source schema.

Initial migration:

```text
15c099525413
```

Schema mencakup:

```text
organizations
divisions
members
programs
committee_assignments
media
articles
contact_messages
```

Migration diverifikasi melalui:

```text
upgrade
downgrade
autogenerate verification
```

Alembic tidak menyimpan database credential di `alembic.ini`.

Database URL diambil melalui configuration boundary yang sudah ada.

### Verification

```text
164 passed
Ruff: passed
Alembic check: No new upgrade operations detected
Alembic head: 15c099525413
```

Commit:

```text
44072a0 feat: add alembic migration foundation
```

---

# 14. M6.12 — PostgreSQL Integration Test Foundation

Tahap terakhir M6 menambahkan integration test terhadap PostgreSQL nyata.

Environment variable yang digunakan:

```text
TEST_DATABASE_URL
```

Credential tidak disimpan di repository.

Integration tests dipisahkan dari unit tests menggunakan pytest marker:

```text
integration
```

Command:

```bash
python -m pytest -m integration -q
```

Jika PostgreSQL tidak tersedia atau `TEST_DATABASE_URL` tidak diberikan, integration tests tidak dikonversi menjadi SQLite test. Test akan skip dengan alasan yang jelas.

---

## 15. PostgreSQL Integration Coverage

Integration test mencakup:

* Alembic migration pada PostgreSQL.
* Organization repository round-trip.
* Division repository round-trip.
* Member repository round-trip.
* Program repository round-trip.
* Committee Assignment persistence.
* Committee Assignment uniqueness constraint.
* Media repository round-trip.
* Article repository round-trip.
* Contact Message repository round-trip.
* Contact Message timezone behavior.
* Repository API tidak membocorkan ORM object.

Schema PostgreSQL dibuat melalui:

```text
Alembic migration
```

bukan hanya:

```text
Base.metadata.create_all()
```

Integration environment juga dibersihkan setelah pengujian.

---

# 16. Final Verification

Normal test suite:

```text
164 passed
38 skipped
```

Integration test:

```text
38 passed
```

Ruff:

```text
All checks passed
```

PostgreSQL:

```text
Actually exercised
```

Alembic migration:

```text
Successfully exercised against PostgreSQL
```

Integration cleanup:

```text
Successful
```

Working tree setelah commit:

```text
On branch main
nothing to commit, working tree clean
```

Final M6 integration commit:

```text
d68af09 test: add postgresql integration foundation
```

---

# 17. M6 Final Result

M6 berhasil membangun persistence foundation yang lengkap:

```text
Domain
   ↓
Application Repository Abstraction
   ↓
Infrastructure Repository
   ↓
SQLAlchemy
   ↓
PostgreSQL
```

Database schema:

```text
SQLAlchemy Models
        ↓
      Alembic
        ↓
   PostgreSQL
```

Testing:

```text
Unit Tests
    ↓
SQLite / in-memory

Integration Tests
    ↓
Real PostgreSQL
    ↓
Alembic Migration
```

Dengan hasil ini, persistence layer sudah memiliki:

* domain/persistence separation
* repository abstraction
* SQLAlchemy implementation
* PostgreSQL target
* Alembic migration
* migration verification
* PostgreSQL integration testing
* ORM/domain separation verification
* timezone behavior verification
* composite uniqueness verification
* clean configuration boundary
* no hard-coded credentials

---

## 18. Milestone Commits

```text
7757fe3 feat: add persistence configuration boundary
4cf6ece feat: add sqlalchemy persistence boundary
d68a052 feat: add organization persistence
f7f0b0e feat: add division persistence
1c9285a feat: add member persistence
ebe974c feat: add program persistence
093b3ad feat: add committee assignment persistence
ac0d9b6 feat: add media persistence
fcb9c57 feat: add article persistence
8d5696a feat: add contact message persistence
44072a0 feat: add alembic migration foundation
d68af09 test: add postgresql integration foundation
```

## Status

**M6 — Persistence & Database Integration: COMPLETE**

The project is now ready to move from isolated domain/application/persistence verification toward the first end-to-end application vertical slice.
