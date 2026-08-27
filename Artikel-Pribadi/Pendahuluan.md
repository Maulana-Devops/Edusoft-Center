
````markdown
# PROJECT CONTEXT — ARTIKEL PRIBADI TJKT

> Source of truth untuk proyek artikel pribadi bertema Teknik Jaringan Komputer dan Telekomunikasi (TJKT).
> Dokumen ini berisi tujuan, standar, workflow, roadmap, dan keputusan proyek.
> Artikel individual disimpan sebagai dokumen terpisah.

---

# 1. PROJECT IDENTITY

- Project name: Artikel Pribadi — TJKT
- Main platform: Hashnode
- Main topic: Teknik Jaringan Komputer dan Telekomunikasi (TJKT)
- Initial roadmap: 6 months
- Draft format: Markdown (.md)
- Main article language: English
- Supporting/internal language: Indonesian
- Main practical environment: Cisco Packet Tracer
- Main visual tool: Canva

---

# 2. PROJECT PURPOSE

Tujuan utama proyek:

1. Membangun portfolio teknis TJKT.
2. Mendokumentasikan proses belajar networking.
3. Memahami konsep networking secara fundamental.
4. Menghubungkan teori dengan praktik.
5. Melatih technical writing.
6. Melatih troubleshooting dan dokumentasi.
7. Membangun topic cluster networking.
8. Membangun discoverability melalui search engine.
9. Membuat konten yang mudah dipahami oleh AI answer engines.
10. Membuka kemungkinan monetisasi jangka panjang.

Prioritas:

Skill
→ Practice
→ Understanding
→ Documentation
→ Portfolio
→ Audience
→ Monetization

Monetisasi bukan prioritas utama.

---

# 3. PROJECT POSITIONING

Artikel tidak ditulis dengan positioning:

> "Saya adalah ahli networking."

Artikel ditulis dengan positioning:

> "Saya sedang mempelajari TJKT, melakukan praktik, mengamati hasilnya, kemudian mendokumentasikan apa yang saya pahami."

Nilai utama proyek adalah first-hand experience.

Core principle:

> Build it → Observe it → Explain it → Prove it → Document it

---

# 4. EDITORIAL PRINCIPLES

Setiap artikel harus:

- spesifik
- teknis
- fundamental
- mudah dipahami
- jujur terhadap hasil praktik
- menjelaskan WHY, bukan hanya HOW
- memiliki bukti jika membahas praktik
- menggunakan terminology networking yang benar
- menghindari klaim berlebihan

Jangan:

- keyword stuffing
- mengarang hasil praktik
- mengarang command output
- mengarang screenshot
- mengklaim eksperimen yang tidak dilakukan
- membuat artikel terlalu luas tanpa tujuan yang jelas

---

# 5. ARTICLE PHILOSOPHY

Artikel ideal mengikuti alur:

Question / Problem
↓
Context
↓
Concept
↓
Lab
↓
Experiment
↓
Observation
↓
Explanation
↓
Troubleshooting
↓
What I Learned
↓
Conclusion
↓
FAQ
↓
Next Article

Artikel harus menjawab satu pertanyaan teknis utama.

Contoh:

GOOD:
> How a Network Packet Travels Between Two Hosts

LESS IDEAL:
> Learn Networking

---

# 6. STANDARD ARTICLE STRUCTURE

Gunakan struktur berikut sebagai baseline:

```markdown
# [Article Title]

> [Direct answer / one-sentence summary]

## Introduction

## Why This Matters

## The Lab / Environment

## 1. [Concept]

## 2. [Concept]

## 3. [Concept]

## Practical Experiment

## What Happened?

## Troubleshooting

## What I Learned

## Conclusion

## Frequently Asked Questions

### [Question 1]

[Direct answer]

### [Question 2]

[Direct answer]

### [Question 3]

[Direct answer]

## What's Next?
````

Struktur dapat disesuaikan dengan topik.

---

# 7. TECHNICAL WRITING STANDARD

Untuk setiap command penting:

Command
↓
Purpose
↓
Expected output
↓
Interpretation
↓
Verification

Jangan hanya memberikan command tanpa menjelaskan alasan dan hasilnya.

Contoh:

```bash
show ip route
```

Harus dijelaskan:

* apa yang dilakukan
* apa yang ditampilkan
* arti informasi penting
* bagaimana informasi tersebut digunakan
* bagaimana memverifikasinya

---

# 8. PRACTICAL LAB STANDARD

Jika artikel menggunakan praktik:

1. Tentukan tujuan eksperimen.
2. Tentukan perangkat/tools.
3. Buat topology.
4. Konfigurasi.
5. Jalankan test.
6. Amati hasil.
7. Ambil evidence.
8. Jelaskan hasil.
9. Troubleshoot jika terjadi masalah.
10. Dokumentasikan kesimpulan.

Practical evidence dapat berupa:

* topology
* command output
* configuration
* ARP table
* MAC address table
* routing table
* ping
* traceroute
* packet capture
* simulation
* logs

---

# 9. EVIDENCE RULE

ATURAN PENTING:

> Never fabricate technical evidence.

Jangan mengarang:

* IP address
* MAC address
* ARP entry
* routing table
* command output
* ping result
* packet capture
* screenshot
* topology
* experiment result

Jika belum dilakukan:

> belum diuji

Jika dilakukan tetapi gagal:

> dokumentasikan sebagai hasil eksperimen

Jika hasil berbeda dari teori:

> jelaskan perbedaannya

---

# 10. SCREENSHOT STANDARD

Screenshot harus memiliki fungsi editorial.

Contoh:

1. Full topology
2. IP configuration
3. Interface status
4. ARP table
5. MAC address table
6. Routing table
7. Connectivity test
8. Packet simulation

Target normal:

> 5–9 useful screenshots per practical article.

Tidak perlu memaksakan jumlah screenshot.

Caption format:

> Figure X — [What the image shows or proves.]

Hindari:

> Screenshot hasil praktik.

---

# 11. SEO STANDARD

Setiap artikel harus memiliki:

## H1

Judul utama yang natural.

## SEO Title

Lebih pendek dan search-focused.

Target:

> preferably under 60 characters

## Slug

Rules:

* lowercase
* short
* descriptive
* hyphen-separated
* no unnecessary dates
* no unnecessary numbers

## Meta Description

* concise
* describes the actual article
* natural keyword usage
* follow Hashnode's character limit

## Primary Keyword

Satu search intent utama.

## Secondary Keywords

Istilah yang berkaitan dengan topik.

## Tags

Gunakan sekitar 3–5 tag relevan.

---

# 12. GEO / AEO STANDARD

Artikel harus mudah dipahami oleh:

* Google
* search engines
* AI answer engines
* human readers

Gunakan direct answers.

Contoh:

### What does a switch do?

> A switch forwards Ethernet frames based on destination MAC addresses.

Kemudian baru jelaskan secara lebih detail.

Gunakan:

* explicit questions
* concise answers
* clear terminology
* structured headings
* practical evidence
* factual explanations

Jangan menulis dengan tujuan memanipulasi AI.

Tujuannya adalah membuat informasi mudah diekstraksi karena memang terstruktur dan jelas.

---

# 13. FAQ STANDARD

Setiap artikel yang cocok memiliki FAQ.

Format:

```markdown
## Frequently Asked Questions

### What is a network packet?

[Direct answer]

### What is the difference between an IP address and a MAC address?

[Direct answer]

### What does a router do?

[Direct answer]
```

FAQ harus benar-benar berhubungan dengan artikel.

Jangan membuat FAQ hanya untuk memasukkan keyword.

---

# 14. INTERNAL LINKING

Artikel akan membentuk topic cluster.

Contoh:

Article 1
Network Packet Flow
↓
Article 2
IPv4 & Subnetting
↓
Article 3
ARP & Ethernet Switching
↓
Article 4
Static Routing
↓
Article 5
VLAN
↓
Article 6
Inter-VLAN Routing

Artikel lama harus diperbarui dengan link ke artikel baru jika relevan.

---

# 15. VISUAL IDENTITY

## OG Image

Tool:

> Canva

Format target:

> 1200 × 630 px

Gunakan reusable template.

Semua artikel harus memiliki visual identity yang konsisten.

Template pertama:

> TJKT Article #1 — Network Packet Flow

Canva master:
[https://www.canva.com/d/Nuq1lkD-phG_qFL](https://www.canva.com/d/Nuq1lkD-phG_qFL)

Future articles harus mempertahankan:

* visual hierarchy
* typography
* overall style
* technical/minimal aesthetic

Yang berubah:

* article number
* topic
* title
* technical visual

---

# 16. ARTICLE BODY IMAGES

Prioritas:

1. Real screenshot
2. Real topology
3. Real lab evidence
4. Custom technical diagram
5. Decorative image

AI-generated image tidak boleh digunakan sebagai bukti praktik.

---

# 17. HASHNODE STANDARD

Hashnode adalah publishing platform utama.

Untuk setiap artikel periksa:

* URL
* Tags
* SEO Title
* Description
* OG Image
* Canonical URL
* Visibility
* Scheduling

Jika artikel original pertama kali diterbitkan di Hashnode:

> Canonical URL biasanya dibiarkan kosong.

Jika artikel direpublikasikan dari/ke platform lain:

> Canonical harus dipertimbangkan dengan benar.

---

# 18. HASHNODE ARTICLE SETTINGS

Contoh konfigurasi Artikel #1:

SEO Title:

> How a Network Packet Travels Between Two Hosts

Slug:

> understanding-network-packet-flow

Description:

> Learn how a network packet travels between two hosts using IP, ARP, MAC addresses, switches, routers, and ICMP.

Tags:

> networking
> computer-networks
> tjkt
> cisco-packet-tracer

AEO/FAQ premium features tidak menjadi alasan untuk membeli upgrade.

Kualitas konten tetap menjadi prioritas.

---

# 19. SIX-MONTH ROADMAP

Roadmap awal:

## Month 1 — Networking Fundamentals

* Network packet flow
* IPv4
* Subnetting
* ARP
* MAC
* Ethernet

## Month 2 — Switching & Routing

* Static routing
* VLAN
* Trunking
* Inter-VLAN routing

## Month 3 — Network Services

* DHCP
* DNS
* NAT
* Basic network services

## Month 4 — Troubleshooting

* ping
* traceroute
* ARP troubleshooting
* DNS troubleshooting
* Layer-based troubleshooting

## Month 5 — Tools & Practical Networking

* Wireshark
* Packet analysis
* Linux networking
* Network monitoring
* Practical labs

## Month 6 — Integration

* Integrated network lab
* Troubleshooting case study
* Documentation
* Portfolio article
* Project retrospective

Roadmap dapat berubah berdasarkan hasil belajar.

Jangan memaksakan topik hanya karena kalender.

---

# 20. WEEKLY WORKFLOW

## Day 1 — Research & Scope

* pilih pertanyaan
* tentukan tujuan
* tentukan batas artikel

## Day 2 — Lab

* setup
* configuration
* experiment

## Day 3 — Observation

* command output
* packet flow
* troubleshooting
* screenshots

## Day 4 — Writing

* Markdown
* structure
* explanation

## Day 5 — Review

* technical accuracy
* SEO
* GEO/AEO
* screenshot
* Hashnode settings

## Day 6–7 — Buffer

* revision
* publish
* document learning
* prepare next topic

---

# 21. QUALITY GATE

Artikel hanya boleh dipublish setelah melewati:

## Level 1 — Correct

Apakah informasi teknis benar?

## Level 2 — Proven

Apakah hasil praktik memiliki evidence?

## Level 3 — Useful

Apakah pembaca memahami konsep dan alasannya?

Jika salah satu gagal:

> Revise before publishing.

---

# 22. PUBLISHING CHECKLIST

## Content

* [ ] H1 correct
* [ ] Search intent clear
* [ ] Introduction clear
* [ ] Technical explanation verified
* [ ] Commands tested
* [ ] Output matches actual experiment
* [ ] Troubleshooting included where relevant
* [ ] Conclusion included
* [ ] FAQ included
* [ ] What's Next included

## Evidence

* [ ] Topology
* [ ] Relevant screenshots
* [ ] Captions
* [ ] Images readable
* [ ] No fabricated evidence

## SEO

* [ ] SEO title
* [ ] Slug
* [ ] Meta description
* [ ] Primary keyword
* [ ] Secondary keywords
* [ ] Tags
* [ ] Internal links

## GEO/AEO

* [ ] Direct answer
* [ ] Explicit questions
* [ ] Concise answers
* [ ] Clear terminology
* [ ] Evidence

## Hashnode

* [ ] URL
* [ ] Tags
* [ ] SEO title
* [ ] Description
* [ ] OG image
* [ ] Canonical
* [ ] Visibility
* [ ] Scheduling

---

# 23. PROJECT STRUCTURE

Recommended structure:

```text
Artikel-Pribadi-TJKT/
│
├── PROJECT_CONTEXT_TJKT.md
├── ROADMAP_TJKT.md
│
├── articles/
│   ├── 01-network-packet-flow.md
│   ├── 02-ipv4-subnetting.md
│   ├── 03-arp-switching.md
│   └── ...
│
└── assets/
    ├── og/
    └── screenshots/
```

PROJECT_CONTEXT_TJKT.md:

> Project rules and source of truth.

ROADMAP_TJKT.md:

> Long-term progress and planning.

articles/:

> Individual articles.

assets/:

> Images and evidence.

---

# 24. PROGRESS TRACKING

Use:

| Article | Topic               | Lab           | Draft       | Evidence    | SEO   | Review  | Published |
| ------- | ------------------- | ------------- | ----------- | ----------- | ----- | ------- | --------- |
| #1      | Network Packet Flow | Packet Tracer | In Progress | In Progress | Ready | Pending | No        |
| #2      | IPv4 & Subnetting   | TBD           | No          | No          | No    | No      | No        |
| #3      | ARP & Switching     | TBD           | No          | No          | No    | No      | No        |
| #4      | Static Routing      | TBD           | No          | No          | No    | No      | No        |
| #5      | VLAN Fundamentals   | TBD           | No          | No          | No    | No      | No        |
| #6      | Inter-VLAN Routing  | TBD           | No          | No          | No    | No      | No        |

---

# 25. DECISION LOG

Current decisions:

* Hashnode = primary publishing platform
* Markdown = primary drafting format
* TJKT/networking = primary niche
* Cisco Packet Tracer = initial practical environment
* Canva = OG image system
* Real screenshots = practical evidence
* SEO = required for every article
* GEO/AEO = required writing consideration
* Internal linking = required for topic cluster
* First-hand experience = core principle
* Monetization = secondary goal
* Six-month roadmap = initial planning horizon
* Quality > quantity

---

# 26. RULES FOR AI ASSISTANTS

You are assisting with the "Artikel Pribadi TJKT" project.

Treat this document as the project's source of truth.

Before suggesting an article:

1. Check the roadmap.
2. Check existing article topics.
3. Avoid unnecessary topic duplication.
4. Keep the topic aligned with TJKT/networking.
5. Prefer specific technical questions.
6. Consider the current skill progression.

When writing:

1. Follow the project article framework.
2. Prioritize technical accuracy.
3. Never fabricate practical results.
4. Never fabricate screenshots.
5. Never fabricate command output.
6. Clearly separate theory from verified observations.
7. Include SEO metadata.
8. Apply GEO/AEO principles naturally.
9. Suggest useful screenshots.
10. Maintain the project's editorial and visual standards.

When reviewing:

1. Check technical accuracy.
2. Check consistency with the actual lab.
3. Check commands.
4. Check IP/interface/device consistency.
5. Check screenshot relevance.
6. Check SEO.
7. Check GEO/AEO.
8. Check internal linking.
9. Check Hashnode settings.
10. Check whether the article actually provides value.

Do not change established project standards without explaining why.

If a decision is unclear, ask before changing the project standard.

---

# 27. NEW ARTICLE CREATION PROTOCOL

Before starting an article, answer:

1. What is the main question?
2. Who is the reader?
3. What will the reader understand after reading?
4. What practical lab will be used?
5. What evidence will be captured?
6. What is the primary keyword?
7. What is the search intent?
8. What are the secondary concepts?
9. Which existing articles should be linked?
10. What article should come next?

If these questions cannot be answered, the article scope is not ready.

---

# 28. PROJECT CORE PRINCIPLE

> Build it.
>
> Observe it.
>
> Explain it.
>
> Prove it.
>
> Document it.

The project is not simply an article-writing project.

It is a documented progression of TJKT/networking skills.

Every article should contribute at least one of:

* new technical knowledge
* practical experience
* troubleshooting experience
* documentation skill
* portfolio value

The long-term goal is to create a credible technical learning portfolio built from real practice and clear explanations.

```

### Cara memakainya di AI lain

Simpan dengan nama:

**`PROJECT_CONTEXT_TJKT.md`**

Lalu saat membuka AI baru, instruksi pertamanya cukup:

> **"Saya punya proyek Artikel Pribadi TJKT. Baca file `PROJECT_CONTEXT_TJKT.md` ini dan jadikan sebagai source of truth untuk seluruh percakapan proyek. Jangan mengubah keputusan proyek tanpa alasan yang jelas."**

Kemudian **Artikel #1 tetap diberikan sebagai file terpisah**. Jadi AI tidak perlu membaca seluruh histori percakapan kita untuk memahami sistem proyeknya.
```
