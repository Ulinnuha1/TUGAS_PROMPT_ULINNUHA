# DRAF LLD — Sistem Informasi Buku Populer Berbasis Web

## 1. Informasi Dokumen

| Item | Keterangan |
|---|---|
| Nama Sistem | Sistem Informasi Buku Populer Berbasis Web |
| Dokumen | Low Level Design (LLD) |
| Platform | Website |
| Backend | Python Flask |
| Database | MySQL |
| AI | Naïve Bayes |
| Arsitektur | Client - Backend API - AI Service - Data Store |
| Pola Arsitektur | Layered Architecture |
| Status | Draf |

---

## 2. Tujuan LLD

LLD digunakan sebagai rancangan teknis yang menjadi acuan sebelum proses implementasi dan coding.

LLD ini menjelaskan:
- desain modul dan class;
- struktur data;
- relasi antarentitas;
- spesifikasi API;
- alur detail fitur AI;
- error handling dan fallback;
- traceability terhadap FR dan NFR.

Seluruh rancangan diturunkan dari SRS dan HLD hasil revisi. Bagian yang belum ditentukan secara eksplisit diberi tanda `[KEPUTUSAN TIM: ...]`.

---

# 3. Ruang Lingkup Implementasi

Fitur yang menjadi prioritas Must:

1. Dashboard;
2. Upload Dataset;
3. Manajemen Dataset;
4. Training Naïve Bayes;
5. Testing Model;
6. Evaluasi Model;
7. Input Data Buku Baru;
8. Penentuan hasil Populer atau Tidak Populer.

Fitur berstatus Should dan Could tidak menjadi fokus utama implementasi Must.

---

# 4. Arsitektur Implementasi

Arsitektur sistem menggunakan pola layered architecture.

Alur utama:

Web Client
→ Backend API
→ Service Layer
→ AI Service
→ Data Store

Komponen utama:

| Komponen | Teknologi | Tanggung Jawab |
|---|---|---|
| Web Client | HTML, CSS, JavaScript | Menampilkan antarmuka dan mengirim request |
| Backend API | Python Flask | Menangani request, validasi, dan koordinasi service |
| Dataset Service | Python | Mengelola dataset |
| AI Service | Python | Preprocessing, training, testing, dan prediction |
| Data Store | MySQL | Menyimpan dataset dan hasil proses |
| Naïve Bayes Model | Library AI lokal | Melakukan training dan prediction |
| Fallback Handler | Python Flask | Menangani kegagalan model dan service |

---

# 5. Struktur Modul

Struktur modul awal:

| Modul | Tanggung Jawab |
|---|---|
| DashboardModule | Mengambil dan menampilkan ringkasan data |
| DatasetModule | Upload, validasi, penyimpanan, dan penghapusan dataset |
| TrainingModule | Menyiapkan data dan menjalankan training |
| TestingModule | Menjalankan pengujian model |
| EvaluationModule | Menghitung dan menampilkan metrik evaluasi |
| PredictionModule | Memproses data buku baru |
| PreprocessingModule | Membersihkan dan menyiapkan data teks |
| NaiveBayesModule | Mengelola model Naïve Bayes |
| ErrorHandler | Menangani error dan fallback |

---

# 6. Desain Class DatasetService

## Tanggung Jawab

`DatasetService` bertanggung jawab untuk:
- menerima dataset;
- memvalidasi format dataset;
- memeriksa atribut yang dibutuhkan;
- menyimpan dataset;
- mengambil dataset;
- menghapus dataset.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| datasetRepository | DatasetRepository | Akses data dataset |
| validator | DatasetValidator | Validasi dataset |

## Method Utama

| Method | Parameter | Return | Keterangan |
|---|---|---|---|
| uploadDataset | file | DatasetResult | Memproses file dataset |
| validateDataset | data | ValidationResult | Memeriksa validitas dataset |
| saveDataset | data | Dataset | Menyimpan dataset |
| getDataset | datasetId | Dataset | Mengambil dataset |
| deleteDataset | datasetId | Boolean | Menghapus dataset |

---

# 7. Desain Class TrainingService

## Tanggung Jawab

`TrainingService` bertanggung jawab menjalankan proses training model Naïve Bayes berdasarkan dataset yang telah tersedia.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| datasetService | DatasetService | Mengambil dataset |
| preprocessingService | PreprocessingService | Melakukan preprocessing |
| naiveBayesModel | NaiveBayesModel | Model Naïve Bayes |
| evaluationService | EvaluationService | Mengolah hasil evaluasi |

## Method Utama

| Method | Parameter | Return | Keterangan |
|---|---|---|---|
| train | datasetId | TrainingResult | Menjalankan training |
| prepareTrainingData | dataset | TrainingData | Menyiapkan data training |
| saveTrainingResult | result | Boolean | Menyimpan hasil training |

## Alur

Dataset
→ Validasi
→ Preprocessing
→ Pembagian data
→ Training Naïve Bayes
→ Model siap digunakan

---

# 8. Desain Class PredictionService

## Tanggung Jawab

`PredictionService` bertanggung jawab memproses data buku baru dan menghasilkan hasil prediksi menggunakan model Naïve Bayes yang telah dilatih.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| preprocessingService | PreprocessingService | Memproses data input |
| naiveBayesModel | NaiveBayesModel | Model prediksi |
| predictionRepository | PredictionRepository | Penyimpanan hasil prediksi |

## Method Utama

| Method | Parameter | Return | Keterangan |
|---|---|---|---|
| validateInput | data | ValidationResult | Validasi data buku |
| preprocessInput | data | ProcessedData | Preprocessing |
| predict | data | PredictionResult | Menentukan hasil |
| savePrediction | result | Boolean | Menyimpan hasil |

---

# 9. Desain Class PreprocessingService

## Tanggung Jawab

Melakukan preprocessing terhadap data teks sebelum digunakan oleh model Naïve Bayes.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| stopwordList | List | Daftar stopword |
| stemmer | Stemmer | Komponen stemming |

## Method Utama

| Method | Parameter | Return | Keterangan |
|---|---|---|---|
| normalizeText | text | String | Mengubah teks menjadi lowercase |
| removeSymbols | text | String | Menghapus simbol |
| removeStopwords | text | String | Menghapus stopword |
| stemming | text | String | Melakukan stemming |
| preprocess | data | ProcessedData | Menjalankan seluruh preprocessing |

## Tahapan

Input text
→ Lowercase
→ Remove punctuation/symbol
→ Stopword removal
→ Stemming
→ Processed text

---

# 10. Desain Class TestingService

## Tanggung Jawab

Menjalankan proses testing model menggunakan data testing.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| naiveBayesModel | NaiveBayesModel | Model yang diuji |
| evaluationService | EvaluationService | Menghitung evaluasi |

## Method Utama

| Method | Parameter | Return | Keterangan |
|---|---|---|---|
| test | model, testData | TestResult | Menjalankan testing |
| generatePrediction | testData | PredictionList | Menghasilkan prediksi |
| evaluate | actual, predicted | EvaluationResult | Menghasilkan metrik |

---

# 11. Desain Class EvaluationService

## Tanggung Jawab

Menghitung metrik evaluasi model berdasarkan hasil prediksi dan label sebenarnya.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| evaluationRepository | EvaluationRepository | Penyimpanan hasil evaluasi |

## Method Utama

| Method | Parameter | Return |
|---|---|---|
| calculateAccuracy | actual, predicted | Float |
| calculatePrecision | actual, predicted | Float |
| calculateRecall | actual, predicted | Float |
| calculateF1 | actual, predicted | Float |
| generateEvaluation | actual, predicted | EvaluationResult |

Metrik yang digunakan:
- Accuracy;
- Precision;
- Recall;
- F1 Score.

---

# 12. Desain Class NaiveBayesModel

## Tanggung Jawab

Mengelola model Naïve Bayes untuk proses training dan prediction.

## Atribut Utama

| Atribut | Tipe | Keterangan |
|---|---|---|
| model | Model | Model Naïve Bayes |
| vectorizer | Vectorizer | Representasi data teks |
| modelStatus | String | Status model |
| modelVersion | String | Versi model |

## Method Utama

| Method | Parameter | Return |
|---|---|---|
| fit | XTrain, yTrain | Boolean |
| predict | XTest | PredictionList |
| saveModel | - | Boolean |
| loadModel | - | Boolean |
| isModelAvailable | - | Boolean |

## Status Model

| Status | Arti |
|---|---|
| NOT_TRAINED | Model belum dilatih |
| TRAINING | Training sedang berjalan |
| READY | Model siap digunakan |
| FAILED | Training/model gagal |

---

# 13. Desain Class DashboardService

## Tanggung Jawab

Mengambil informasi ringkasan yang diperlukan untuk Dashboard.

## Atribut Utama

| Atribut | Tipe |
|---|---|
| datasetRepository | DatasetRepository |
| evaluationRepository | EvaluationRepository |

## Method Utama

| Method | Return | Keterangan |
|---|---|---|
| getDashboardSummary | DashboardSummary | Ringkasan dashboard |
| getDatasetSummary | DatasetSummary | Ringkasan dataset |
| getEvaluationSummary | EvaluationSummary | Ringkasan evaluasi |

---

# 14. Pilihan Library Naïve Bayes

Library AI belum ditetapkan secara eksplisit pada requirement.

## Opsi 1 — scikit-learn

Kelebihan:
- mendukung algoritma Naïve Bayes;
- mudah diintegrasikan dengan Python Flask;
- implementasi relatif sederhana;
- dokumentasi luas;
- sesuai untuk prototype.

Kekurangan:
- membutuhkan dependency tambahan.

## Opsi 2 — Implementasi Manual

Kelebihan:
- tidak bergantung pada library machine learning;
- seluruh proses algoritma dapat dikontrol sendiri.

Kekurangan:
- implementasi lebih panjang;
- lebih banyak kode;
- risiko kesalahan implementasi lebih besar;
- waktu pengembangan lebih lama.

## Kriteria Pemilihan

| Kriteria | scikit-learn | Manual |
|---|---|---|
| Kemudahan implementasi | Tinggi | Rendah |
| Integrasi Flask | Mudah | Sedang |
| Waktu implementasi | Lebih singkat | Lebih lama |
| Maintenance | Lebih mudah | Lebih sulit |

[KEPUTUSAN TIM: ______________________________]

---

# 15. Pilihan Penyimpanan Model

## Opsi 1 — File Model Lokal

Model disimpan sebagai file pada server.

Kelebihan:
- sederhana;
- sesuai untuk prototype;
- tidak membutuhkan layanan tambahan.

Kekurangan:
- harus mengelola file model;
- versi model harus dikontrol.

## Opsi 2 — Database Metadata Model

Informasi model disimpan pada database dan file model dikaitkan dengan metadata tersebut.

Kelebihan:
- informasi model lebih terstruktur;
- dapat menyimpan informasi versi dan waktu training.

Kekurangan:
- implementasi lebih kompleks.

## Kriteria

Pilihan ditentukan berdasarkan:
- kemudahan implementasi;
- kebutuhan prototype;
- kemudahan maintenance;
- kebutuhan pencatatan versi.

[KEPUTUSAN TIM: ______________________________]

---

# 16. Skema Data

Entitas utama:

1. `datasets`
2. `books`
3. `model_evaluations`
4. `predictions`

Struktur tersebut digunakan untuk mendukung pengelolaan dataset, proses AI, hasil evaluasi, dan hasil prediksi.

---

# 17. Entitas Dataset

## Tabel `datasets`

| Field | Type | Constraint | Keterangan |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | ID dataset |
| file_name | VARCHAR(255) | NOT NULL | Nama file |
| total_records | INT | NOT NULL | Jumlah data |
| uploaded_at | DATETIME | NOT NULL | Waktu upload |
| status | VARCHAR(30) | NOT NULL | Status dataset |

Status dataset:

- `UPLOADED`
- `VALID`
- `INVALID`
- `PROCESSED`

---

# 18. Entitas Books

## Tabel `books`

| Field | Type | Constraint | Keterangan |
|---|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT | ID buku |
| dataset_id | BIGINT | FK, NOT NULL | ID dataset |
| title | VARCHAR(255) | NOT NULL | Judul buku |
| price | DECIMAL(12,2) | NULL | Harga buku |
| review_helpfulness | TEXT | NULL | Data kebermanfaatan review |
| review_summary | TEXT | NULL | Ringkasan review |
| review_text | TEXT | NULL | Isi review |
| description | TEXT | NULL | Deskripsi buku |
| author | VARCHAR(255) | NULL | Penulis |
| categories | TEXT | NULL | Kategori buku |
| popularity | VARCHAR(30) | NULL | Label popularitas |

Constraint:
- `dataset_id` harus mengacu pada dataset yang tersedia;
- `title` wajib tersedia;
- data training harus memiliki label `popularity`;
- data buku baru tidak wajib memiliki label sebelum prediksi.

---

# 19. Batasan Dataset

Dataset dibatasi pada data buku yang digunakan untuk proses sistem.

Atribut yang digunakan berdasarkan HLD:

- title;
- price;
- review/helpfulness;
- review/summary;
- review/text;
- description;
- author;
- categories;
- popularity.

Dataset penelitian yang menjadi dasar memiliki 1000 data buku. Jumlah tersebut menjadi referensi dataset, bukan requirement minimum sistem kecuali diputuskan oleh tim.

[KEPUTUSAN TIM: Jumlah minimum dataset yang wajib diterima sistem adalah __________________]

---

# 20. Batasan Label

Label yang digunakan:

| Label | Keterangan |
|---|---|
| Populer | Buku termasuk kategori populer |
| Tidak Populer | Buku termasuk kategori tidak populer |

Dataset training wajib memiliki label.

Data buku baru yang akan diprediksi tidak harus memiliki label karena label akan dihasilkan oleh model.

Aturan atau threshold yang menentukan sebuah buku diberi label Populer atau Tidak Populer belum dijelaskan secara eksplisit pada SRS/HLD.

[KEPUTUSAN TIM: Aturan pembentukan label adalah ______________________________]

---

# 21. Entitas Model Evaluation

## Tabel `model_evaluations`

| Field | Type | Constraint |
|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT |
| accuracy | DECIMAL(6,4) | NOT NULL |
| precision | DECIMAL(6,4) | NOT NULL |
| recall | DECIMAL(6,4) | NOT NULL |
| f1_score | DECIMAL(6,4) | NOT NULL |
| created_at | DATETIME | NOT NULL |

Data evaluasi digunakan untuk menampilkan hasil pengujian model.

---

# 22. Entitas Prediction

## Tabel `predictions`

| Field | Type | Constraint |
|---|---|---|
| id | BIGINT | PK, AUTO_INCREMENT |
| book_id | BIGINT | NULL |
| predicted_label | VARCHAR(30) | NOT NULL |
| created_at | DATETIME | NOT NULL |

`predicted_label` hanya dapat berisi:

- `Populer`
- `Tidak Populer`

Penyimpanan riwayat prediksi merupakan bagian yang perlu disesuaikan dengan keputusan implementasi terhadap FR yang tersedia.

[KEPUTUSAN TIM: Penyimpanan riwayat prediksi __________________]

---

# 23. Relasi Entitas

Relasi utama:

`datasets` 1 : N `books`

Artinya satu dataset dapat memiliki banyak data buku.

`books` 1 : N `predictions`

Artinya satu data buku dapat memiliki hasil prediksi yang tersimpan.

`model_evaluations` berdiri sebagai penyimpanan hasil evaluasi model.

ERD teks:

`datasets`
→ `books`
→ `predictions`

---

# 24. Constraint Database

Constraint utama:

1. Primary key pada setiap tabel;
2. Foreign key `books.dataset_id` menuju `datasets.id`;
3. Field wajib tidak boleh `NULL`;
4. Label hanya menggunakan `Populer` atau `Tidak Populer`;
5. Dataset harus valid sebelum digunakan untuk training;
6. Data training harus memiliki label;
7. Data buku baru tidak membutuhkan label;
8. Data duplikat perlu ditangani pada proses preprocessing/validasi.

---

# 25. API Utama

Endpoint utama yang digunakan:

| Method | Path | Fungsi |
|---|---|---|
| GET | `/api/dashboard` | Mengambil data dashboard |
| POST | `/api/dataset` | Upload dataset |
| GET | `/api/dataset` | Mengambil dataset |
| DELETE | `/api/dataset/{id}` | Menghapus dataset |
| POST | `/api/training` | Menjalankan training |
| POST | `/api/testing` | Menjalankan testing |
| GET | `/api/evaluation` | Mengambil hasil evaluasi |
| POST | `/api/predict` | Melakukan prediksi data baru |

---

# 26. API Dashboard

## Endpoint

`GET /api/dashboard`

## Request

Tidak membutuhkan request body.

## Response berhasil

```json
{
  "status": "success",
  "data": {
    "total_books": 1000,
    "dataset_status": "VALID",
    "model_status": "READY"
  }
}

