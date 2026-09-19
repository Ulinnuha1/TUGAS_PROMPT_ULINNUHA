# USE CASE SPECIFICATION

## Praktikum Prompt AI · Intelligent Mobile and Web Application Development

**Program Studi:** Teknik Informatika
**Tahapan:** PRD → SRS → HLD → LLD
**Proyek:** Sistem Informasi Buku Tamu Digital
**Platform:** Website
**Fitur AI:** Naïve Bayes

---

# 1. Daftar Use Case

| ID    | Nama Use Case                                    | Aktor Utama   | Aktor Pendukung                         | Prioritas   |
| ----- | ------------------------------------------------ | ------------- | --------------------------------------- | ----------- |
| UC-01 | Mencatat Data Kunjungan                          | Tamu          | Database                                | Must Have   |
| UC-02 | Mengelola Data Kunjungan                         | Admin/Petugas | Database                                | Must Have   |
| UC-03 | Menganalisis Data Kunjungan dengan Naïve Bayes ★ | Admin/Petugas | Layanan Inferensi Naïve Bayes, Database | Must Have   |
| UC-04 | Melihat Hasil Klasifikasi Kunjungan ★            | Admin/Petugas | Layanan Inferensi Naïve Bayes, Database | Should Have |

> **Catatan:** UC-03 dan UC-04 menjadi fokus utama karena melibatkan layanan AI.

---

# 2. UC-01 — Mencatat Data Kunjungan

## 2.1 Identitas

**ID:** UC-01
**Nama:** Mencatat Data Kunjungan
**Aktor Utama:** Tamu
**Aktor Pendukung:** Database
**Prioritas:** Must Have
**User Story:** US-01
**FR Asal:** FR-01

## 2.2 Precondition

1. Sistem dapat digunakan melalui platform website.
2. Tamu dapat mengakses fungsi pencatatan kunjungan.
3. Database tersedia untuk menyimpan data.

## 2.3 Postcondition

Data kunjungan berhasil tersimpan dan dapat digunakan oleh sistem untuk pengelolaan serta analisis.

## 2.4 Alur Utama

1. Tamu memulai proses pencatatan kunjungan.
2. Sistem meminta data kunjungan yang diperlukan.
3. Tamu memasukkan data kunjungan.
4. Sistem memeriksa kelengkapan dan validitas data.
5. Sistem menyimpan data kunjungan ke database.
6. Sistem memberikan hasil bahwa data kunjungan telah berhasil dicatat.
7. Data tersedia untuk proses pengelolaan dan analisis.

## 2.5 Alur Alternatif

**A1 — Data tidak lengkap**

1. Sistem menemukan data yang diperlukan belum lengkap.
2. Sistem meminta tamu melengkapi data.
3. Tamu melengkapi data.
4. Sistem melakukan validasi kembali.
5. Proses dilanjutkan ke langkah penyimpanan.

## 2.6 Alur Eksepsi

**E1 — Database tidak tersedia**

1. Sistem gagal menyimpan data ke database.
2. Sistem tidak menganggap data sebagai berhasil tersimpan.
3. Sistem memberikan informasi bahwa proses pencatatan gagal.
4. Data tidak digunakan sebagai data analisis sampai berhasil tersimpan.

---

# 3. UC-02 — Mengelola Data Kunjungan

## 3.1 Identitas

**ID:** UC-02
**Nama:** Mengelola Data Kunjungan
**Aktor Utama:** Admin/Petugas
**Aktor Pendukung:** Database
**Prioritas:** Must Have
**User Story:** US-02, US-03
**FR Asal:** FR-02, FR-03

## 3.2 Precondition

1. Data kunjungan telah tersedia.
2. Admin/Petugas dapat mengakses data kunjungan.
3. Database dapat diakses.

## 3.3 Postcondition

Data kunjungan berhasil ditampilkan atau dikelola sesuai proses yang dilakukan.

## 3.4 Alur Utama

1. Admin/Petugas memulai proses pengelolaan data.
2. Sistem mengambil data kunjungan dari database.
3. Sistem menampilkan data kunjungan yang tersedia.
4. Admin/Petugas memilih data yang akan dikelola.
5. Sistem memproses perubahan data sesuai tindakan yang dilakukan.
6. Sistem menyimpan perubahan ke database.
7. Sistem memastikan data terbaru tersedia untuk proses berikutnya.

## 3.5 Alur Alternatif

**A1 — Data yang dicari tidak tersedia**

1. Admin/Petugas meminta data tertentu.
2. Sistem melakukan pencarian pada database.
3. Sistem tidak menemukan data yang sesuai.
4. Sistem memberikan informasi bahwa data tidak ditemukan.
5. Admin/Petugas dapat melakukan pencarian kembali.

## 3.6 Alur Eksepsi

**E1 — Database gagal diakses**

1. Sistem tidak dapat mengambil atau menyimpan data.
2. Sistem menghentikan proses pengelolaan.
3. Sistem memberikan informasi bahwa proses tidak dapat diselesaikan.
4. Data yang belum berhasil disimpan tidak dianggap sebagai perubahan yang berhasil.

---

# 4. UC-03 — Menganalisis Data Kunjungan dengan Naïve Bayes ★

## 4.1 Identitas

**ID:** UC-03
**Nama:** Menganalisis Data Kunjungan dengan Naïve Bayes
**Aktor Utama:** Admin/Petugas
**Aktor Pendukung:** Layanan Inferensi Naïve Bayes, Database
**Prioritas:** Must Have
**User Story:** US-05 ★
**FR Asal:** FR-05

## 4.2 Tujuan

Menghasilkan klasifikasi berdasarkan data kunjungan menggunakan metode Naïve Bayes sehingga hasil analisis dapat digunakan sebagai informasi tambahan dalam memahami pola data kunjungan.

## 4.3 Precondition

1. Data kunjungan tersedia di database.
2. Variabel dan kelas klasifikasi telah ditentukan berdasarkan data kunjungan.
3. Data memiliki jumlah dan kualitas yang memenuhi kebutuhan analisis.
4. Layanan inferensi Naïve Bayes tersedia.

## 4.4 Postcondition

1. Sistem memperoleh hasil klasifikasi dari model Naïve Bayes.
2. Hasil klasifikasi disimpan atau tersedia untuk ditampilkan.
3. Jika model tidak dapat memberikan hasil yang memenuhi ambang keyakinan, sistem tidak menggunakan hasil tersebut sebagai klasifikasi yang valid.

## 4.5 Alur Utama

1. Admin/Petugas memulai proses analisis data kunjungan.
2. Sistem mengambil data kunjungan yang diperlukan dari database.
3. Sistem memeriksa kelengkapan dan kualitas data yang akan digunakan.
4. Sistem menyiapkan data sesuai variabel dan kelas yang telah ditentukan.
5. Sistem mengirimkan data ke layanan inferensi Naïve Bayes.
6. Layanan inferensi memproses data.
7. Layanan inferensi mengembalikan hasil klasifikasi beserta skor keyakinan.
8. Sistem memeriksa skor keyakinan terhadap ambang batas yang ditentukan.
9. Jika skor memenuhi ambang batas, sistem menerima hasil klasifikasi.
10. Sistem menyimpan atau meneruskan hasil klasifikasi untuk ditampilkan.
11. Proses analisis selesai.

---

## 4.6 Alur Alternatif

### A1 — Jumlah Data Belum Memadai

1. Sistem memeriksa data yang tersedia.
2. Sistem menemukan jumlah data belum memenuhi kebutuhan analisis.
3. Sistem tidak menjalankan inferensi.
4. Sistem memberikan informasi bahwa analisis belum dapat dilakukan.
5. Admin/Petugas dapat menjalankan analisis setelah data mencukupi.

### A2 — Data Tidak Lengkap

1. Sistem menemukan sebagian variabel yang diperlukan tidak tersedia.
2. Sistem mengidentifikasi data yang tidak lengkap.
3. Sistem tidak mengirim data yang tidak memenuhi persyaratan ke layanan inferensi.
4. Sistem memberikan informasi mengenai data yang perlu dilengkapi.

---

# 4.7 Alur Eksepsi Khusus AI

### E-AI-01 — Kualitas Masukan Data Rendah

**Kondisi:** Data yang akan digunakan untuk inferensi memiliki kualitas yang tidak memenuhi persyaratan.

1. Sistem melakukan pemeriksaan kualitas data sebelum inferensi.
2. Sistem mendeteksi data yang kualitasnya rendah atau tidak memenuhi persyaratan.
3. Sistem menghentikan proses pengiriman data ke layanan AI.
4. Sistem memberikan informasi bahwa data belum layak digunakan untuk analisis.
5. Data tidak digunakan untuk menghasilkan klasifikasi.

**Fallback:**
Sistem menggunakan informasi data yang valid saja apabila aturan analisis mengizinkannya. Jika tidak memungkinkan, proses dihentikan sampai data memenuhi persyaratan.

---

### E-AI-02 — Timeout atau Gagal Koneksi ke Layanan AI

**Kondisi:** Permintaan inferensi tidak memperoleh respons dalam batas waktu NFR atau terjadi kegagalan koneksi.

1. Sistem mengirimkan permintaan inferensi ke layanan AI.
2. Sistem menunggu respons sampai batas waktu yang ditentukan.
3. Layanan AI tidak memberikan respons atau koneksi gagal.
4. Sistem menandai proses inferensi sebagai gagal.
5. Sistem tidak menampilkan hasil AI sebagai hasil klasifikasi yang valid.
6. Sistem memberikan informasi bahwa analisis AI belum dapat diselesaikan.
7. Data kunjungan tetap tersimpan dan tidak dihapus akibat kegagalan layanan AI.

**Fallback:**
Sistem mempertahankan data kunjungan dan memungkinkan proses analisis dilakukan kembali ketika layanan AI tersedia.

---

### E-AI-03 — Skor Keyakinan Model Rendah

**Kondisi:** Hasil inferensi memiliki skor keyakinan di bawah ambang batas yang ditentukan dalam SRS.

1. Layanan AI mengembalikan hasil klasifikasi dan skor keyakinan.
2. Sistem membandingkan skor keyakinan dengan ambang batas.
3. Sistem menemukan skor berada di bawah ambang batas.
4. Sistem tidak menetapkan hasil tersebut sebagai klasifikasi yang valid.
5. Sistem memberikan informasi bahwa hasil analisis memiliki tingkat keyakinan rendah.
6. Sistem dapat meminta analisis ulang setelah data yang digunakan memenuhi kondisi yang lebih sesuai.

**Fallback:**
Hasil dengan low confidence tidak digunakan sebagai hasil klasifikasi final.

---

# 5. UC-04 — Melihat Hasil Klasifikasi Kunjungan ★

## 5.1 Identitas

**ID:** UC-04
**Nama:** Melihat Hasil Klasifikasi Kunjungan
**Aktor Utama:** Admin/Petugas
**Aktor Pendukung:** Database, Layanan Inferensi Naïve Bayes
**Prioritas:** Should Have
**User Story:** US-06 ★
**FR Asal:** FR-06

## 5.2 Precondition

1. Data kunjungan telah tersedia.
2. Proses klasifikasi telah berhasil dilakukan.
3. Hasil klasifikasi tersedia.
4. Hasil dengan skor keyakinan rendah tidak dianggap sebagai hasil klasifikasi valid.

## 5.3 Postcondition

Admin/Petugas memperoleh informasi hasil klasifikasi yang dapat digunakan untuk memahami data kunjungan.

## 5.4 Alur Utama

1. Admin/Petugas meminta hasil analisis data kunjungan.
2. Sistem mengambil hasil klasifikasi dari penyimpanan data.
3. Sistem memeriksa ketersediaan hasil klasifikasi.
4. Sistem memeriksa status validitas hasil.
5. Sistem memberikan hasil klasifikasi yang valid.
6. Admin/Petugas dapat menggunakan informasi tersebut untuk memahami pola data kunjungan.

## 5.5 Alur Alternatif

### A1 — Belum Ada Hasil Klasifikasi

1. Admin/Petugas meminta hasil analisis.
2. Sistem tidak menemukan hasil klasifikasi.
3. Sistem memberikan informasi bahwa analisis belum tersedia.
4. Admin/Petugas dapat menjalankan proses analisis.

### A2 — Hasil Tidak Valid

1. Sistem menemukan hasil dengan status tidak valid.
2. Sistem tidak menggunakan hasil tersebut sebagai klasifikasi final.
3. Sistem memberikan informasi bahwa hasil analisis belum dapat digunakan.

---

# 5.6 Alur Eksepsi Khusus AI

### E-AI-01 — Data Pendukung Tidak Layak

1. Sistem memeriksa data yang menjadi dasar hasil klasifikasi.
2. Sistem menemukan data tidak memenuhi persyaratan.
3. Sistem tidak menggunakan hasil tersebut.
4. Sistem memberikan informasi bahwa hasil analisis tidak tersedia untuk digunakan.

### E-AI-02 — Layanan AI Tidak Tersedia

1. Admin/Petugas meminta proses analisis baru.
2. Sistem mencoba mengakses layanan AI.
3. Koneksi gagal atau layanan mengalami timeout.
4. Sistem mempertahankan hasil sebelumnya jika masih tersedia dan valid.
5. Jika tidak ada hasil valid, sistem menyatakan bahwa hasil analisis belum tersedia.
6. Sistem tidak membuat hasil klasifikasi baru tanpa respons dari layanan AI.

### E-AI-03 — Low Confidence

1. Sistem menerima hasil inferensi dengan skor keyakinan.
2. Sistem membandingkan skor dengan ambang batas.
3. Skor berada di bawah ambang batas.
4. Sistem menandai hasil sebagai low confidence.
5. Sistem tidak menyajikannya sebagai klasifikasi final.

---

# 6. Kaitan Use Case dengan User Story dan FR

| Use Case | User Story   | FR Asal      | Fitur                              |
| -------- | ------------ | ------------ | ---------------------------------- |
| UC-01    | US-01        | FR-01        | Pencatatan buku tamu               |
| UC-02    | US-02, US-03 | FR-02, FR-03 | Pengelolaan data kunjungan         |
| UC-03    | US-05 ★      | FR-05        | Analisis Naïve Bayes ★             |
| UC-04    | US-06 ★      | FR-06        | Hasil klasifikasi pada dashboard ★ |

---

# 7. Aktor Sistem

| Aktor                         | Jenis           | Peran                                                               |
| ----------------------------- | --------------- | ------------------------------------------------------------------- |
| Tamu                          | Aktor Utama     | Memberikan data kunjungan kepada sistem.                            |
| Admin/Petugas                 | Aktor Utama     | Mengelola data dan menggunakan hasil analisis kunjungan.            |
| Database                      | Aktor Pendukung | Menyediakan dan menyimpan data kunjungan serta hasil analisis.      |
| Layanan Inferensi Naïve Bayes | Aktor Pendukung | Memproses data dan menghasilkan klasifikasi beserta skor keyakinan. |

---

# 8. Parameter AI dan NFR

Parameter berikut harus mengikuti nilai yang telah ditetapkan pada `srs.md`.

| Parameter                         | Nilai                                                                                     |
| --------------------------------- | ----------------------------------------------------------------------------------------- |
| Metode AI                         | Naïve Bayes                                                                               |
| Input AI                          | Data/variabel kunjungan yang ditentukan dalam SRS                                         |
| Output AI                         | Kelas/hasil klasifikasi dan skor keyakinan                                                |
| Ambang Low Confidence             | Mengikuti NFR/SRS                                                                         |
| Batas Latensi AI                  | Mengikuti NFR/SRS                                                                         |
| Toleransi Error/Kegagalan Koneksi | Mengikuti NFR/SRS                                                                         |
| Fallback                          | Tidak menggunakan hasil AI yang gagal atau low confidence sebagai hasil klasifikasi final |

> **Catatan:** Nilai numerik untuk latensi, ambang confidence, dan toleransi error tidak ditentukan di dokumen ini agar tidak menambahkan kebutuhan yang belum memiliki dasar pada SRS.

---

# 9. Checklist Review Tahap 2

* [x] Layanan inferensi AI dicatat sebagai aktor pendukung.
* [x] Database dicatat sebagai aktor pendukung.
* [x] Alur utama memiliki langkah berurutan dari awal sampai selesai.
* [x] Alur alternatif mencakup variasi input yang wajar.
* [x] Kualitas data rendah ditangani sebelum inferensi.
* [x] Timeout/gagal koneksi AI memiliki penanganan.
* [x] Low confidence memiliki penanganan.
* [x] Hasil AI yang gagal tidak dianggap sebagai klasifikasi valid.
* [x] Tidak membahas detail tombol, layout, atau implementasi coding.
* [x] Use Case dikaitkan dengan User Story dan FR asal.
* [ ] Nilai latensi, confidence threshold, dan toleransi error harus dicocokkan dengan NFR pada `srs.md`.

---

# 10. Catatan Traceability

Dokumen Use Case ini diturunkan dari User Story dan Functional Requirements. Detail teknis mengenai arsitektur layanan AI, database, API, komponen sistem, struktur kelas, dan rancangan antarmuka tidak dibahas karena menjadi bagian dari tahap **HLD dan LLD**.
