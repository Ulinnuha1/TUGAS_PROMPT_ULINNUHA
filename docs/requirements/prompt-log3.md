# Prompt Log

## Informasi Proyek

| Keterangan      | Detail                                                                           |
| --------------- | -------------------------------------------------------------------------------- |
| Nama Proyek     | Sistem Informasi Buku Tamu Digital                                               |
| Mata Kuliah     | Intelligent Mobile and Web Application Development                               |
| Pertemuan       | Pertemuan 02 — PRD → SRS                                                         |
| Platform        | Website                                                                          |
| Metode Analisis | Naïve Bayes                                                                      |
| Tujuan          | Mendokumentasikan proses penggunaan AI dalam penyusunan dokumen kebutuhan sistem |

---

## 1. Tujuan Prompt Log

Prompt Log digunakan untuk mencatat proses penggunaan AI dalam penyusunan dokumen proyek, mulai dari pemberian prompt, hasil draf awal yang dihasilkan AI, hingga koreksi dan penyesuaian yang dilakukan secara manual oleh tim.

Dokumen ini digunakan sebagai catatan proses dan membantu memastikan bahwa hasil akhir tetap sesuai dengan kebutuhan proyek.

---

# 2. Prompt 01 — Penyusunan PRD

### Prompt yang Dikirim ke AI

```text
Buatkan Product Requirements Document (PRD) untuk proyek
"Sistem Informasi Buku Tamu Digital Berbasis Website dengan
Dashboard Analitik Data Kunjungan Menggunakan Metode Naïve Bayes".

PRD harus mencakup:
1. Problem Statement
2. Target User dan Stakeholder
3. Persona
4. Value Proposition
5. KPI
6. MoSCoW Prioritization
7. Fitur Utama

Gunakan bahasa Indonesia yang jelas dan sesuai dengan kebutuhan
proyek akademik.
```

### Draf Awal Hasil Generate

AI menghasilkan struktur PRD yang mencakup masalah pencatatan tamu secara manual, target pengguna, persona, manfaat sistem, KPI, prioritas fitur, serta penggunaan Naïve Bayes untuk analisis data kunjungan.

### Koreksi Manual Tim

* Menyesuaikan nama dan deskripsi proyek.
* Mengubah bahasa agar lebih sederhana dan natural.
* Memastikan target pengguna hanya mencakup **Tamu** dan **Admin/Petugas**.
* Menambahkan dashboard analitik sebagai fitur utama.
* Memastikan penggunaan Naïve Bayes memiliki tujuan yang jelas dan bukan sekadar fitur tambahan.
* Memisahkan fakta proyek dan asumsi agar tidak tercampur.
* Menghindari klaim yang belum memiliki dasar atau bukti.

---

# 3. Prompt 02 — Penyusunan Asumsi PRD

### Prompt yang Dikirim ke AI

```text
Buatkan bagian asumsi untuk PRD Sistem Informasi Buku Tamu Digital.

Asumsi harus berkaitan dengan:
- pengguna sistem,
- ketersediaan data kunjungan,
- variabel dan kelas Naïve Bayes,
- penggunaan website,
- hasil klasifikasi Naïve Bayes.

Gunakan format ID asumsi seperti ASUMSI-01 dan seterusnya.
```

### Draf Awal Hasil Generate

AI menghasilkan beberapa asumsi terkait pengguna, data kunjungan, penggunaan website, dan analisis Naïve Bayes.

### Koreksi Manual Tim

Asumsi disesuaikan menjadi:

* **ASUMSI-01:** Pengguna terdiri dari tamu dan admin/petugas.
* **ASUMSI-02:** Data kunjungan tersedia dalam jumlah yang dapat digunakan untuk analisis.
* **ASUMSI-03:** Variabel dan kelas Naïve Bayes ditentukan berdasarkan data kunjungan.
* **ASUMSI-04:** Sistem utama digunakan melalui platform website.
* **ASUMSI-05:** Hasil klasifikasi/prediksi Naïve Bayes dapat ditampilkan pada dashboard.

Tim juga memastikan bahwa asumsi tidak ditulis sebagai fakta.

---

# 4. Prompt 03 — Penyusunan SRS dari PRD

### Prompt yang Dikirim ke AI

```text
Berdasarkan PRD Sistem Informasi Buku Tamu Digital,
buatkan Software Requirements Specification (SRS).

SRS harus mencakup:
1. Functional Requirements
2. Non-Functional Requirements
3. Acceptance/verification untuk setiap requirement
4. Kebutuhan analisis Naïve Bayes

Functional Requirement harus memiliki ID seperti FR-01,
FR-02, dan seterusnya.

Non-Functional Requirement harus mencakup:
- Performance
- Security
- Privacy
- Usability
- AI Accuracy
```

### Draf Awal Hasil Generate

AI menghasilkan daftar kebutuhan fungsional dan non-fungsional berdasarkan fitur pada PRD.

Contoh kebutuhan fungsional yang dihasilkan:

* FR-01 — Pencatatan Data Kunjungan
* FR-02 — Melihat Data Kunjungan
* FR-03 — Pengelolaan Data Kunjungan
* FR-04 — Dashboard Analitik
* FR-05 — Analisis Naïve Bayes
* FR-06 — Menampilkan Hasil Klasifikasi

### Koreksi Manual Tim

* Memastikan setiap requirement memiliki ID unik.
* Memastikan requirement dapat diverifikasi dengan metode black-box.
* Memastikan FR tidak terlalu teknis.
* Memisahkan fitur CRUD dari fitur AI.
* Memastikan Naïve Bayes memiliki fungsi analisis/klasifikasi yang jelas.
* Menyesuaikan NFR dengan kebutuhan proyek.
* Tidak menambahkan angka performa atau akurasi yang belum ditentukan dalam SRS.

---

# 5. Prompt 04 — Penyusunan User Stories

### Prompt yang Dikirim ke AI

```text
Transformasikan Functional Requirements pada SRS menjadi
user stories.

Gunakan format:
"Sebagai [persona], saya ingin [tujuan], sehingga [manfaat]."

Gunakan persona Tamu dan Admin/Petugas.

Pisahkan user story untuk fitur CRUD dan fitur AI.
Berikan ID US-01, US-02, dan seterusnya serta hubungkan
setiap user story dengan FR terkait.
```

### Draf Awal Hasil Generate

AI menghasilkan beberapa user story berdasarkan FR.

### Koreksi Manual Tim

User story disesuaikan menjadi:

| ID    | User Story                                                                                                                               | FR    | Prioritas |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----- | --------- |
| US-01 | Sebagai Tamu, saya ingin mencatat data kunjungan agar data kunjungan tersimpan secara digital.                                           | FR-01 | Must      |
| US-02 | Sebagai Admin/Petugas, saya ingin melihat data kunjungan agar dapat mengetahui data tamu yang tercatat.                                  | FR-02 | Must      |
| US-03 | Sebagai Admin/Petugas, saya ingin mengelola data kunjungan agar data tetap terorganisir dan dapat diperbarui.                            | FR-03 | Must      |
| US-04 | Sebagai Admin/Petugas, saya ingin melihat dashboard analitik agar dapat memahami ringkasan data kunjungan.                               | FR-04 | Must      |
| US-05 | Sebagai Admin/Petugas, saya ingin mendapatkan hasil klasifikasi menggunakan Naïve Bayes agar dapat membantu menganalisis pola kunjungan. | FR-05 | Must      |
| US-06 | Sebagai Admin/Petugas, saya ingin melihat hasil klasifikasi Naïve Bayes pada dashboard agar hasil analisis mudah dipahami.               | FR-06 | Should    |

---

# 6. Prompt 05 — Penyusunan Use Case

### Prompt yang Dikirim ke AI

```text
Buatkan use case berdasarkan user stories dan functional
requirements Sistem Informasi Buku Tamu Digital.

Gunakan aktor:
- Tamu
- Admin/Petugas
- Database
- Layanan Inferensi Naïve Bayes

Fokuskan use case pada fitur utama dan sertakan
exception/failure handling untuk proses AI.
```

### Draf Awal Hasil Generate

AI menghasilkan use case untuk pencatatan, pengelolaan, dashboard, dan analisis Naïve Bayes.

### Koreksi Manual Tim

Use case diperjelas agar tidak terlalu teknis dan tetap berfokus pada kebutuhan sistem.

Alur AI juga diberi kondisi kegagalan, yaitu:

* Data tidak memenuhi kondisi yang diperlukan untuk analisis.
* Proses analisis mengalami kegagalan atau timeout.
* Hasil klasifikasi memiliki tingkat keyakinan yang rendah.
* Sistem memberikan fallback atau informasi bahwa hasil analisis belum dapat digunakan.

---

# 7. Prompt 06 — Penyusunan User Flow

### Prompt yang Dikirim ke AI

```text
Buatkan user flow untuk fitur utama Sistem Informasi Buku Tamu
Digital dan fitur analisis Naïve Bayes.

User flow harus menunjukkan:
1. Kondisi awal
2. Input pengguna
3. Validasi
4. Proses sistem
5. Proses AI
6. Hasil
7. Kondisi gagal atau fallback

Gunakan persona Tamu dan Admin/Petugas.
```

### Draf Awal Hasil Generate

AI menghasilkan alur dari input data sampai data ditampilkan pada sistem serta alur proses analisis Naïve Bayes.

### Koreksi Manual Tim

User flow disederhanakan agar mudah dipahami dan tidak masuk terlalu jauh ke detail implementasi.

Untuk proses AI ditambahkan empat kondisi:

1. **Validasi awal** — memastikan data dapat diproses.
2. **Proses AI** — sistem menjalankan analisis Naïve Bayes.
3. **Hasil analisis** — sistem menampilkan hasil klasifikasi.
4. **Fallback** — sistem memberikan informasi jika proses gagal atau hasil tidak cukup meyakinkan.

---

# 8. Prompt 07 — Penyusunan Acceptance Criteria

### Prompt yang Dikirim ke AI

```text
Buatkan acceptance criteria untuk setiap user story
menggunakan format Given-When-Then.

Setiap user story memiliki 2-4 skenario.

Untuk fitur Naïve Bayes, sertakan:
- happy path,
- input edge case,
- low confidence,
- timeout atau kegagalan proses AI.

Acceptance criteria harus dapat diuji dan tidak boleh
mengarang nilai numerik yang belum ditentukan pada SRS.
```

### Draf Awal Hasil Generate

AI menghasilkan beberapa skenario Given-When-Then untuk setiap user story.

### Koreksi Manual Tim

* Setiap acceptance criteria dibuat lebih spesifik dan dapat diuji.
* Kondisi normal dan kondisi gagal dipisahkan.
* Untuk AI ditambahkan skenario **low confidence** dan **timeout/failure**.
* Tidak menggunakan angka akurasi, latency, atau confidence tertentu jika belum ditetapkan dalam SRS.
* Nilai yang belum ditentukan diarahkan untuk mengikuti ketentuan pada SRS.

---

# 9. Prompt 08 — Penyusunan Tabel Keterlacakan

### Prompt yang Dikirim ke AI

```text
Buatkan tabel traceability yang menghubungkan:
User Story → Functional Requirement → Use Case →
User Flow → Acceptance Criteria.

Pastikan setiap kebutuhan memiliki hubungan yang jelas
dan tidak ada requirement yang tidak memiliki user story
atau acceptance criteria.
```

### Draf Awal Hasil Generate

AI menghasilkan tabel keterlacakan antara user story, FR, use case, user flow, dan acceptance criteria.

### Koreksi Manual Tim

Tim melakukan pemeriksaan terhadap:

* ID user story.
* ID functional requirement.
* Hubungan user story dengan use case.
* Hubungan use case dengan user flow.
* Hubungan user story dengan acceptance criteria.
* Konsistensi fitur Naïve Bayes di seluruh dokumen.

---

# 10. Pemeriksaan Manual Akhir

Setelah hasil generate AI diperoleh, tim melakukan pemeriksaan manual untuk memastikan:

* [x] Nama dan ruang lingkup proyek sesuai.
* [x] Persona menggunakan **Tamu** dan **Admin/Petugas**.
* [x] Setiap Functional Requirement memiliki ID.
* [x] User Story memiliki hubungan dengan FR.
* [x] Use Case sesuai dengan kebutuhan sistem.
* [x] User Flow tidak bertentangan dengan Use Case.
* [x] Acceptance Criteria menggunakan format Given-When-Then.
* [x] Fitur Naïve Bayes dipisahkan dari fitur CRUD.
* [x] Kondisi gagal/timeout AI diperhatikan.
* [x] Asumsi diberi label sebagai asumsi.
* [x] Tidak terdapat klaim yang tidak didukung kebutuhan proyek.
* [x] Tidak ada nilai numerik yang dibuat tanpa dasar dari SRS.
* [x] Tabel keterlacakan diperiksa kembali.

---

# 11. Ringkasan Proses

| Tahap               | Input                        | Output             | Koreksi Manual                       |
| ------------------- | ---------------------------- | ------------------ | ------------------------------------ |
| PRD                 | Ide dan tujuan proyek        | PRD awal           | Penyesuaian ruang lingkup dan bahasa |
| Asumsi              | Kebutuhan dan batasan proyek | Daftar asumsi      | Pemisahan fakta dan asumsi           |
| SRS                 | PRD                          | FR dan NFR         | Validasi ID dan keterukuran          |
| User Stories        | FR                           | US-01 s.d. US-06   | Penyesuaian persona dan manfaat      |
| Use Case            | User Stories                 | Use Case sistem    | Penambahan exception handling        |
| User Flow           | Use Case                     | Alur pengguna      | Penyederhanaan alur                  |
| Acceptance Criteria | User Stories                 | Given-When-Then    | Penyesuaian agar dapat diuji         |
| Traceability        | Seluruh artefak              | Tabel keterlacakan | Pemeriksaan konsistensi              |

---

# 12. Kesimpulan

AI digunakan sebagai alat bantu dalam menyusun draf awal dokumen kebutuhan sistem. Hasil yang diberikan AI tidak langsung digunakan sebagai hasil akhir, tetapi diperiksa dan disesuaikan secara manual oleh tim.

Koreksi manual dilakukan untuk memastikan isi dokumen sesuai dengan ruang lingkup **Sistem Informasi Buku Tamu Digital**, menggunakan persona yang tepat, memiliki requirement yang dapat diverifikasi, serta menerapkan Naïve Bayes sesuai kebutuhan analisis sistem.
