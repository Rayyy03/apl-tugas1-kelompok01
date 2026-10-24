# BAB I. Pendahuluan

## 1.1 Gambaran layanan inti
Layanan pengaduan dan pelaporan **AMANAH** (`https://umi.ac.id/amanah`) merupakan kanal resmi pada subsistem **Layanan Pendukung Kampus** di Universitas Muslim Indonesia (UMI) yang memfasilitasi sivitas akademika maupun masyarakat kampus untuk menyampaikan pengaduan, aspirasi, saran, apresiasi, serta permohonan informasi. Layanan ini menangani 15 kategori permasalahan—mulai dari operasional rutin seperti akademik, keuangan, layanan, dan sarana prasarana, hingga pelaporan sensitif (*whistleblowing*) seperti pelanggaran etika, gratifikasi, korupsi, kekerasan seksual, perundungan, dan diskriminasi.

Secara arsitektural, layanan inti AMANAH mencakup empat alur utama:
1. **Pengiriman laporan:** Pelapor mengisi formulir publik tanpa kewajiban *login* SSO di awal dengan memilih tingkat kerahasiaan identitas (**Terbuka**, **Rahasia**, atau **Anonim**), tingkat urgensi (**Rendah**, **Sedang**, **Tinggi**), objek unit/pihak terlapor, uraian kronologi, serta mengunggah berkas bukti pendukung.
2. **Penugasan ke unit (*disposisi*):** Pengelola memverifikasi laporan dan meneruskannya ke unit kerja atau fakultas terkait sesuai kategori dan objek laporan.
3. **Tindak lanjut:** Unit kerja menangani laporan sesuai jenis penyelesaian yang dibutuhkan (klarifikasi, mediasi, investigasi, perbaikan pelayanan, pemberian sanksi, atau tanggapan resmi) dan memperbarui status tiket.
4. **Umpan balik dan pelacakan:** Pelapor memantau perkembangan penanganan laporan secara mandiri melalui halaman pelacakan (`https://umi.ac.id/amanah/cek`) menggunakan kode tiket berformat `AMANAH-XXXXXX`.

## 1.2 Ruang lingkup (3-5 kasus penggunaan)
Ruang lingkup analisis dan perancangan arsitektur pada laporan ini mencakup empat kasus penggunaan (*use cases*) inti pada layanan AMANAH:

1. **Pengiriman Laporan Berjenjang (Terbuka/Rahasia/Anonim) dan Unggah Bukti:** Pelapor mengakses formulir AMANAH, memilih mode kerahasiaan identitas (di mana mode *Anonim* membebaskan pelapor dari pengisian data diri), memilih jenis dan kategori laporan, mengisi kronologi, serta mengunggah berkas bukti pendukung (format PDF, JPG, PNG, DOCX, MP4, atau MP3 dengan ukuran maksimal 10 MB) hingga memperoleh kode tiket `AMANAH-XXXXXX`.
2. **Verifikasi dan Penugasan Laporan ke Unit Kerja (*Disposisi*):** Admin pengelola AMANAH memeriksa kelengkapan laporan yang masuk, menyaring kesesuaian bukti, dan menugaskan penanganan laporan kepada unit kerja atau fakultas yang berwenang dengan tetap menyembunyikan data pelapor apabila berstatus *Rahasia*.
3. **Pembaruan Progres Tindak Lanjut oleh Unit Kerja:** Staf unit penerima penugasan menindaklanjuti laporan (seperti perbaikan layanan, mediasi, atau investigasi) dan mencatat pembaruan status beserta tanggapan resmi ke dalam sistem.
4. **Pelacakan Status Tiket dan Penyampaian Umpan Balik:** Pelapor memasukkan kode tiket `AMANAH-XXXXXX` pada halaman `/amanah/cek` untuk melihat riwayat tindak lanjut dari unit terkait serta memberikan umpan balik atas hasil penyelesaian laporan.

## 1.3 Sumber data
Analisis konteks dan perancangan arsitektur pada laporan ini didasarkan pada empat sumber data berikut tanpa memuat identitas pribadi:

1. **Pengalaman sebagai pengguna:** Menguji coba antarmuka halaman formulir pelaporan (`https://umi.ac.id/amanah`) dan halaman pelacakan status (`https://umi.ac.id/amanah/cek`). Dari pengamatan langsung, ditemukan bahwa formulir dapat diakses publik dengan tiga opsi privasi (*Terbuka, Rahasia, Anonim*) dan mendukung unggahan multimedia hingga 10 MB, namun mekanisme pengiriman salinan kode tiket `AMANAH-XXXXXX` maupun notifikasi perubahan status ke Email/WhatsApp pelapor belum dijelaskan secara eksplisit pada antarmuka halaman.
2. **Informasi publik:** Menelaah struktur kategori layanan, ketentuan kerahasiaan pelapor, serta daftar unit kerja pendukung yang tercantum pada portal resmi Universitas Muslim Indonesia (`umi.ac.id`).
3. **Wawancara singkat dengan *stakeholder* (5 responden):** Melakukan wawancara singkat kepada 5 responden di lingkungan UMI yang disamarkan dengan kode **R1 sampai R5**, terdiri atas:
   - **R1, R2, dan R3 (Mahasiswa UMI):** Menggali kebutuhan akan jaminan keamanan identitas saat melaporkan kasus sensitif (seperti perundungan atau fasilitas rusak), risiko lupa kode tiket `AMANAH-XXXXXX` jika tidak ada notifikasi otomatis, serta kebutuhan transparansi batas waktu tindak lanjut unit.
   - **R4 dan R5 (Staf Pengelola Layanan / Unit Kerja di UMI):** Menggali alur verifikasi laporan masuk, proses penerusan (*disposisi*) laporan ke fakultas atau unit teknis (seperti PDTI dan Biro Umum), serta kebutuhan rekapitulasi status penyelesaian laporan.
4. **Pengamatan langsung:** Mengamati proses komunikasi dan penanganan keluhan fasilitas serta layanan administrasi pada unit-unit kerja di lingkungan kampus UMI.
