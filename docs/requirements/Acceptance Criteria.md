# ACCEPTANCE CRITERIA

## Praktikum Prompt AI · Intelligent Mobile and Web Application Development

**Program Studi:** Teknik Informatika
**Tahapan:** PRD → SRS → HLD → LLD
**Proyek:** Sistem Informasi Buku Tamu Digital
**Platform:** Website
**Metode AI:** Naïve Bayes

---

# 1. Tujuan

Dokumen ini mendefinisikan **Acceptance Criteria** untuk setiap User Story menggunakan pola **Given-When-Then**.

Acceptance Criteria digunakan untuk memastikan bahwa setiap User Story memiliki kondisi pengujian yang jelas, terukur, dan dapat diverifikasi.

### Parameter NFR dari SRS

| Parameter         | Nilai                    |
| ----------------- | ------------------------ |
| Batas latensi AI  | `[NFR-AI-LATENCY] detik` |
| Target akurasi AI | `[NFR-AI-ACCURACY]%`     |
| Ambang confidence | `[NFR-AI-CONFIDENCE]`    |
| Batas timeout     | `[NFR-AI-TIMEOUT] detik` |
| Pesan error AI    | `[PESAN-ERROR-SRS]`      |

> **Catatan:** Nilai di atas harus diganti dengan nilai aktual dari `srs.md`. Jangan menetapkan angka baru tanpa dasar dari SRS.

---

# 2. US-01 — Mencatat Data Kunjungan

**User Story:**

> Sebagai **tamu**, saya ingin mengisi data kunjungan secara digital, agar proses pencatatan kunjungan dapat dilakukan tanpa pencatatan manual.

**FR Asal:** FR-01
**Prioritas:** Must Have
**Kategori:** Fitur Inti

## Scenario 1 — Data kunjungan berhasil dicatat

```gherkin
Scenario: Tamu berhasil mencatat data kunjungan
Given sistem dapat diakses dan seluruh data kunjungan yang diwajibkan tersedia
When tamu mengirimkan data kunjungan yang lengkap dan valid
Then sistem menyimpan data kunjungan ke database
And sistem memberikan status bahwa pencatatan berhasil
```

**Metode uji:** Integration Test + User Acceptance Test

## Scenario 2 — Data kunjungan tidak lengkap

```gherkin
Scenario: Sistem menolak data kunjungan yang tidak lengkap
Given tamu sedang melakukan pencatatan kunjungan
When tamu mengirimkan data yang belum lengkap
Then sistem tidak menyimpan data sebagai data kunjungan yang valid
And sistem meminta data yang belum lengkap untuk dilengkapi
```

**Metode uji:** Unit Test + Integration Test

---

# 3. US-02 — Melihat Data Kunjungan

**User Story:**

> Sebagai **admin/petugas**, saya ingin melihat data kunjungan yang telah dicatat, agar saya dapat mengetahui dan memantau riwayat kunjungan tamu.

**FR Asal:** FR-02
**Prioritas:** Must Have
**Kategori:** Fitur Inti

## Scenario 1 — Data kunjungan tersedia

```gherkin
Scenario: Admin melihat data kunjungan yang tersimpan
Given database memiliki data kunjungan yang valid
When admin/petugas meminta data kunjungan
Then sistem mengambil data dari database
And sistem menampilkan data kunjungan yang tersedia
```

**Metode uji:** Integration Test + User Acceptance Test

## Scenario 2 — Data kunjungan tidak tersedia

```gherkin
Scenario: Tidak terdapat data kunjungan
Given database tidak memiliki data kunjungan
When admin/petugas meminta data kunjungan
Then sistem tidak menampilkan data yang tidak tersedia
And sistem memberikan informasi bahwa data kunjungan belum tersedia
```

**Metode uji:** Integration Test

---

# 4. US-03 — Mengelola Data Kunjungan

**User Story:**

> Sebagai **admin/petugas**, saya ingin mengelola data kunjungan, agar data yang tersimpan tetap dapat dikelola sesuai kebutuhan administrasi.

**FR Asal:** FR-03
**Prioritas:** Must Have
**Kategori:** Fitur Inti

## Scenario 1 — Data berhasil dikelola

```gherkin
Scenario: Admin berhasil mengelola data kunjungan
Given data kunjungan tersedia di database
When admin/petugas melakukan perubahan yang valid terhadap data kunjungan
Then sistem menyimpan perubahan ke database
And data terbaru tersedia pada sistem
```

**Metode uji:** Integration Test

## Scenario 2 — Data yang dikelola tidak ditemukan

```gherkin
Scenario: Admin mencoba mengelola data yang tidak tersedia
Given data kunjungan yang diminta tidak terdapat di database
When admin/petugas melakukan pengelolaan terhadap data tersebut
Then sistem tidak melakukan perubahan pada database
And sistem memberikan informasi bahwa data tidak ditemukan
```

**Metode uji:** Integration Test

---

# 5. US-04 — Melihat Dashboard Analitik

**User Story:**

> Sebagai **admin/petugas**, saya ingin melihat ringkasan data kunjungan melalui dashboard, agar pola dan informasi kunjungan dapat dipantau dengan lebih terstruktur.

**FR Asal:** FR-04
**Prioritas:** Must Have
**Kategori:** Fitur Inti

## Scenario 1 — Dashboard menampilkan data

```gherkin
Scenario: Dashboard menampilkan ringkasan data kunjungan
Given database memiliki data kunjungan yang valid
When admin/petugas meminta informasi analitik kunjungan
Then sistem mengambil data yang diperlukan
And sistem menampilkan ringkasan berdasarkan data kunjungan
```

**Metode uji:** Integration Test + User Acceptance Test

## Scenario 2 — Data belum tersedia

```gherkin
Scenario: Dashboard tidak memiliki data untuk dianalisis
Given database tidak memiliki data kunjungan yang dapat dianalisis
When admin/petugas meminta informasi analitik
Then sistem tidak menghasilkan analisis dari data yang tidak tersedia
And sistem memberikan informasi bahwa data belum tersedia
```

**Metode uji:** Integration Test

---

# 6. US-05 ★ — Menganalisis Data dengan Naïve Bayes

**User Story:**

> Sebagai **admin/petugas**, saya ingin mendapatkan hasil klasifikasi menggunakan Naïve Bayes berdasarkan data kunjungan, agar saya dapat memperoleh informasi pola atau kategori kunjungan dari data yang tersedia.

**FR Asal:** FR-05
**Prioritas:** Must Have
**Kategori:** Fitur AI ★

---

## Scenario 1 — Happy Path: Klasifikasi berhasil

```gherkin
Scenario: Sistem berhasil melakukan klasifikasi Naïve Bayes
Given data kunjungan tersedia dan memenuhi persyaratan analisis
And layanan inferensi Naïve Bayes dapat diakses
When admin/petugas menjalankan proses analisis
Then sistem mengirim data yang valid ke layanan inferensi
And layanan AI mengembalikan hasil klasifikasi dan skor confidence
And skor confidence >= [NFR-AI-CONFIDENCE]
And sistem menerima hasil sebagai klasifikasi yang valid
And waktu respons tidak melebihi [NFR-AI-TIMEOUT] detik
```

**Metode uji:** Integration Test

---

## Scenario 2 — Edge Case: Data masukan tidak memenuhi persyaratan

```gherkin
Scenario: Sistem menolak data yang tidak memenuhi persyaratan analisis
Given data kunjungan tidak lengkap atau tidak memenuhi persyaratan input Naïve Bayes
When admin/petugas menjalankan proses analisis
Then sistem tidak mengirim data yang tidak memenuhi persyaratan ke layanan AI
And sistem memberikan informasi bahwa data perlu dilengkapi atau diperbaiki
And tidak ada hasil klasifikasi yang ditetapkan
```

**Metode uji:** Unit Test + Integration Test

---

## Scenario 3 — Low Confidence

```gherkin
Scenario: Hasil klasifikasi memiliki confidence di bawah ambang batas
Given data kunjungan berhasil diproses oleh layanan Naïve Bayes
When layanan AI mengembalikan skor confidence < [NFR-AI-CONFIDENCE]
Then sistem menandai hasil sebagai low confidence
And sistem tidak menetapkan hasil tersebut sebagai klasifikasi final
And sistem memberikan informasi bahwa hasil analisis memiliki tingkat keyakinan rendah
```

**Metode uji:** Integration Test

---

## Scenario 4 — AI Timeout atau Gagal Koneksi

```gherkin
Scenario: Layanan AI tidak memberikan respons dalam batas waktu
Given data kunjungan telah lolos validasi
And sistem telah mengirim permintaan ke layanan inferensi Naïve Bayes
When layanan AI tidak memberikan respons dalam waktu <= [NFR-AI-TIMEOUT] detik atau koneksi gagal
Then sistem menghentikan penantian terhadap permintaan tersebut
And sistem tidak menetapkan hasil klasifikasi baru
And sistem menampilkan pesan "[PESAN-ERROR-SRS]"
And data kunjungan tetap tersimpan
And pengguna dapat mencoba proses analisis kembali
```

**Metode uji:** Integration Test

---

# 7. US-06 ★ — Melihat Hasil Klasifikasi

**User Story:**

> Sebagai **admin/petugas**, saya ingin melihat hasil klasifikasi Naïve Bayes pada dashboard, agar informasi hasil analisis dapat digunakan sebagai bahan memahami data kunjungan.

**FR Asal:** FR-06
**Prioritas:** Should Have
**Kategori:** Fitur AI ★

---

## Scenario 1 — Hasil klasifikasi valid tersedia

```gherkin
Scenario: Admin melihat hasil klasifikasi yang valid
Given proses Naïve Bayes telah menghasilkan klasifikasi dengan confidence >= [NFR-AI-CONFIDENCE]
When admin/petugas meminta hasil analisis
Then sistem mengambil hasil klasifikasi yang valid
And sistem menampilkan hasil klasifikasi
And hasil yang ditampilkan merupakan hasil dari proses inferensi yang berhasil
```

**Metode uji:** Integration Test + User Acceptance Test

---

## Scenario 2 — Hasil klasifikasi low confidence

```gherkin
Scenario: Sistem tidak menetapkan hasil low confidence sebagai klasifikasi final
Given hasil Naïve Bayes tersedia
And skor confidence < [NFR-AI-CONFIDENCE]
When admin/petugas meminta hasil klasifikasi
Then sistem tidak menetapkan hasil tersebut sebagai klasifikasi final
And sistem memberikan informasi bahwa hasil analisis memiliki confidence rendah
```

**Metode uji:** Integration Test

---

## Scenario 3 — Hasil analisis belum tersedia karena AI gagal

```gherkin
Scenario: Hasil klasifikasi tidak tersedia karena layanan AI gagal
Given data kunjungan tersedia
And layanan AI mengalami timeout atau gagal koneksi
When admin/petugas meminta hasil analisis
Then sistem tidak membuat hasil klasifikasi baru
And sistem memberikan informasi bahwa hasil analisis belum tersedia
And data kunjungan tetap dapat diakses
And admin/petugas dapat mencoba proses analisis kembali
```

**Metode uji:** Integration Test + User Acceptance Test

---

# 8. Ringkasan Acceptance Criteria

| User Story | Normal | Edge Case | Failure/Timeout | Metode Utama      |
| ---------- | -----: | --------: | --------------: | ----------------- |
| US-01      |      ✓ |         ✓ |               - | Integration + UAT |
| US-02      |      ✓ |         ✓ |               - | Integration + UAT |
| US-03      |      ✓ |         ✓ |               - | Integration       |
| US-04      |      ✓ |         ✓ |               - | Integration + UAT |
| US-05 ★    |      ✓ |         ✓ |               ✓ | Integration       |
| US-06 ★    |      ✓ |         ✓ |               ✓ | Integration + UAT |

---

# 9. Traceability

| Acceptance Criteria | User Story | FR    | Use Case | NFR Terkait       |
| ------------------- | ---------- | ----- | -------- | ----------------- |
| AC-01               | US-01      | FR-01 | UC-01    | NFR Usability     |
| AC-02               | US-02      | FR-02 | UC-02    | NFR Performance   |
| AC-03               | US-03      | FR-03 | UC-02    | NFR Security      |
| AC-04               | US-04      | FR-04 | UC-04    | NFR Performance   |
| AC-05               | US-05 ★    | FR-05 | UC-03    | NFR AI Accuracy   |
| AC-06               | US-05 ★    | FR-05 | UC-03    | NFR AI Latency    |
| AC-07               | US-05 ★    | FR-05 | UC-03    | NFR AI Confidence |
| AC-08               | US-05 ★    | FR-05 | UC-03    | NFR AI Fallback   |
| AC-09               | US-06 ★    | FR-06 | UC-04    | NFR AI Accuracy   |
| AC-10               | US-06 ★    | FR-06 | UC-04    | NFR AI Fallback   |

---

# 10. Checklist Review Tahap 4

* [x] Semua skenario menggunakan **Given, When, Then**.
* [x] Setiap User Story memiliki minimal 2 skenario.
* [x] User Story AI ★ memiliki skenario normal.
* [x] User Story AI ★ memiliki skenario edge case.
* [x] User Story AI ★ memiliki skenario kegagalan/timeout.
* [x] Low confidence memiliki kriteria pengujian.
* [x] Kegagalan koneksi AI memiliki kriteria pengujian.
* [x] Tidak menggunakan istilah subjektif seperti "cepat" atau "akurat" tanpa ukuran.
* [x] Metode pengujian dicantumkan.
* [x] Data tetap dipertahankan ketika inferensi AI gagal.
* [ ] Nilai `[NFR-AI-TIMEOUT]` harus disesuaikan dengan SRS.
* [ ] Nilai `[NFR-AI-CONFIDENCE]` harus disesuaikan dengan SRS.
* [ ] Nilai `[NFR-AI-ACCURACY]` harus disesuaikan dengan SRS.
* [ ] `[PESAN-ERROR-SRS]` harus diganti dengan pesan error yang ditetapkan pada SRS.

---

# 11. Catatan Validasi

Acceptance Criteria ini hanya dapat dianggap final setelah seluruh placeholder NFR diganti dengan nilai yang benar-benar terdapat pada `srs.md`.

Khusus fitur AI, pengujian harus membedakan antara:

```text
Data valid
    ↓
Inferensi berhasil
    ↓
Confidence memenuhi threshold
    ↓
Hasil valid
```

dan:

```text
Data tidak valid
       ↓
Tidak dilakukan inferensi
```

serta:

```text
Inferensi gagal / timeout
       ↓
Tidak ada klasifikasi baru
       ↓
Fallback
```

dan:

```text
Inferensi berhasil
       ↓
Confidence < threshold
       ↓
Hasil low confidence
       ↓
Tidak menjadi klasifikasi final
```

Dengan demikian, keberhasilan fitur AI tidak hanya dinilai dari apakah model mengembalikan hasil, tetapi juga dari **kualitas input, confidence, batas waktu respons, dan penanganan kegagalan**.
