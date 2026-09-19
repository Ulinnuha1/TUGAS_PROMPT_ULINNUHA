# SOFTWARE REQUIREMENTS SPECIFICATION (SRS)

## Sistem Informasi Buku Populer Berbasis Web

**Status:** Draf
**Prioritas:** MoSCoW
**Platform:** Website
**Stack:** [ASUMSI-01] Belum ditentukan dalam PRD dan tidak dibahas pada SRS ini.

---

# 1. Tujuan, Scope, dan Definisi Istilah

## 1.1 Tujuan

SRS ini mendefinisikan kebutuhan fungsional dan nonfungsional untuk Sistem Informasi Buku Populer Berbasis Web. Sistem ditujukan untuk mengelola data buku dan menghasilkan informasi mengenai kepopuleran buku berdasarkan pengolahan data menggunakan algoritma Naïve Bayes.

Penelitian yang menjadi dasar menggunakan 1.000 data buku dan menghasilkan nilai pengujian accuracy 72,63%, precision 71,84%, recall 62,11%, dan F1-score 62,34%.

## 1.2 Scope

### Termasuk dalam scope

* Pengelolaan dataset buku.
* Upload dataset.
* Pelatihan model Naïve Bayes.
* Pengujian model.
* Evaluasi hasil model.
* Pengujian data buku baru.
* Penyajian informasi hasil pengolahan data.
* Dashboard informasi buku.

Fitur-fitur tersebut mengacu pada fitur sistem yang dijelaskan dalam penelitian.

### Di luar scope

* Sistem rekomendasi buku personal.
* Pengembangan deep learning.
* Integrasi otomatis dengan banyak sumber data eksternal.
* Aplikasi native Android/iOS.
* Fitur di luar kebutuhan pengolahan dan penyajian informasi kepopuleran buku.

---

## 1.3 Definisi Istilah

| Istilah     | Definisi                                                                                       |
| ----------- | ---------------------------------------------------------------------------------------------- |
| Dataset     | Kumpulan data buku yang digunakan untuk proses pengolahan dan pengujian.                       |
| Naïve Bayes | Algoritma yang digunakan untuk menentukan kategori kepopuleran berdasarkan data yang tersedia. |
| Training    | Proses pembentukan model berdasarkan data pelatihan.                                           |
| Testing     | Proses pengujian model menggunakan data pengujian.                                             |
| Accuracy    | Persentase hasil prediksi yang benar dari seluruh data pengujian.                              |
| Precision   | Tingkat ketepatan hasil positif yang diberikan model.                                          |
| Recall      | Kemampuan model menemukan data yang termasuk kategori positif.                                 |
| F1-score    | Nilai gabungan antara precision dan recall.                                                    |
| Data baru   | Data buku yang belum digunakan dalam proses pelatihan dan ingin diuji oleh pengguna.           |

---

# 2. User, Stakeholder, Lingkungan Operasi, Asumsi & Dependensi

## 2.1 User dan Stakeholder

| Role              | Kebutuhan                                   | Pengaruh |
| ----------------- | ------------------------------------------- | -------- |
| Pembaca           | Mendapatkan informasi kepopuleran buku      | Tinggi   |
| Penerbit          | Mendapatkan informasi mengenai buku populer | Sedang   |
| Pengelola Dataset | Mengelola data buku                         | Tinggi   |
| Pengelola Sistem  | Mengelola penggunaan sistem                 | Tinggi   |

**Catatan:** Persona tersebut merupakan **[ASUMSI-02]** karena penelitian tidak menjelaskan persona pengguna secara rinci.

## 2.2 Lingkungan Operasi

| Aspek          | Keterangan                                                      |
| -------------- | --------------------------------------------------------------- |
| Platform       | Website                                                         |
| Perangkat      | [ASUMSI-03] Perangkat yang memiliki browser web                 |
| Koneksi        | [ASUMSI-04] Koneksi jaringan diperlukan untuk mengakses website |
| Sistem operasi | Tidak ditentukan dalam PRD                                      |
| Browser        | Tidak ditentukan dalam PRD                                      |

Tidak ada spesifikasi sistem operasi, browser, atau perangkat tertentu dalam penelitian sehingga tidak ditetapkan sebagai persyaratan teknis.

## 2.3 Asumsi

* **[ASUMSI-05]** Prototype dikembangkan dalam waktu satu semester.
* **[ASUMSI-06]** Sumber daya data dan biaya pengembangan terbatas.
* **[ASUMSI-07]** Pengguna dapat menyediakan data buku yang diperlukan untuk pengolahan.
* **[ASUMSI-08]** Data yang digunakan memiliki struktur yang dapat diproses oleh sistem.

## 2.4 Dependensi

* Dataset buku sebagai sumber data.
* Data hasil preprocessing sebagai data yang digunakan dalam pengolahan model.
* Algoritma Naïve Bayes sebagai metode pengolahan.
* Data testing untuk melakukan evaluasi model.

Penelitian menggunakan proses preprocessing berupa penghapusan duplikasi/data kosong, lowercase, penghapusan tanda baca/simbol, stopword removal, dan stemming.

---

# 3. Functional Requirements (FR)

| ID    | Functional Requirement                                                                                                                                     | Prioritas | Metode Verifikasi  |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------------------ |
| FR-01 | Sistem harus dapat menampilkan informasi buku pada dashboard saat pengguna mengakses halaman informasi → sistem menampilkan informasi buku yang tersedia.  | Must      | Black-box testing  |
| FR-02 | Sistem harus dapat menerima dataset buku saat pengguna melakukan upload dataset → sistem menerima dataset untuk diproses.                                  | Must      | Black-box testing  |
| FR-03 | Sistem harus dapat mengelola dataset saat pengelola dataset melakukan pengelolaan data → sistem menyediakan data yang dapat dikelola.                      | Must      | Black-box testing  |
| FR-04 | Sistem harus dapat melakukan pelatihan Naïve Bayes saat dataset pelatihan tersedia → sistem menghasilkan model hasil pelatihan.                            | Must ★    | Functional testing |
| FR-05 | Sistem harus dapat melakukan pengujian model saat data pengujian tersedia → sistem menghasilkan hasil pengujian.                                           | Must ★    | Functional testing |
| FR-06 | Sistem harus dapat menghitung accuracy, precision, recall, dan F1-score saat hasil pengujian tersedia → sistem menampilkan nilai evaluasi model.           | Must ★    | Perhitungan ulang  |
| FR-07 | Sistem harus dapat menerima data buku baru saat pengguna melakukan pengujian data → sistem memproses data tersebut menggunakan model.                      | Must ★    | Black-box testing  |
| FR-08 | Sistem harus dapat menentukan kategori kepopuleran buku saat data buku baru berhasil diproses → sistem menghasilkan informasi populer atau tidak populer.  | Must ★    | Functional testing |
| FR-09 | Sistem harus dapat menampilkan hasil pengujian data baru saat proses pengujian selesai → pengguna memperoleh hasil kepopuleran buku.                       | Must ★    | Black-box testing  |
| FR-10 | Sistem harus dapat menampilkan hasil training saat proses pelatihan selesai → pengguna dapat melihat hasil proses training.                                | Must ★    | Black-box testing  |
| FR-11 | Sistem harus dapat menampilkan hasil testing saat proses pengujian selesai → pengguna dapat melihat hasil evaluasi pengujian.                              | Must ★    | Black-box testing  |
| FR-12 | Sistem harus dapat menghapus dataset saat pengelola dataset memilih data yang akan dihapus → dataset yang dipilih tidak lagi tersedia.                     | Must      | Black-box testing  |
| FR-13 | [ASUMSI-09] Sistem harus dapat menampilkan riwayat hasil pengujian saat data hasil pengujian tersedia → pengguna dapat melihat hasil pengujian sebelumnya. | Should    | Black-box testing  |
| FR-14 | [ASUMSI-10] Sistem harus dapat menampilkan ringkasan informasi kepopuleran saat data buku tersedia → pengguna memperoleh ringkasan informasi buku populer. | Should    | Black-box testing  |

Fitur FR-01 sampai FR-12 terutama diturunkan dari fitur penelitian berupa Dashboard, Upload Dataset, Hasil Training, Hasil Testing, Uji Data Baru, dan Manajemen Dataset.

---

# 4. Non-Functional Requirements (NFR)

## 4.1 Kebutuhan Kualitas

Karakteristik ISO/IEC 25010 yang relevan dengan produk ini dipilih berdasarkan kebutuhan sistem yang memiliki pengolahan data dan model AI.

| ID     | Kategori ISO/IEC 25010 | NFR                                                                                                                                                                                         | Metrik                                                      | Target                                            | Kondisi Ukur                                             |
| ------ | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------- |
| NFR-01 | Performance Efficiency | Sistem harus dapat menghasilkan hasil pengujian data baru dalam waktu yang terukur.                                                                                                         | Waktu respons AI                                            | **[ASUMSI-11] ≤ 5 detik/data**                    | Diukur dari saat data baru dikirim sampai hasil tersedia |
| NFR-02 | Functional Suitability | Model harus menghasilkan accuracy sesuai hasil evaluasi penelitian sebagai baseline.                                                                                                        | Accuracy                                                    | ≥ 72,63% sebagai baseline penelitian              | Dataset testing                                          |
| NFR-03 | Functional Suitability | Model harus menghasilkan precision sesuai hasil evaluasi penelitian sebagai baseline.                                                                                                       | Precision                                                   | ≥ 71,84% sebagai baseline penelitian              | Dataset testing                                          |
| NFR-04 | Functional Suitability | Model harus menghasilkan recall sesuai hasil evaluasi penelitian sebagai baseline.                                                                                                          | Recall                                                      | ≥ 62,11% sebagai baseline penelitian              | Dataset testing                                          |
| NFR-05 | Functional Suitability | Model harus menghasilkan F1-score sesuai hasil evaluasi penelitian sebagai baseline.                                                                                                        | F1-score                                                    | ≥ 62,34% sebagai baseline penelitian              | Dataset testing                                          |
| NFR-06 | Security               | [ASUMSI-12] Sistem harus membatasi akses terhadap fungsi pengelolaan dataset kepada pengguna yang memiliki hak akses.                                                                       | Persentase pengujian akses yang berhasil dibatasi           | 100% skenario akses tidak sah ditolak             | Pengujian akses                                          |
| NFR-07 | Privacy                | [ASUMSI-13] Sistem harus membatasi penggunaan data yang disimpan hanya untuk kebutuhan produk.                                                                                              | Kepatuhan terhadap tujuan penggunaan data                   | 100% data digunakan sesuai tujuan yang ditetapkan | Review penggunaan data                                   |
| NFR-08 | Usability              | [ASUMSI-14] Pengguna harus dapat menyelesaikan proses pengujian data baru tanpa bantuan operator.                                                                                           | Task completion rate                                        | ≥ 90% pengguna uji berhasil menyelesaikan tugas   | Usability testing                                        |
| NFR-09 | Reliability            | Sistem harus menampilkan hasil yang konsisten ketika data pengujian yang sama diproses kembali menggunakan model yang sama.                                                                 | Konsistensi hasil                                           | 100% hasil sama                                   | Pengujian berulang                                       |
| NFR-10 | Performance Efficiency | Sistem harus dapat memproses data baru ketika data memenuhi kebutuhan input model.                                                                                                          | Persentase proses berhasil                                  | ≥ 95% data uji berhasil diproses                  | Pengujian dataset uji                                    |
| NFR-11 | Reliability            | [ASUMSI-15] Sistem harus memberikan informasi bahwa hasil tidak tersedia ketika data baru tidak memenuhi kebutuhan input model → pengguna menerima status proses yang gagal/tidak tersedia. | Persentase kasus gagal yang menghasilkan status yang sesuai | 100% kasus uji                                    | Negative testing                                         |

### Catatan penting NFR

NFR-01, NFR-06, NFR-07, NFR-08, dan NFR-11 **belum memiliki bukti empiris dari penelitian**. Angka targetnya ditandai **[ASUMSI]** karena checklist tugas secara eksplisit mewajibkan adanya latensi AI, keamanan, privasi, usability, dan fallback.

Sementara itu, NFR-02 sampai NFR-05 menggunakan hasil penelitian sebagai **baseline**, bukan klaim bahwa prototype pasti mencapai angka tersebut. Penelitian melaporkan hasil pengujian accuracy 72,63%, precision 71,84%, recall 62,11%, dan F1-score 62,34%.

---

# 5. Kebutuhan Data Minimum Fitur AI

## 5.1 Input Model

Berdasarkan penelitian, data yang digunakan memiliki atribut yang berkaitan dengan buku dan ulasan. Dataset penelitian berjumlah 1.000 data dengan atribut seperti judul, harga, review/helpfulness, review/summary, review/text, description, author, categories, dan popularity.

### Input minimum

| Data               | Fungsi                                         |
| ------------------ | ---------------------------------------------- |
| Judul buku         | Identitas buku                                 |
| Review/text        | Informasi teks ulasan                          |
| Review/helpfulness | Informasi pendukung dari ulasan                |
| Description        | Informasi deskripsi buku                       |
| Author             | Informasi penulis                              |
| Categories         | Informasi kategori buku                        |
| Popularity         | Label yang digunakan dalam proses pembelajaran |

**Catatan:** Tidak semua atribut di atas dapat dipastikan sebagai **input minimum untuk data baru**, karena penelitian tidak menjelaskan secara eksplisit subset minimum ketika melakukan fitur *Uji Data Baru*. Karena itu, kebutuhan field minimum untuk input data baru perlu dikonfirmasi **[ASUMSI-16]**.

## 5.2 Proses Data

Secara konseptual:

```text
Data Buku
   ↓
Preprocessing
   ↓
Data Siap Diproses
   ↓
Naïve Bayes
   ↓
Hasil Kepopuleran Buku
```

Preprocessing dalam penelitian mencakup penghapusan data duplikat/data kosong, lowercase, penghapusan tanda baca dan simbol, stopword removal, serta stemming.

## 5.3 Output Model

Output utama model:

```text
Input Data Buku
        ↓
    Naïve Bayes
        ↓
Kategori Kepopuleran
        ↓
Populer / Tidak Populer
```

Penelitian menjelaskan bahwa sistem dapat digunakan untuk menguji data buku baru dan menentukan apakah buku tersebut populer atau tidak.

---

# 6. Aturan Bisnis Hasil Riset

| ID    | Aturan Bisnis                                                                                                                                              |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BR-01 | Dataset harus tersedia sebelum proses training dilakukan.                                                                                                  |
| BR-02 | Model Naïve Bayes digunakan untuk menghasilkan informasi kepopuleran buku.                                                                                 |
| BR-03 | Data training dan data testing digunakan untuk proses pembentukan dan evaluasi model.                                                                      |
| BR-04 | Hasil model dievaluasi menggunakan accuracy, precision, recall, dan F1-score.                                                                              |
| BR-05 | Data buku baru dapat digunakan untuk memperoleh hasil kepopuleran berdasarkan model yang telah dilatih.                                                    |
| BR-06 | Preprocessing diperlukan sebelum data teks digunakan dalam pengolahan model.                                                                               |
| BR-07 | Hasil pengujian penelitian menjadi baseline evaluasi dengan accuracy 72,63%, precision 71,84%, recall 62,11%, dan F1-score 62,34%.                         |
| BR-08 | Hasil model tidak dianggap selalu benar karena penelitian menunjukkan masih terdapat keterbatasan pada recall dan adanya pengaruh ketidakseimbangan kelas. |

Penelitian menyebutkan bahwa performa model dapat dipengaruhi oleh ketidakseimbangan kelas dan recall masih memiliki keterbatasan.

---

# 7. Matriks Traceability

| Requirement | Fitur/Bagian PRD Terkait       | Bukti                                               |
| ----------- | ------------------------------ | --------------------------------------------------- |
| FR-01       | Dashboard                      | Fitur Dashboard pada penelitian                     |
| FR-02       | Upload Dataset                 | Fitur Upload Dataset                                |
| FR-03       | Manajemen Dataset              | Fitur Manajemen Dataset                             |
| FR-04       | ★ Training Naïve Bayes         | Metode Naïve Bayes dan proses training              |
| FR-05       | ★ Testing Model                | Proses testing model                                |
| FR-06       | ★ Evaluasi Model               | Accuracy, precision, recall, F1-score               |
| FR-07       | ★ Uji Data Baru                | Fitur Uji Data Baru                                 |
| FR-08       | ★ Penentuan Kepopuleran        | Sistem menentukan buku populer/tidak populer        |
| FR-09       | ★ Hasil Uji Data Baru          | Fitur Uji Data Baru                                 |
| FR-10       | ★ Hasil Training               | Fitur Hasil Training                                |
| FR-11       | ★ Hasil Testing                | Fitur Hasil Testing                                 |
| FR-12       | Manajemen Dataset              | Fitur penghapusan dataset                           |
| FR-13       | [ASUMSI] Riwayat Pengujian     | Fitur Should pada PRD                               |
| FR-14       | [ASUMSI] Ringkasan Kepopuleran | Fitur Should pada PRD                               |
| NFR-01      | Kinerja AI                     | [ASUMSI] Belum terdapat target latensi pada riset   |
| NFR-02      | KPI Accuracy                   | Hasil penelitian 72,63%                             |
| NFR-03      | KPI Precision                  | Hasil penelitian 71,84%                             |
| NFR-04      | KPI Recall                     | Hasil penelitian 62,11%                             |
| NFR-05      | KPI F1-score                   | Hasil penelitian 62,34%                             |
| NFR-06      | Keamanan                       | [ASUMSI] Tidak dibahas secara eksplisit dalam riset |
| NFR-07      | Privasi                        | [ASUMSI] Tidak dibahas secara eksplisit dalam riset |
| NFR-08      | Usability                      | [ASUMSI] Tidak dibahas secara eksplisit dalam riset |
| NFR-09      | Konsistensi hasil              | [ASUMSI] Belum diuji dalam riset                    |
| NFR-10      | Keberhasilan pemrosesan        | [ASUMSI] Belum ada target pada riset                |
| NFR-11      | Fallback                       | [ASUMSI] Belum dibahas dalam riset                  |

---

# Review Checklist SRS

| Checklist                                                   | Status | Keterangan                                                          |
| ----------------------------------------------------------- | ------ | ------------------------------------------------------------------- |
| Semua FR/NFR testable                                       | ✅      | Setiap requirement memiliki metode verifikasi                       |
| Tidak menggunakan istilah kosong seperti "cepat/mudah/aman" | ✅      | Diganti dengan metrik/target terukur                                |
| Akurasi AI tersedia                                         | ✅      | Accuracy 72,63% sebagai baseline                                    |
| Latensi AI tersedia                                         | ⚠️     | Target masih [ASUMSI-11]                                            |
| Privasi tersedia                                            | ⚠️     | Wajib checklist, tetapi belum didukung riset                        |
| Keamanan tersedia                                           | ⚠️     | Wajib checklist, tetapi belum didukung riset                        |
| Usability tersedia                                          | ⚠️     | Wajib checklist, tetapi belum didukung riset                        |
| Fallback tersedia                                           | ⚠️     | Masih [ASUMSI-15]                                                   |
| Traceability FR/NFR                                         | ✅/⚠️   | FR utama tertelusur; beberapa NFR wajib checklist masih asumsi      |
| MoSCoW digunakan                                            | ✅      | Must/Should/Could/Won't                                             |
| Verifikasi realistis untuk 1 semester                       | ✅      | Black-box, functional testing, perhitungan ulang, usability testing |
| Arsitektur/UI detail tidak dibahas                          | ✅      | Tidak masuk HLD/LLD                                                 |
| Asumsi diberi tanda                                         | ✅      | Menggunakan [ASUMSI-XX]                                             |

## Catatan Requirements Analyst

SRS ini **belum seharusnya dianggap final** pada bagian keamanan, privasi, usability, latensi, dan fallback. Bukan karena requirement tersebut tidak penting, tetapi karena **PRD dan penelitian yang menjadi sumber tidak menyediakan bukti atau target untuk kelima aspek tersebut**.

Untuk menjaga aturan *“dilarang menambah kebutuhan tanpa bukti”*, kebutuhan tersebut sengaja ditandai `[ASUMSI]`. Setelah dosen/user research memberikan target atau aturan yang jelas, bagian tersebut dapat diperbarui menjadi requirement final.
