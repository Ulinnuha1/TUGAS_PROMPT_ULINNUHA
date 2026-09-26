# LLD (Low Level Design)

## 1. Desain Modul/Class

### 1.1 Modul Pencatatan Data Kunjungan

**Class:** `GuestVisit`

**Tanggung jawab:**

1. Menyimpan data kunjungan tamu.
2. Memvalidasi data kunjungan.
3. Mengelola data kunjungan.

**Atribut utama:**

1. `id`
2. `guestName`
3. `institution`
4. `visitPurpose`
5. `visitDate`
6. `createdAt`
7. `updatedAt`

**Method utama:**

1. `createVisit()`
2. `validateVisit()`
3. `getVisitById()`
4. `getVisits()`
5. `updateVisit()`
6. `deleteVisit()`

### 1.2 Modul Analitik

**Class:** `AnalyticsService`

**Tanggung jawab:**

* Mengambil data kunjungan.
* Menyiapkan data untuk proses analisis.
* Memproses hasil analisis Naïve Bayes.

**Method utama:**

* `validateInput()`
* `prepareFeatures()`
* `classify()`
* `validatePrediction()`

### 1.3 Modul AI

**Class:** `NaiveBayesService`

**Tanggung jawab:**

* Melakukan preprocessing data.
* Menjalankan klasifikasi Naïve Bayes.
* Menghasilkan hasil klasifikasi dan confidence.
* Menangani timeout dan kegagalan model.

**Atribut utama:**

* `modelVersion`
* `timeout`
* `confidenceThreshold`

**Method utama:**

* `preprocess()`
* `predict()`
* `validateConfidence()`
* `handleTimeout()`
* `handleModelError()`

**Pilihan implementasi AI:**

* Opsi 1: Naïve Bayes sebagai layanan REST API terpisah.
* Opsi 2: Naïve Bayes dijalankan langsung pada backend.

**Kriteria:** dipilih berdasarkan kebutuhan deployment, pemisahan layanan, dan kemampuan stack yang digunakan.

**[KEPUTUSAN TIM: Pilih opsi implementasi layanan AI]**

---

## 2. Skema Data

### Entitas `guest_visits`

```sql
CREATE TABLE guest_visits (
    id UUID PRIMARY KEY,
    guest_name VARCHAR(150) NOT NULL,
    institution VARCHAR(150),
    visit_purpose VARCHAR(255) NOT NULL,
    visit_date TIMESTAMP NOT NULL,
    created_at TIMESTAMP NOT NULL,
    updated_at TIMESTAMP NOT NULL
);
```

### Entitas `predictions`

```sql
CREATE TABLE predictions (
    id UUID PRIMARY KEY,
    guest_visit_id UUID NOT NULL,
    predicted_class VARCHAR(100) NOT NULL,
    confidence DECIMAL(5,4) NOT NULL,
    model_version VARCHAR(50) NOT NULL,
    created_at TIMESTAMP NOT NULL,

    CONSTRAINT fk_prediction_visit
        FOREIGN KEY (guest_visit_id)
        REFERENCES guest_visits(id)
);
```

### Relasi

```text
guest_visits 1 -------- N predictions
```

### Constraint

* `guest_name`, `visit_purpose`, dan `visit_date` wajib diisi.
* `predicted_class` tidak boleh kosong.
* `confidence` harus berada pada rentang nilai yang valid.
* `model_version` wajib dicatat.
* `guest_visit_id` harus mengacu pada data kunjungan yang tersedia.

---

## 3. Spesifikasi API

### 3.1 Menambahkan Data Kunjungan

**Method:** `POST`
**Path:** `/api/guest-visits`

**Request:**

```json
{
  "guestName": "Budi Santoso",
  "institution": "Universitas ABC",
  "visitPurpose": "Kunjungan akademik",
  "visitDate": "2026-09-27T09:00:00+07:00"
}
```

**Response `201 Created`:**

```json
{
  "id": "uuid",
  "guestName": "Budi Santoso",
  "institution": "Universitas ABC",
  "visitPurpose": "Kunjungan akademik",
  "visitDate": "2026-09-27T09:00:00+07:00"
}
```

**Kode error:**

* `400 VALIDATION_ERROR`
* `500 DATABASE_ERROR`

### 3.2 Melihat Data Kunjungan

**Method:** `GET`
**Path:** `/api/guest-visits`

**Response `200 OK`:**

```json
{
  "data": [
    {
      "id": "uuid",
      "guestName": "Budi Santoso",
      "institution": "Universitas ABC",
      "visitPurpose": "Kunjungan akademik",
      "visitDate": "2026-09-27T09:00:00+07:00"
    }
  ]
}
```

**Kode error:**

* `404 DATA_NOT_FOUND`
* `500 DATABASE_ERROR`

### 3.3 Analisis Naïve Bayes

**Method:** `POST`
**Path:** `/api/analytics/predict`

**Request:**

```json
{
  "visitId": "uuid"
}
```

**Response `200 OK`:**

```json
{
  "visitId": "uuid",
  "predictedClass": "Kunjungan Akademik",
  "confidence": 0.87,
  "modelVersion": "NB-1.0"
}
```

**Kode error:**

* `400 INVALID_INPUT`
* `404 VISIT_NOT_FOUND`
* `408 AI_TIMEOUT`
* `422 LOW_CONFIDENCE`
* `503 AI_UNAVAILABLE`
* `500 AI_MODEL_ERROR`

---

## 4. Sequence dan Error Handling Fitur AI

### Alur Utama

```text
┌─────────────┐
│    Mulai    │
└──────┬──────┘
       ↓
┌─────────────────────────┐
│ Pilih Analisis          │
└──────────┬──────────────┘
           ↓
┌─────────────────────────┐
│ Ambil Data Kunjungan    │
└──────────┬──────────────┘
           ↓
┌─────────────────────────┐
│ Validasi Input          │
└──────────┬──────────────┘
           ↓
       ┌───────┐
       │ Valid?│
       └───┬───┘
       Tidak│Ya
          ↓  ↓
   ┌──────────┐  ┌─────────────────┐
   │ Pesan    │  │ Preprocessing   │
   │ Error    │  └────────┬────────┘
   └────┬─────┘           ↓
        │        ┌─────────────────────┐
        │        │ Panggil Naive Bayes │
        │        └──────────┬──────────┘
        │                   ↓
        │        ┌─────────────────────┐
        │        │ Proses Inferensi AI │
        │        └──────────┬──────────┘
        │                   ↓
        │             ┌───────────┐
        │             │  Berhasil?│
        │             └─────┬─────┘
        │              Tidak│Ya
        │                ↓   ↓
        │        ┌──────────┐ ┌──────────────────┐
        │        │ Fallback │ │ Hasil + Confidence│
        │        └────┬─────┘ └────────┬─────────┘
        │             │                ↓
        │             │        ┌──────────────┐
        │             │        │ Confidence   │
        │             │        │ memenuhi?    │
        │             │        └──────┬───────┘
        │             │          Tidak│Ya
        │             │            ↓   ↓
        │             │     ┌──────────┐ ┌──────────────┐
        │             │     │   Low    │ │ Simpan Hasil │
        │             │     │Confidence│ └──────┬───────┘
        │             │     └────┬─────┘        ↓
        │             │          │       ┌──────────────┐
        │             │          │       │ Tampilkan    │
        │             │          │       │ Hasil        │
        │             │          │       └──────┬───────┘
        └─────────────┴──────────┴──────────────┘
                                               ↓
                                         ┌──────────┐
                                         │  Selesai │
                                         └──────────┘
```

### Penanganan Input Tidak Valid

* Sistem melakukan validasi sebelum data dikirim ke AI.
* Data yang tidak memenuhi persyaratan tidak dikirim.
* Sistem memberikan pesan agar data diperbaiki.

### Penanganan Timeout

* Sistem menunggu sesuai batas waktu pada NFR.
* Jika batas waktu terlewati, proses dihentikan.
* Sistem mengembalikan `AI_TIMEOUT`.
* Data kunjungan tetap tersimpan.
* Pengguna dapat mencoba kembali.

### Penanganan Model Gagal

* Sistem tidak menetapkan hasil klasifikasi.
* Sistem mengembalikan `AI_MODEL_ERROR`.
* Pengguna dapat menjalankan proses kembali.

### Penanganan Low Confidence

* Sistem membandingkan confidence dengan threshold.
* Jika confidence di bawah threshold, hasil diberi status meragukan.
* Hasil tidak ditetapkan sebagai klasifikasi final.

### Retry dan Offline

Retry digunakan untuk kegagalan sementara seperti timeout atau gangguan koneksi.

**[KEPUTUSAN TIM: Tentukan jumlah maksimum retry]**

Jika mode offline belum ditetapkan pada SRS/HLD:

**[KEPUTUSAN TIM: Tentukan apakah mode offline termasuk scope implementasi]**

---

## 5. Traceability

| Elemen LLD               | FR    | NFR            |
| ------------------------ | ----- | -------------- |
| `GuestVisit`             | FR-01 | Usability      |
| `getVisits()`            | FR-02 | Performance    |
| `updateVisit()`          | FR-03 | Security       |
| `AnalyticsService`       | FR-04 | Performance    |
| `NaiveBayesService`      | FR-05 | AI Accuracy    |
| `predict()`              | FR-05 | AI Latency     |
| `validateConfidence()`   | FR-05 | AI Accuracy    |
| `/api/analytics/predict` | FR-05 | AI Latency     |
| `predictions`            | FR-06 | Data Integrity |
| `AI_TIMEOUT`             | FR-05 | AI Latency     |
| `LOW_CONFIDENCE`         | FR-05 | AI Accuracy    |
| `AI_MODEL_ERROR`         | FR-05 | Reliability    |

**Catatan:** ID dan nama NFR harus disesuaikan dengan `srs.md` dan HLD hasil revisi. LLD tidak boleh mengubah atau menambahkan requirement yang belum ditetapkan pada SRS.
