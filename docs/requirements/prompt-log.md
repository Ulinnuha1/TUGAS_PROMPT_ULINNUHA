# Prompt Log

Dokumen ini berisi riwayat penggunaan prompt dalam proses penyusunan dokumen kebutuhan perangkat lunak untuk proyek **Sistem Informasi Buku Tamu Digital**.

## 1. Informasi Proyek

| Informasi   | Keterangan                                                                                                                               |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Nama Proyek | Sistem Informasi Buku Tamu Digital                                                                                                       |
| Judul       | Pengembangan Sistem Informasi Buku Tamu Digital Berbasis Website dengan Dashboard Analitik Data Kunjungan Menggunakan Metode Naïve Bayes |
| Mata Kuliah | Intelligent Mobile and Web Application Development                                                                                       |
| Fokus       | Penyusunan PRD dan SRS                                                                                                                   |
| Platform    | Website                                                                                                                                  |
| Metode AI   | Naïve Bayes                                                                                                                              |

---

## 2. Prompt Penyusunan PRD

### Prompt 01 — Penyusunan PRD

**Tujuan:**
Menyusun Product Requirements Document (PRD) yang menjelaskan masalah, pengguna, tujuan produk, fitur, prioritas, KPI, serta kebutuhan penggunaan metode Naïve Bayes.

**Prompt:**

> Buatkan PRD untuk proyek "Pengembangan Sistem Informasi Buku Tamu Digital Berbasis Website dengan Dashboard Analitik Data Kunjungan Menggunakan Metode Naïve Bayes".
>
> PRD harus mencakup:
>
> * Problem Statement
> * Masalah yang ingin diselesaikan
> * Bukti riset
> * Fakta dan asumsi
> * Target user dan stakeholder
> * Persona pengguna
> * Value Proposition
> * Peran Naïve Bayes dan alasan penggunaannya
> * KPI
> * Prioritas fitur menggunakan metode MoSCoW
> * Fitur utama sistem
>
> Pastikan kebutuhan yang ditulis berdasarkan informasi dan hasil riset yang tersedia. Tandai bagian yang masih berupa asumsi dan jangan membuat klaim yang tidak memiliki dasar.

**Hasil:**
Menghasilkan dokumen `docs/requirements/prd.md` sebagai dasar penyusunan SRS.

---

## 3. Review dan Revisi PRD

### Prompt 02 — Revisi Asumsi PRD

**Tujuan:**
Memperjelas bagian asumsi agar dapat dibedakan dari fakta yang diperoleh dari riset.

**Prompt:**

> Revisi bagian asumsi pada PRD menjadi 5 asumsi yang jelas dan dapat digunakan sebagai dasar pengembangan SRS. Jangan menggunakan kolom status.
>
> Gunakan format:
>
> * ASUMSI-01
> * ASUMSI-02
> * ASUMSI-03
> * ASUMSI-04
> * ASUMSI-05

**Hasil revisi:**

* **ASUMSI-01:** Pengguna terdiri dari tamu dan admin/petugas.
* **ASUMSI-02:** Data kunjungan tersedia dalam jumlah yang dapat digunakan untuk analisis.
* **ASUMSI-03:** Variabel dan kelas Naïve Bayes ditentukan berdasarkan data kunjungan.
* **ASUMSI-04:** Sistem utama digunakan melalui platform website.
* **ASUMSI-05:** Hasil klasifikasi/prediksi Naïve Bayes dapat ditampilkan pada dashboard.

---

## 4. Prompt Penyusunan SRS

### Prompt 03 — PRD → SRS

**Tujuan:**
Mengubah PRD menjadi Software Requirements Specification (SRS) tanpa menambahkan kebutuhan yang tidak memiliki dasar dari PRD atau hasil riset.

**Prompt:**

> Kamu adalah requirements analyst senior.
>
> Ubah PRD hasil revisi menjadi DRAF SRS ringkas.
>
> Acuan kualitas: ISO/IEC 25010 dengan memilih karakteristik yang relevan.
>
> Prioritas kebutuhan menggunakan MoSCoW.
>
> Platform: Website.
>
> SRS harus mencakup:
>
> 1. Tujuan, scope, dan definisi istilah.
> 2. User dan stakeholder, lingkungan operasi, asumsi dan dependensi.
> 3. Functional Requirements (FR-01 sampai FR-n) dengan format:
>    "Sistem harus dapat <aksi> <objek> saat <kondisi> → <output>"
>    serta kolom ID, prioritas MoSCoW, dan metode verifikasi.
> 4. Non-Functional Requirements (NFR-01 sampai NFR-m) berdasarkan ISO/IEC 25010 yang mencakup metrik, target, dan kondisi pengukuran.
> 5. Kebutuhan data minimum untuk fitur AI, dari input sampai output model.
> 6. Aturan bisnis berdasarkan hasil riset.
> 7. Matriks traceability antara FR/NFR dengan fitur pada PRD.
>
> Wajib memuat kebutuhan terkait akurasi dan latensi AI, keamanan, privasi, usability, serta fallback AI.
>
> Setiap FR dan NFR harus dapat ditelusuri ke bukti pada PRD atau riset. Jangan menambahkan kebutuhan tanpa bukti.
>
> Jika pembahasan mulai masuk ke arsitektur atau UI, hentikan karena hal tersebut merupakan bagian HLD/LLD.

**Hasil:**
Menghasilkan dokumen `docs/requirements/srs.md`.

---

## 5. Review SRS

### Prompt 04 — Review Requirements

**Tujuan:**
Memeriksa kelengkapan dan keterujian kebutuhan pada SRS.

**Prompt:**

> Review SRS yang telah dibuat menggunakan checklist berikut:
>
> * Semua FR/NFR harus testable.
> * Tidak menggunakan istilah seperti "cepat", "mudah", atau "aman" tanpa metrik atau kriteria yang dapat diuji.
> * NFR AI harus mencakup akurasi, latensi, privasi, dan fallback.
> * Setiap FR/NFR harus dapat ditelusuri ke fitur PRD dan problem statement.
> * Metode verifikasi harus realistis untuk dikerjakan dalam satu semester.
> * Semua asumsi harus ditandai.
> * Jangan menambahkan kebutuhan baru yang tidak memiliki dasar pada PRD atau riset.

**Checklist hasil review:**

* [ ] Semua FR dapat diuji.
* [ ] Semua NFR memiliki metrik dan target.
* [ ] Akurasi AI tercantum.
* [ ] Latensi AI tercantum.
* [ ] Keamanan tercantum.
* [ ] Privasi tercantum.
* [ ] Fallback AI tercantum.
* [ ] Traceability PRD → SRS tersedia.
* [ ] Asumsi ditandai.
* [ ] Tidak terdapat pembahasan HLD/LLD.

---

## 6. Alur Penyusunan Dokumen

```text
Hasil Riset
    ↓
PRD
    ↓
Review & Revisi PRD
    ↓
SRS
    ↓
Review Requirements
    ↓
Dokumen Requirements Final
```

## 7. Struktur File

```text
docs/
└── requirements/
    ├── prd.md
    ├── srs.md
    └── prompt-log.md
```

## 8. Catatan

Prompt digunakan sebagai alat bantu dalam proses penyusunan dokumentasi kebutuhan. Hasil dari setiap prompt tetap melalui proses review untuk memastikan kebutuhan yang ditulis sesuai dengan hasil riset, dapat diuji, memiliki prioritas, dan dapat ditelusuri kembali ke PRD.
