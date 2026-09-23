
# M8 — Public Search

**Status:** Completed  
**Commit:** `1e2e836 feat: add public search`

## 1. Tujuan

M8 bertujuan menambahkan fitur pencarian publik pada Organizational Portfolio Platform.

Fitur ini memungkinkan pengunjung mencari informasi organisasi melalui satu endpoint API dan halaman pencarian web.

Prinsip utama:

- Search merupakan application capability, bukan domain entity.
- Menggunakan PostgreSQL sebagai search backend.
- Tidak menggunakan search engine eksternal.
- Tidak menambahkan tabel khusus untuk search.
- Tidak menggunakan Elasticsearch, Meilisearch, Redis, vector database, atau AI ranking.
- Hanya konten yang boleh ditampilkan publik yang dapat muncul pada hasil pencarian.

---

## 2. Arsitektur

Alur pencarian:

```text
Search UI
    │
    ▼
GET /api/v1/search?q=...
    │
    ▼
FastAPI API Boundary
    │
    ▼
SearchPublicContent
    │
    ▼
SearchRepository
    │
    ▼
SqlAlchemySearchRepository
    │
    ▼
PostgreSQL
````

Implementasi mengikuti layered architecture yang digunakan sejak M1.

---

## 3. Application Layer

Ditambahkan:

```text
core/application/search/
├── __init__.py
├── repository.py
└── use_cases.py
```

### SearchResult

Application layer menggunakan `SearchResult` sebagai representasi hasil pencarian:

```text
type
title
description
url
```

Database ID tidak menjadi bagian dari response.

### SearchRepository

Dibuat abstraction:

```python
class SearchRepository(ABC):
    @abstractmethod
    def search(self, query: str) -> list[SearchResult]:
        raise NotImplementedError
```

Hal ini menjaga application layer tetap tidak bergantung pada SQLAlchemy atau PostgreSQL.

### SearchPublicContent

Use case:

```text
SearchPublicContent
```

bertanggung jawab melakukan validasi query sebelum pencarian diteruskan ke repository.

Aturan:

* query di-trim
* query kosong ditolak
* query whitespace-only ditolak
* maksimal 255 karakter

---

## 4. Persistence Layer

Ditambahkan:

```text
infrastructure/persistence/search_repository.py
```

Implementasi:

```text
SqlAlchemySearchRepository
```

Repository menggunakan PostgreSQL melalui SQLAlchemy dan melakukan pencarian case-insensitive menggunakan `ILIKE`.

### Sumber data yang dicari

| Tipe         | Field                                        |
| ------------ | -------------------------------------------- |
| Organization | `name`, `description`                        |
| Division     | `name`, `description`                        |
| Member       | `name`, `organizational_role`, `description` |
| Program      | `title`, `description`                       |
| Media        | `alt_text`                                   |
| Article      | `title`, `content`                           |

Program dan Article hanya dicari jika berstatus:

```text
PUBLISHED
```

---

## 5. Search Security

Search pattern menangani karakter wildcard PostgreSQL:

```text
\
%
_
```

Karakter tersebut di-escape sebelum digunakan pada `ILIKE`.

Dengan demikian input pengguna tidak secara tidak sengaja diperlakukan sebagai wildcard.

Media hanya dicari berdasarkan:

```text
alt_text
```

Field:

```text
reference
```

sengaja tidak digunakan sebagai search field.

---

## 6. Result Limits

Untuk menjaga response tetap ringan:

```text
Maximum per content type : 10
Maximum total results    : 50
Description limit        : 200 characters
```

Description juga dinormalisasi whitespace-nya sebelum dikirim ke client.

---

## 7. Public API

Ditambahkan endpoint:

```http
GET /api/v1/search?q=<query>
```

Contoh:

```http
GET /api/v1/search?q=rohis
```

Contoh response:

```json
[
  {
    "type": "organization",
    "title": "Rohis Surakarta",
    "description": "Organisasi kerohanian siswa untuk pembinaan dan kegiatan positif.",
    "url": "/about"
  },
  {
    "type": "program",
    "title": "Rohis Academy",
    "description": "Program pembinaan dan pengembangan anggota Rohis.",
    "url": "/programs"
  }
]
```

API tidak mengembalikan database ID.

---

## 8. Content Visibility

Search mengikuti aturan public visibility.

Contoh:

```text
Program PUBLISHED
    → searchable

Program DRAFT
    → tidak searchable

Article PUBLISHED
    → searchable

Article DRAFT
    → tidak searchable
```

Hal ini mencegah draft content bocor melalui endpoint publik.

---

## 9. Web UI

Ditambahkan:

```text
web/src/pages/search.astro
```

Route:

```text
/search
```

Alur client:

```text
User membuka /search
        │
        ▼
Input keyword
        │
        ▼
Submit
        │
        ▼
GET /api/v1/search
        │
        ▼
Render results
```

UI memiliki beberapa state:

```text
Initial
   │
   ├── Searching
   │
   ├── Results found
   │
   ├── No results
   │
   └── Error
```

Input menggunakan:

```html
<input
  type="search"
  maxlength="255"
/>
```

dan memiliki label yang accessible.

---

## 10. Client-Side Security

Hasil dari API tidak langsung dipercaya sebagai HTML.

Text content di-escape sebelum dirender menggunakan fungsi:

```text
escapeHtml()
```

Tujuannya mencegah hasil pencarian diperlakukan sebagai HTML atau JavaScript oleh browser.

---

## 11. Navigation

Search ditambahkan ke navigasi utama:

```text
Tentang
Pengurus
Program
Artikel
Cari
Kontak
```

Dengan demikian `/search` menjadi bagian dari user flow utama platform.

---

## 12. CORS Development

Saat melakukan browser validation ditemukan bahwa Astro development server:

```text
http://127.0.0.1:4321
```

mengakses API:

```text
http://127.0.0.1:8000
```

yang menggunakan origin berbeda.

Browser kemudian memblokir request karena CORS.

Ditambahkan konfigurasi CORS FastAPI untuk development agar frontend dapat mengakses API selama pengembangan lokal.

---

## 13. Testing

M8 menambahkan testing untuk beberapa layer:

```text
tests/unit/test_search_use_case.py
tests/unit/test_search_repository.py
tests/unit/test_search_api.py
tests/integration/test_search_api.py
```

Final test result:

```text
252 passed
67 skipped
1 warning
```

Warning berasal dari dependency Starlette/AnyIO dan bukan dari implementasi Search.

---

## 14. PostgreSQL Integration Test

Search diuji menggunakan PostgreSQL aktual melalui temporary Podman container.

Integration test mencakup:

* pencarian data yang tersimpan
* case-insensitive search
* published-only filtering
* database ID tidak bocor
* `Media.reference` tidak digunakan sebagai search field
* empty query ditolak
* whitespace-only query ditolak
* query terlalu panjang ditolak

Temporary PostgreSQL digunakan hanya selama proses validasi.

Setelah validasi selesai, container:

```text
portofolio-m86-pg
```

telah dihentikan dan dihapus.

Tidak ada container PostgreSQL M8 yang tertinggal.

---

## 15. Code Quality

Ruff validation:

```text
All checks passed!
```

Tidak ditemukan masalah linting pada final M8 implementation.

---

## 16. Production Build

Astro production build berhasil:

```text
output: "static"
mode: "static"
```

Total:

```text
9 page(s) built
```

Termasuk:

```text
/search/index.html
```

Build selesai tanpa error.

---

## 17. Git

M8 dikemas dalam satu commit:

```text
1e2e836 feat: add public search
```

Commit berisi:

```text
18 files changed
1426 insertions(+)
```

Working tree setelah commit:

```text
clean
```

Branch:

```text
main
```

---

## 18. M8 Final Validation

| Validation                   | Result |
| ---------------------------- | ------ |
| Application tests            | PASS   |
| Repository tests             | PASS   |
| API tests                    | PASS   |
| PostgreSQL integration tests | PASS   |
| Published-only filtering     | PASS   |
| Query validation             | PASS   |
| Search UI                    | PASS   |
| Browser validation           | PASS   |
| CORS development setup       | PASS   |
| Ruff                         | PASS   |
| Astro production build       | PASS   |
| Git diff check               | PASS   |
| Git commit                   | PASS   |
| Temporary PostgreSQL cleanup | PASS   |

---

## 19. Result

M8 berhasil mengintegrasikan fitur public search dari frontend sampai persistence layer:

```text
┌─────────────────────┐
│     Search UI       │
│      /search        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   FastAPI /api/v1   │
│       /search       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ SearchPublicContent │
│     Use Case        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  SearchRepository   │
│     Abstraction     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ SQLAlchemy Search   │
│     Repository      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│     PostgreSQL      │
└─────────────────────┘
```

M8 selesai tanpa menambahkan infrastructure baru yang belum dibutuhkan oleh V1.

**Next milestone:** M9.

```
```
