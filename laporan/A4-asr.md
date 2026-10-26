# A4. Kebutuhan Signifikan (ASR)
Penanggung jawab: Abrar Raynaldo Arifuddin (@Rayyy03)

Berdasarkan analisis konteks (A1), identifikasi *stakeholder* (A2), batasan sistem (A3), serta temuan wawancara dan pengamatan langsung pada layanan pengaduan **AMANAH UMI**, berikut adalah 4 **Kebutuhan Signifikan Arsitektur (*Architecturally Significant Requirements* / ASR)** yang paling kritikal bagi perancangan sistem:

## 1. ASR-01: Keamanan dan Pengendalian Akses Data Sensitif (*Security & Confidentiality*)
* **Deskripsi Kebutuhan:** Sistem wajib menyediakan mekanisme perlindungan data pelapor pada mode **Rahasia** dan **Anonim**, serta memastikan 15 kategori masalah (termasuk kasus sensitif seperti kekerasan seksual, perundungan, gratifikasi, dan korupsi) hanya dapat diakses oleh petugas atau unit kerja yang memiliki hak wewenang (*Role-Based Access Control*). 
* **Pengaruh pada Arsitektur:** Memaksa perancangan pemisahan logis antara data identitas pelapor dan isi utama laporan di dalam basis data, serta menuntut penerapan enkripsi data saat disimpan (*at rest*) maupun dikirimkan (*in transit*), agar identitas pelapor tidak bocor ke pihak yang dilaporkan.

## 2. ASR-02: Keandalan Pelacakan dan Pengiriman Notifikasi Tiket (*Reliability & Notification*)
* **Deskripsi Kebutuhan:** Karena pelapor tidak diwajibkan *login* menggunakan akun SSO di awal, sistem harus menjamin bahwa setiap pengiriman laporan dan berkas bukti berhasil menghasilkan kode tiket unik berformat `AMANAH-XXXXXX` yang dapat diandalkan untuk melacak progres di halaman `/amanah/cek` tanpa ada tiket yang hilang atau gagal tercatat.
* **Pengaruh pada Arsitektur:** Mengharuskan adanya komponen pencatatan status terpusat (*immutable audit trail*) serta antrean pesan (*message queue*) untuk menangani pengiriman kode tiket atau notifikasi perubahan status secara asinkron agar tidak membebani proses penyimpanan utama.

## 3. ASR-03: Kinerja dan Keandalan Pengunggahan Berkas Bukti (*Upload Performance & Reliability*)
* **Deskripsi Kebutuhan:** Sistem harus mampu menangani proses pengunggahan berkas bukti multimedia (format PDF, JPG, PNG, DOCX, MP4, MP3) dengan batas ukuran maksimal **10 MB** secara andal, memberikan indikator progres serta pesan kesalahan yang jelas jika koneksi pengguna tidak stabil saat mengunggah berkas besar.
* **Pengaruh pada Arsitektur:** Memerlukan pemisahan penyimpanan lampiran berkas dari basis data utama (misalnya menggunakan *object storage* terpisah) untuk mencegah lonjakan beban server saat banyak pengguna mengunggah berkas bukti secara bersamaan.

## 4. ASR-04: Ketertelusuran Alur Disposisi Lintas-Unit (*Workflow Traceability*)
* **Deskripsi Kebutuhan:** Sistem harus menyediakan alur kerja disposisi yang terstruktur untuk meneruskan laporan dari admin pengelola ke unit kerja atau fakultas yang tepat, serta mencatat setiap riwayat pengalihan, perubahan status, dan penanggung jawab secara transparan.
* **Pengaruh pada Arsitektur:** Menuntut desain komponen manajemen alur kerja (*workflow engine*) yang fleksibel untuk mendukung koordinasi lintas-unit di lingkungan UMI serta penyediaan tenggat waktu penanganan (*SLA tracking*).
