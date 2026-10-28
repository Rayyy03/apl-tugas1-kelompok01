# B1. Identifikasi dan Klasifikasi Karakteristik
Penanggung Jawab: Muhammad Widyadhana Rafi' Putra

## 1. Daftar Kandidat Karakteristik Arsitektur
Berdasarkan analisis konteks dan kebutuhan layanan pengaduan **AMANAH**, berikut adalah 9 kandidat karakteristik arsitektur yang diklasifikasikan menurut kategori (operasional, struktural, lintas sektor) dan sifatnya (eksplisit atau implisit) mengacu pada kerangka *Fundamentals of Software Architecture* [2]:

| No | Kandidat Karakteristik | Kategori | Sifat | Alasan pada Layanan AMANAH |
|---|---|---|---|---|
| 1 | **Keamanan & Kerahasiaan (*Security & Confidentiality*)** | Lintas Sektor | Implisit & Eksplisit | Laporan aduan sering memuat informasi sensitif dan identitas pelapor yang wajib dilindungi dari akses tidak sah agar pelapor merasa aman dari intimidasi. |
| 2 | **Keandalan (*Reliability*)** | Operasional | Eksplisit | Setiap laporan yang dikirim pelapor beserta berkas buktinya harus dijamin tersimpan dan terkirim ke unit tujuan tanpa ada data tiket yang hilang atau gagal tercatat. |
| 3 | **Keterlacakan & Kemampuan Audit (*Auditability / Traceability*)** | Lintas Sektor | Eksplisit | Setiap tahapan laporan (pengiriman, penugasan ke unit, tindak lanjut, hingga umpan balik) wajib memiliki catatan waktu (*timestamp*) dan riwayat pengubah yang jelas untuk dievaluasi pimpinan. |
| 4 | **Kemudahan Perawatan (*Maintainability*)** | Struktural | Implisit | Struktur unit kerja kampus, kategori pengaduan, maupun aturan disposisi laporan dapat berubah mengikuti kebijakan kampus, sehingga kode harus mudah diperbarui tanpa merusak modul lain. |
| 5 | **Kinerja / Waktu Respons (*Performance / Responsiveness*)** | Operasional | Eksplisit | Halaman pengiriman laporan, pengunggahan foto bukti, dan pengecekan status tindak lanjut harus merespons dengan cepat agar pengguna tidak meninggalkan proses pelaporan. |
| 6 | **Ketersediaan (*Availability*)** | Operasional | Eksplisit | Insiden atau keluhan di lingkungan kampus dapat terjadi kapan saja, sehingga portal AMANAH harus siap diakses 24/7 oleh sivitas akademika. |
| 7 | **Kemudahan Penggunaan (*Usability*)** | Lintas Sektor | Eksplisit | Antarmuka pelaporan dan pelacakan tiket harus intuitif bagi seluruh pengguna kampus yang memiliki tingkat literasi digital beragam. |
| 8 | **Modularitas (*Modularity*)** | Struktural | Implisit | Pemisahan tanggung jawab kode antara modul pengiriman laporan, modul penugasan unit, modul tindak lanjut, dan modul umpan balik diperlukan agar pengembangan tim tidak saling bertabrakan. |
| 9 | **Kemudahan Perluasan (*Extensibility*)** | Struktural | Implisit | Sistem perlu mendukung penambahan kanal notifikasi baru (seperti email atau pesan instan) maupun integrasi dengan layanan kampus lain di masa mendatang. |

---

## 2. Pemilihan 3 Karakteristik Pendorong Utama (*Driving Characteristics*)
Untuk menentukan 3 karakteristik pendorong yang paling krusial bagi arsitektur layanan AMANAH, digunakan **tiga ciri karakteristik arsitektur** menurut Richards dan Ford [2] sebagai alat uji:
1. **Ciri 1 (Pertimbangan Desain Non-Domain):** Menentukan bagaimana fungsi sistem diimplementasikan di luar aturan domain bisnis murni.
2. **Ciri 2 (Memengaruhi Struktur Desain):** Menuntut keputusan struktural khusus pada modul, komponen, atau penempatan infrastruktur.
3. **Ciri 3 (Kritis bagi Keberhasilan Sistem):** Kegagalan memenuhi karakteristik ini akan membuat sistem ditinggalkan pengguna atau gagal mencapai tujuan utamanya.

Berdasarkan pengujian terhadap ketiga ciri tersebut serta keselarasan dengan kebutuhan signifikan (ASR) dan keputusan arsitektur (ADR) pada Bagian A, dipilih **3 karakteristik pendorong utama** berikut:

### 1. Keamanan dan Kerahasiaan (*Security & Confidentiality*) — [Lintas Sektor]
* **Mengapa paling penting:** Inti dari sistem pengaduan bernama "AMANAH" adalah kepercayaan (*trust*). Jika identitas pelapor atau isi laporan sensitif bocor ke pihak yang tidak berwenang, sivitas akademika tidak akan berani melapor dan sistem kehilangan fungsi utamanya (memenuhi **Ciri 3**).
* **Hasil uji tiga ciri:** Karakteristik ini berada di luar fungsi dasar pengisian formulir (**Ciri 1**) dan secara langsung memengaruhi struktur arsitektur (**Ciri 2**) karena mengharuskan adanya komponen autentikasi/otorisasi berbasis peran (*Role-Based Access Control*), penyamaran identitas pelapor (*anonymization/masking*) bagi unit yang hanya menangani teknis laporan, serta pembatasan akses penyimpanan berkas bukti.

### 2. Keandalan dan Keterlacakan (*Reliability & Auditability*) — [Operasional / Lintas Sektor]
* **Mengapa paling penting:** Masalah klasik layanan pengaduan kampus adalah laporan yang "menguap" tanpa kejelasan siapa unit yang menangani dan sudah sejauh mana tindak lanjutnya. Menjamin setiap laporan pasti sampai ke unit tujuan dan setiap perubahan statusnya tercatat secara akurat adalah kunci akuntabilitas layanan (memenuhi **Ciri 3**).
* **Hasil uji tiga ciri:** Keandalan pengiriman penugasan dan pencatatan jejak audit mengatur kualitas operasional sistem (**Ciri 1**) serta memengaruhi struktur komponen (**Ciri 2**), yaitu perlunya mekanisme penyimpanan log status (*status history/audit log*) yang permanen pada basis data serta komponen pengelola notifikasi/antrean penugasan agar tidak ada laporan yang terlewat saat diteruskan ke unit kerja.

### 3. Kemudahan Perawatan (*Maintainability*) — [Struktural]
* **Mengapa paling penting:** Layanan AMANAH melibatkan banyak unit kerja pendukung di UMI (PDTI, Biro Umum, Fakultas, dll.) yang alur disposisi dan kategorinya dapat berubah seiring kebijakan manajemen kampus, sementara tim pengembang/pemelihara internal terbatas (memenuhi **Ciri 3**).
* **Hasil uji tiga ciri:** Kemudahan perawatan bukan fitur yang dilihat langsung oleh pengguna akhir (**Ciri 1**), tetapi sangat menentukan pembagian struktur modul perangkat lunak (**Ciri 2**), yakni memisahkan lapisan tampilan, logika aturan penugasan/disposisi unit, logika tindak lanjut, dan akses data agar perubahan aturan disposisi tidak merombak modul lainnya.
