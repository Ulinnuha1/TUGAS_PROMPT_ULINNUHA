# PRODUCT REQUIREMENT DOCUMENT (PRD)

## Sistem Informasi Buku Populer Berbasis Web

---

## 1. Executive Summary

Sistem Informasi Buku Populer Berbasis Web merupakan produk yang digunakan untuk membantu pengguna memperoleh informasi mengenai tingkat kepopuleran buku secara lebih terstruktur.

Berdasarkan penelitian, informasi mengenai tren kepopuleran buku belum tersusun secara sistematis sehingga diperlukan pengolahan data untuk membantu menentukan apakah suatu buku termasuk populer atau tidak. Penelitian menggunakan algoritma **Naïve Bayes** dengan dataset sebanyak 1.000 data buku. Hasil pengujian menghasilkan akurasi sebesar **72,63%**, precision **71,84%**, recall **62,11%**, dan F1-score **62,34%**.

Produk ini berfokus pada penyediaan informasi kepopuleran buku melalui data yang telah tersedia dan hasil pengolahan menggunakan Naïve Bayes.

---

## 2. Problem Statement & Evidence

### Problem Statement

Informasi mengenai kepopuleran buku belum tersusun secara sistematis sehingga pengguna mengalami kesulitan ketika ingin memperoleh gambaran mengenai kepopuleran suatu buku dari data yang tersedia.

### Evidence

| Jenis      | Temuan                                                                                                                                                          |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Fakta**  | Penelitian menyebutkan bahwa informasi mengenai tren kepopuleran buku belum terstruktur secara sistematis.                                                      |
| **Fakta**  | Dataset yang digunakan berjumlah 1.000 data buku.                                                                                                               |
| **Fakta**  | Data yang digunakan mencakup informasi seperti judul, harga, ulasan, deskripsi, penulis, kategori, dan popularitas.                                             |
| **Fakta**  | Data melalui proses preprocessing seperti penghapusan data duplikat, penanganan data kosong, lowercase, penghapusan tanda baca, stopword removal, dan stemming. |
| **Fakta**  | Hasil pengujian menghasilkan akurasi 72,63%, precision 71,84%, recall 62,11%, dan F1-score 62,34%.                                                              |
| **Asumsi** | [ASUMSI-01] Pengguna utama produk adalah pembaca yang membutuhkan informasi kepopuleran buku secara lebih praktis.                                              |
| **Asumsi** | [ASUMSI-02] Produk dikembangkan sebagai prototype dalam waktu satu semester dengan keterbatasan data dan biaya.                                                 |

---

## 3. Target User & Stakeholder

| Role              | Need                                            | Influence |
| ----------------- | ----------------------------------------------- | --------- |
| Pembaca           | Mendapatkan informasi mengenai kepopuleran buku | Tinggi    |
| Penerbit          | Memahami informasi mengenai buku yang populer   | Sedang    |
| Pengelola Dataset | Mengelola dan memperbarui data buku             | Tinggi    |
| Pengelola Sistem  | Mengelola penggunaan sistem dan data            | Tinggi    |

**Catatan:** Pembaca, penerbit, pengelola dataset, dan pengelola sistem merupakan bagian yang masih perlu dikonfirmasi karena sumber penelitian tidak menjelaskan persona pengguna secara rinci. Karena itu, bagian tersebut diberi status asumsi.

---

## 4. Value Proposition

### Pain yang Dikurangi

* Kesulitan memahami informasi kepopuleran buku dari data yang tersedia.
* Data buku yang cukup banyak membutuhkan proses pengolahan.
* Informasi kepopuleran buku belum tersusun secara sistematis.

### Gain yang Dihasilkan

* Pengguna dapat memperoleh informasi mengenai kepopuleran buku dengan lebih praktis.
* Data buku dapat dikelola dalam satu sistem.
* Hasil pengolahan data dapat digunakan sebagai informasi bagi pembaca dan penerbit.

### Mengapa AI Bukan Sekadar Gimmick?

Naïve Bayes digunakan sebagai bagian inti untuk menentukan apakah sebuah buku termasuk populer atau tidak berdasarkan data yang tersedia. Sistem penelitian menyediakan proses pelatihan, pengujian, evaluasi, dan pengujian data buku baru.

Dengan demikian, penggunaan AI memiliki fungsi langsung terhadap kebutuhan utama produk, bukan hanya sebagai fitur tambahan.

---

## 5. Product Goals & KPI

| Product Goal                               | KPI                      | Target/Referensi                            | Measurement              |
| ------------------------------------------ | ------------------------ | ------------------------------------------- | ------------------------ |
| Menghasilkan informasi kepopuleran buku    | Accuracy                 | 72,63% sebagai hasil pengujian penelitian   | Evaluasi hasil pengujian |
| Mengukur ketepatan hasil yang diberikan    | Precision                | 71,84% sebagai hasil pengujian penelitian   | Confusion matrix         |
| Mengukur kemampuan menemukan data populer  | Recall                   | 62,11% sebagai hasil pengujian penelitian   | Confusion matrix         |
| Mengukur keseimbangan precision dan recall | F1-score                 | 62,34% sebagai hasil pengujian penelitian   | Confusion matrix         |
| Menyediakan pengujian data baru            | Data baru dapat diproses | [ASUMSI-03] 100% data uji berhasil diproses | Pengujian fungsional     |

Hasil pengujian penelitian menggunakan data testing dan menghasilkan accuracy 72,63%, precision 71,84%, recall 62,11%, serta F1-score 62,34%.

---

## 6. Scope 3 Bulan – MoSCoW

| Prioritas  | Fitur                                | AI    |
| ---------- | ------------------------------------ | ----- |
| **Must**   | Dashboard informasi buku             | Tidak |
| **Must**   | Upload dataset                       | Tidak |
| **Must**   | Manajemen dataset                    | Tidak |
| **Must**   | Pelatihan model Naïve Bayes          | ★ Ya  |
| **Must**   | Pengujian model                      | ★ Ya  |
| **Must**   | Pengujian data buku baru             | ★ Ya  |
| **Should** | Riwayat hasil pengujian              | Tidak |
| **Should** | Ringkasan informasi kepopuleran buku | Tidak |
| **Could**  | Penggunaan metode AI tambahan        | ★ Ya  |
| **Won't**  | Pengembangan model deep learning     | ★ Ya  |

Fitur dashboard, upload dataset, hasil training, hasil testing, pengujian data baru, dan manajemen dataset mengacu pada fitur yang dijelaskan dalam penelitian.

---

## 7. Explicit Non-Goals

Produk ini **tidak mencakup**:

1. Sistem rekomendasi buku secara personal.
2. Pengembangan model deep learning.
3. Pengambilan data otomatis dari berbagai sumber eksternal.
4. Jaminan bahwa seluruh hasil prediksi selalu benar.
5. Penggantian keputusan pengguna dalam memilih buku.
6. Pengembangan aplikasi native Android atau iOS.
7. Fitur di luar kebutuhan pengolahan dan penyajian informasi kepopuleran buku.

Batasan ini diperlukan agar pengembangan prototype tetap sesuai dengan ruang lingkup waktu satu semester dan keterbatasan sumber daya **[ASUMSI-04]**.

---

## 8. Main Assumptions & Risks

| Assumption/Risk                               | Dampak                                      | Mitigasi                                                     |
| --------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ |
| [ASUMSI-05] Jumlah data terbatas              | Hasil model dapat kurang representatif      | Menggunakan dataset yang tersedia secara optimal             |
| Ketidakseimbangan kelas data                  | Dapat memengaruhi precision dan recall      | Melakukan evaluasi menggunakan confusion matrix              |
| Kualitas teks ulasan berbeda-beda             | Dapat memengaruhi hasil pengolahan data     | Melakukan preprocessing data                                 |
| Hasil model belum optimal                     | Informasi yang diberikan dapat kurang tepat | Melakukan evaluasi accuracy, precision, recall, dan F1-score |
| Waktu pengembangan terbatas                   | Tidak semua fitur dapat dikembangkan        | Memprioritaskan fitur Must                                   |
| [ASUMSI-06] Sumber daya pengembangan terbatas | Ruang lingkup produk menjadi terbatas       | Memfokuskan prototype pada kebutuhan utama                   |

Penelitian menunjukkan bahwa hasil recall masih memiliki keterbatasan dan performa dapat dipengaruhi oleh ketidakseimbangan kelas data.

---

## Review Checklist

| Checklist                                                  | Status |
| ---------------------------------------------------------- | ------ |
| Problem statement jelas                                    | ✅      |
| Problem statement tidak menggunakan solusi sebagai masalah | ✅      |
| Evidence dibedakan antara fakta dan asumsi                 | ✅      |
| KPI dapat diukur                                           | ✅      |
| Peran AI memiliki fungsi terhadap kebutuhan utama          | ✅      |
| Scope 3 bulan menggunakan MoSCoW                           | ✅      |
| Fitur AI ditandai ★                                        | ✅      |
| Non-goals dijelaskan                                       | ✅      |
| Risiko dan mitigasi dijelaskan                             | ✅      |
| Klaim yang tidak didukung sumber diberi `[ASUMSI-XX]`      | ✅      |
| Arsitektur teknis tidak dibahas                            | ✅      |

---

## Referensi Utama

Saputra, R. A., & Fatimah, T. (2025). **Penerapan Algoritma Naïve Bayes untuk Klasifikasi Buku Populer Berbasis Web**. SENAFTI 2025.
