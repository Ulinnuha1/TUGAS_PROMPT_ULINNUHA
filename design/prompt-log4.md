# PROMPT LOG

## 1. Penyusunan HLD

### Prompt yang Dikirim ke AI

Buat DRAF HLD (High Level Design) berdasarkan SRS hasil revisi untuk Sistem Informasi Buku Tamu Digital berbasis website.

Sistem memiliki fitur:
- Pencatatan data kunjungan tamu.
- Pengelolaan data kunjungan.
- Dashboard analitik.
- Analisis data menggunakan metode Naïve Bayes.

HLD harus mencakup:
1. Gambaran arsitektur sistem.
2. Komponen utama sistem dan tanggung jawabnya.
3. Alur komunikasi antar komponen.
4. Integrasi layanan AI Naïve Bayes.
5. Kontrak API tingkat tinggi.
6. Database dan hubungan antar komponen.
7. Keamanan dan kebutuhan non-fungsional.
8. Traceability komponen terhadap FR dan NFR.

Aturan:
- Turunkan desain dari SRS.
- Jangan mengubah requirement.
- Jangan masuk ke detail class, method, atau kode karena akan dibahas pada LLD.
- Jika terdapat keputusan teknologi yang belum ditentukan, tandai sebagai [KEPUTUSAN TIM].

### Draf Awal Hasil Generate

AI menghasilkan rancangan arsitektur dengan komponen utama:

User → Web Application → Backend/API → Database → Analytics Service → Naïve Bayes Service

Komponen yang dihasilkan:
- Web Application
- Backend/API
- Database
- Analytics Service
- Naïve Bayes Service

### Koreksi Manual Tim

- Memastikan HLD hanya membahas arsitektur tingkat tinggi.
- Menghapus detail implementasi yang seharusnya masuk LLD.
- Memastikan setiap komponen sesuai dengan kebutuhan pada SRS.
- Memastikan fitur Naïve Bayes memiliki integrasi dengan layanan AI.
- Menambahkan penanganan timeout dan kegagalan layanan AI.
- Menambahkan hubungan komponen dengan FR/NFR.
- Memberikan tanda [KEPUTUSAN TIM] pada teknologi yang belum ditentukan.

---

## 2. Penyusunan LLD

### Prompt yang Dikirim ke AI

Buat DRAF LLD (Low Level Design) untuk fitur prioritas Must berdasarkan SRS dan HLD hasil revisi.

LLD harus mencakup:
1. Desain modul/class untuk fitur Must terpenting termasuk fitur AI.
2. Skema data dan relasi.
3. Spesifikasi API detail.
4. Sequence/alur detail fitur AI.
5. Error handling dan fallback.
6. Traceability elemen desain terhadap FR/NFR.

Aturan:
- Turunkan rancangan dari SRS dan HLD.
- Jangan mengubah requirement.
- Nama class dan field menggunakan Bahasa Inggris.
- Penjelasan menggunakan Bahasa Indonesia.
- Pilihan teknologi atau library yang belum diputuskan ditandai sebagai [KEPUTUSAN TIM].

### Draf Awal Hasil Generate

AI menghasilkan modul utama:

- GuestVisit
- AnalyticsService
- NaiveBayesService

Entitas database:

- guest_visits
- predictions

API utama:

- POST /api/guest-visits
- GET /api/guest-visits
- POST /api/analytics/predict

Alur AI:

Validasi Input → Preprocessing → Pemanggilan Naïve Bayes → Inferensi Model → Prediction + Confidence → Validasi Confidence → Hasil/Fallback

Kode error:

- INVALID_INPUT
- AI_TIMEOUT
- LOW_CONFIDENCE
- AI_UNAVAILABLE
- AI_MODEL_ERROR

### Koreksi Manual Tim

- GuestVisit digunakan untuk pengelolaan data kunjungan.
- AnalyticsService digunakan untuk proses analitik.
- NaiveBayesService digunakan untuk proses klasifikasi AI.
- Relasi guest_visits dan predictions diperiksa kembali.
- API dilengkapi method, path, request, response, dan kode error.
- Alur AI diperjelas mulai dari validasi input sampai hasil klasifikasi.
- Penanganan timeout ditambahkan.
- Penanganan kegagalan model ditambahkan.
- Penanganan low confidence ditambahkan.
- Fallback disediakan ketika proses AI gagal.
- Tidak menambahkan requirement baru yang tidak terdapat pada SRS.
- Detail yang belum diputuskan diberi tanda [KEPUTUSAN TIM].

---

## 3. Review dan Validasi HLD

### Hasil Review

- Arsitektur sistem sesuai dengan kebutuhan SRS.
- Komponen utama dapat ditelusuri ke fitur sistem.
- Integrasi layanan AI telah dijelaskan.
- HLD tidak memasukkan detail class atau method.
- Hubungan antar komponen telah dijelaskan.
- Penanganan kegagalan layanan AI telah dipertimbangkan.

### Koreksi Akhir

HLD digunakan sebagai dasar penyusunan LLD. Detail implementasi yang belum dibutuhkan pada tingkat HLD dipindahkan ke tahap LLD.

---

## 4. Review dan Validasi LLD

### Hasil Review

- Modul/class dapat dipetakan ke FR.
- Skema data memiliki entitas dan relasi yang jelas.
- API memiliki request dan response.
- API memiliki kode error.
- Fitur AI memiliki alur validasi input.
- Fitur AI memiliki preprocessing.
- Fitur AI memiliki penanganan timeout.
- Fitur AI memiliki penanganan model error.
- Fitur AI memiliki penanganan low confidence.
- Fallback tersedia ketika AI gagal.
- Traceability FR/NFR telah disediakan.
- Tidak terdapat perubahan requirement secara diam-diam.

### Koreksi Akhir

LLD disesuaikan agar dapat menjadi dasar implementasi tanpa mengubah requirement yang telah ditetapkan pada SRS dan HLD.

---

## 5. Ringkasan Perubahan

| Dokumen | Draf AI | Koreksi Manual |
|---|---|---|
| HLD | Arsitektur dan komponen sistem | Disesuaikan agar tetap pada tingkat high-level |
| HLD | Integrasi AI | Diperjelas hubungan dengan Analytics Service |
| HLD | Komponen sistem | Dipetakan dengan FR/NFR |
| LLD | Modul GuestVisit | Dipertahankan dan diperjelas tanggung jawabnya |
| LLD | AnalyticsService | Dipertahankan untuk proses analitik |
| LLD | NaiveBayesService | Dipertahankan untuk proses AI |
| LLD | Database | Diperiksa entitas, relasi, dan constraint |
| LLD | API | Dilengkapi request, response, dan error |
| LLD | Alur AI | Ditambahkan timeout, low confidence, dan fallback |
| LLD | Traceability | Disesuaikan dengan FR/NFR |

## 6. Kesimpulan

HLD dan LLD dibuat dengan bantuan AI sebagai draf awal. Hasil generate kemudian diperiksa dan dikoreksi secara manual agar tetap sesuai dengan SRS, kebutuhan fitur Must, arsitektur sistem, serta fitur analisis Naïve Bayes. Keputusan teknis yang belum ditetapkan oleh tim tidak dianggap sebagai keputusan final dan diberi tanda [KEPUTUSAN TIM].
