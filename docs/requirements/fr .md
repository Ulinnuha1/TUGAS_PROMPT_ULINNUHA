# USER STORIES

## 1. Informasi Dokumen

| Informasi     | Keterangan                             |
| ------------- | -------------------------------------- |
| Nama Proyek   | Sistem Informasi Buku Tamu Digital     |
| Dokumen Acuan | SRS PTM-02                             |
| Platform      | Website                                |
| Metode AI     | Naïve Bayes                            |
| Prioritas     | Must Have dan Should Have              |
| Penyusun      | Agile Product Owner & Business Analyst |

---

## 2. User Stories

User stories berikut diturunkan dari Functional Requirements (FR) pada SRS. Setiap story menggunakan persona yang telah ditentukan pada PRD dan berfokus pada manfaat nyata bagi pengguna.

| ID Story | Narasi                                                                                                                                                                                                             | FR Asal | Prioritas MoSCoW | Kategori   |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- | ---------------- | ---------- |
| US-01    | Sebagai **tamu**, saya ingin mengisi data kunjungan secara digital, agar proses pencatatan kunjungan dapat dilakukan tanpa pencatatan manual.                                                                      | FR-01   | Must Have        | Fitur Inti |
| US-02    | Sebagai **admin/petugas**, saya ingin melihat data kunjungan yang telah dicatat, agar saya dapat mengetahui dan memantau riwayat kunjungan tamu.                                                                   | FR-02   | Must Have        | Fitur Inti |
| US-03    | Sebagai **admin/petugas**, saya ingin mengelola data kunjungan, agar data yang tersimpan tetap dapat dikelola sesuai kebutuhan administrasi.                                                                       | FR-03   | Must Have        | Fitur Inti |
| US-04    | Sebagai **admin/petugas**, saya ingin melihat ringkasan data kunjungan melalui dashboard, agar pola dan informasi kunjungan dapat dipantau dengan lebih terstruktur.                                               | FR-04   | Must Have        | Fitur Inti |
| US-05 ★  | Sebagai **admin/petugas**, saya ingin mendapatkan hasil klasifikasi menggunakan Naïve Bayes berdasarkan data kunjungan, agar saya dapat memperoleh informasi pola atau kategori kunjungan dari data yang tersedia. | FR-05   | Must Have        | Fitur AI ★ |
| US-06 ★  | Sebagai **admin/petugas**, saya ingin melihat hasil klasifikasi Naïve Bayes pada dashboard, agar informasi hasil analisis dapat digunakan sebagai bahan memahami data kunjungan.                                   | FR-06   | Should Have      | Fitur AI ★ |

> **Catatan:** ID FR pada tabel di atas harus disesuaikan dengan ID FR yang sebenarnya terdapat pada `srs.md`. Narasi tidak boleh digunakan sebagai pengganti penelusuran FR.

---

## 3. Evaluasi Prinsip INVEST

| ID Story | Independent | Negotiable | Valuable | Estimable | Small | Testable | Evaluasi                                                                                      |
| -------- | ----------- | ---------- | -------- | --------- | ----- | -------- | --------------------------------------------------------------------------------------------- |
| US-01    | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Memenuhi INVEST dan dapat diuji melalui pengujian pencatatan data kunjungan.                  |
| US-02    | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Memiliki ruang lingkup terpisah dan dapat diverifikasi dari data kunjungan yang tersimpan.    |
| US-03    | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Dapat diuji berdasarkan keberhasilan pengelolaan data kunjungan.                              |
| US-04    | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Dapat diuji dengan memeriksa apakah ringkasan data kunjungan dapat ditampilkan.               |
| US-05 ★  | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Fitur AI terpisah dari fungsi CRUD dan dapat diuji berdasarkan input serta hasil klasifikasi. |
| US-06 ★  | ✓           | ✓          | ✓        | ✓         | ✓     | ✓        | Terpisah dari proses klasifikasi sehingga hasil AI dapat diverifikasi pada bagian analitik.   |

### Keterangan

* **Independent**: Story dapat dikembangkan tanpa ketergantungan yang tidak perlu pada story lain.
* **Negotiable**: Story menjelaskan kebutuhan pengguna tanpa menentukan detail teknis implementasi.
* **Valuable**: Story memberikan manfaat nyata bagi persona.
* **Estimable**: Lingkup story cukup jelas untuk diperkirakan.
* **Small**: Story cukup kecil untuk dikerjakan dalam satu iterasi.
* **Testable**: Story memiliki hasil yang dapat diverifikasi.

---

## 4. Pemecahan Epic

### Epic: Analisis Data Menggunakan Naïve Bayes ★

Fitur analisis Naïve Bayes dapat menjadi terlalu besar apabila mencakup seluruh proses sekaligus. Oleh karena itu, fitur tersebut dipecah menjadi beberapa story:

```text
Epic
└── Analisis Data Kunjungan dengan Naïve Bayes ★
    ├── US-05 ★
    │   └── Melakukan klasifikasi berdasarkan data kunjungan
    │
    └── US-06 ★
        └── Menampilkan hasil klasifikasi pada dashboard
```

Pemecahan tersebut membuat proses analisis AI dan penyajian hasilnya dapat diuji secara terpisah.

---

## 5. Traceability User Story

| User Story | FR Asal | Fitur PRD                        | Persona       | Nilai/Manfaat                                            |
| ---------- | ------- | -------------------------------- | ------------- | -------------------------------------------------------- |
| US-01      | FR-01   | Pencatatan buku tamu             | Tamu          | Mengurangi pencatatan kunjungan secara manual.           |
| US-02      | FR-02   | Pengelolaan data kunjungan       | Admin/Petugas | Memudahkan pemantauan riwayat kunjungan.                 |
| US-03      | FR-03   | Pengelolaan data kunjungan       | Admin/Petugas | Membantu pengelolaan data kunjungan secara digital.      |
| US-04      | FR-04   | Dashboard analitik               | Admin/Petugas | Membantu memahami informasi dan pola kunjungan.          |
| US-05 ★    | FR-05   | Analisis Naïve Bayes             | Admin/Petugas | Memberikan hasil klasifikasi berdasarkan data kunjungan. |
| US-06 ★    | FR-06   | Dashboard analitik + Naïve Bayes | Admin/Petugas | Membantu melihat hasil analisis secara terstruktur.      |

---

## 6. Checklist Review Tahap 1

* [x] Peran pengguna menggunakan persona yang telah ditentukan.
* [x] Manfaat menjelaskan nilai nyata bagi pengguna.
* [x] Detail UI dan coding tidak dimasukkan ke dalam user story.
* [x] Fitur AI ★ dipisahkan dari fitur CRUD.
* [x] Story AI dipecah berdasarkan fungsi yang berbeda.
* [ ] Seluruh ID FR telah dicocokkan dengan SRS PTM-02.
* [ ] Seluruh persona telah dicocokkan dengan PRD.
* [ ] Seluruh prioritas Must/Should telah dicocokkan dengan SRS.
* [ ] Setiap story telah diverifikasi terhadap NFR terkait.

---

## 7. Catatan Validasi

User stories harus divalidasi kembali terhadap `prd.md` dan `srs.md` sebelum digunakan sebagai dasar backlog pengembangan. Tidak ada kebutuhan baru yang boleh ditambahkan hanya berdasarkan user story apabila kebutuhan tersebut tidak memiliki sumber pada PRD, riset, atau SRS.
