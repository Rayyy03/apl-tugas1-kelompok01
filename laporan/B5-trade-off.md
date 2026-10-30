# B5. Analisis Trade-off
**Penanggung Jawab:** Abrar Raynaldo Arifuddin  

Dalam perancangan arsitektur sistem pengaduan dan pelaporan **AMANAH UMI**, tidak seluruh karakteristik kualitas dapat dimaksimalkan secara bersamaan tanpa menimbulkan dampak atau benturan (*trade-off*) satu sama lain. Peningkatan pada satu karakteristik sering kali menuntut pengorbanan atau kompromi pada karakteristik lainnya. Bagian ini mendokumentasikan analisis *trade-off* utama beserta keputusan mitigasinya pada sistem AMANAH.

---

## 1. Matriks Analisis Trade-off

| No. | Karakteristik A | Karakteristik B | Bentuk Konflik / Trade-off | Keputusan / Mitigasi Arsitektur |
|---|---|---|---|---|
| 1 | **Security & Confidentiality** (Keamanan & Kerahasiaan) | **Performance / Responsiveness** (Efisiensi Waktu Tanggap) | Penerapan enkripsi data berlapis, kontrol akses ketat (RBAC), pencatatan *audit log*, serta penyamaran identitas (*data masking*) pada laporan berstatus Rahasia menambah waktu pemrosesan kueri oleh server dan memperpanjang waktu respons. | Memisahkan tabel data identitas secara logis, melakukan pengindeksan basis data yang optimal pada kolom kunci tiket, serta membatasi pemeriksaan otorisasi hanya pada endpoint layanan yang membutuhkan saja. |
| 2 | **Reliability & Auditability** (Keandalan & Keterlacakan) | **Maintainability & Flexibility** (Kemudahan Pemeliharaan) | Pencatatan riwayat perubahan status (*audit trail*) yang sangat rinci dan terpusat di setiap tahapan disposisi membuat struktur basis data dan kode sumber menjadi lebih terikat (*tightly coupled*), sehingga sulit diubah jika struktur unit kampus berubah. | Menerapkan pola perancangan berlapis (*layered architecture*) dan menggunakan layanan antrean pesan terpisah agar perubahan logika bisnis notifikasi tidak merusak struktur tabel pencatatan riwayat tiket utama. |
| 3 | **Performance / Responsiveness** (Kinerja / Waktu Tanggap) | **Reliability & Recoverability** (Keandalan & Pemulihan Sistem) | Pengunggahan berkas bukti pendukung berukuran besar (mendekati batas maksimal 10 MB yang mencakup dokumen PDF maupun video MP4) dapat membebani server utama dan memperlambat waktu tanggap bagi pengguna lain jika disimpan secara langsung. | Menggunakan arsitektur penyimpanan eksternal terpisah (*object/file storage*) untuk berkas multimedia dan memproses pengiriman notifikasi status secara asinkron menggunakan antrean pesan (*message queue*). |

---

## 2. Pembahasan Mendalam Benturan Karakteristik Utama

### 2.1 Keamanan (*Security*) vs. Kinerja Akses (*Performance*)
Pada layanan AMANAH, pelapor dapat memilih mode **Rahasia** di mana data diri (Nama, NIM/NIP, kontak) wajib diisi oleh pelapor tetapi harus disembunyikan dari staf unit kerja yang menerima disposisi laporan. 
* **Analisis Benturan:** Untuk memastikan keamanan data pelapor, sistem harus melakukan validasi peran pengguna (*RBAC*) dan memfilter kolom identitas setiap kali kueri data laporan ditarik oleh unit kerja. Proses validasi berlapis ini berisiko meningkatkan latensi dan menurunkan kecepatan respons (*responsiveness*) halaman pemantauan unit.
* **Mitigasi:** Tim memutuskan untuk menerapkan teknik *data masking* di tingkat aplikasi serta memisahkan tabel relasi data diri dari tabel inti pengaduan, sehingga kueri data umum tidak terbebani oleh pengecekan enkripsi yang tidak perlu.

### 2.2 Keandalan Pencatatan (*Reliability*) vs. Kompleksitas Pemeliharaan (*Maintainability*)
Pengelola layanan dan pimpinan kampus menuntut akuntabilitas yang tinggi melalui riwayat perubahan status (*audit trail*) yang transparan dari pelaporan awal hingga penutupan tiket.
* **Analisis Benturan:** Semakin detail riwayat log dicatat untuk menjamin keandalan dan audit, semakin kompleks hubungan antar-tabel dalam basis data. Hal ini berdampak negatif pada *maintainability*, di mana pengembang akan kesulitan melakukan modifikasi struktur kategori atau perubahan alur unit kerja di masa depan.
* **Mitigasi:** Log pencatatan riwayat status distandarisasi ke dalam modul layanan tersendiri (*logging service*), sehingga perubahan struktur unit kerja tidak mengharuskan perombakan total pada logika inti pencatatan tiket.

---

## 3. Kesimpulan Analisis
Berdasarkan analisis *trade-off* di atas, arsitektur sistem AMANAH UMI menitikberatkan prioritas utama pada **Security & Confidentiality** serta **Reliability & Auditability** untuk melindungi pelapor dan menjaga akuntabilitas kampus, dengan tetap menjaga batas toleransi kinerja melalui pemisahan penyimpanan berkas (*object storage*) dan penggunaan antrean asinkron.
