# BAB I. Pendahuluan
Penanggung Jawab: Muhammad Widyadhana Rafi' Putra

## 1.1 Gambaran layanan inti
Layanan pengaduan dan pelaporan **AMANAH** (`https://umi.ac.id/amanah`) merupakan kanal resmi pada subsistem **Layanan Pendukung Kampus** di Universitas Muslim Indonesia (UMI) yang memfasilitasi sivitas akademika maupun masyarakat kampus untuk menyampaikan pengaduan, aspirasi, saran, apresiasi, serta permohonan informasi. Layanan ini menangani 15 kategori permasalahan—mulai dari operasional rutin seperti akademik, keuangan, pelayanan, dan sarana prasarana, hingga pelaporan sensitif (*whistleblowing*) seperti pelanggaran etika, gratifikasi, korupsi, kekerasan seksual, perundungan, dan diskriminasi.

Secara arsitektural, layanan inti AMANAH mencakup empat alur utama:
1. **Pengiriman laporan:** Pelapor mengisi formulir publik tanpa kewajiban *login* SSO di awal dengan memilih tingkat kerahasiaan identitas (**Terbuka**, **Rahasia**, atau **Anonim**), tingkat urgensi (**Rendah**, **Sedang**, **Tinggi**), objek unit/pihak terlapor, uraian kronologi, serta mengunggah berkas bukti pendukung.
2. **Penugasan ke unit (*disposisi*):** Pengelola memverifikasi laporan dan meneruskannya ke unit kerja atau fakultas terkait sesuai kategori dan objek laporan.
3. **Tindak lanjut:** Unit kerja menangani laporan sesuai jenis penyelesaian yang dibutuhkan (klarifikasi, mediasi, investigasi, perbaikan pelayanan, pemberian sanksi, atau tanggapan resmi) dan memperbarui status tiket.
4. **Umpan balik dan pelacakan:** Pelapor memantau perkembangan penanganan laporan secara mandiri melalui halaman pelacakan (`https://umi.ac.id/amanah/cek`) menggunakan kode tiket berformat `AMANAH-XXXXXX`.

## 1.2 Ruang lingkup (3-5 kasus penggunaan)
Ruang lingkup analisis dan perancangan arsitektur pada laporan ini mencakup empat kasus penggunaan (*use cases*) inti pada layanan AMANAH:

1. **Pengiriman Laporan Berjenjang (Terbuka/Rahasia/Anonim) dan Unggah Bukti:** Pelapor mengakses formulir AMANAH, memilih mode kerahasiaan identitas (di mana mode *Anonim* membebaskan pelapor dari pengisian data diri), memilih jenis dan kategori laporan, mengisi kronologi, serta mengunggah berkas bukti pendukung (format PDF, JPG, PNG, DOCX, MP4, atau MP3 dengan ukuran maksimal 10 MB) hingga memperoleh kode tiket `AMANAH-XXXXXX`.
2. **Verifikasi dan Penugasan Laporan ke Unit Kerja (*Disposisi*):** Admin pengelola AMANAH memeriksa kelengkapan laporan yang masuk, menyaring kesesuaian bukti, dan menugaskan penanganan laporan kepada unit kerja atau fakultas yang berwenang dengan tetap menyembunyikan data pelapor apabila berstatus *Rahasia*.
3. **Pembaruan Progres Tindak Lanjut oleh Unit Kerja:** Staf unit penerima penugasan menindaklanjuti laporan (seperti perbaikan pelayanan, mediasi, atau investigasi) dan mencatat pembaruan status beserta tanggapan resmi ke dalam sistem.
4. **Pelacakan Status Tiket dan Penyampaian Umpan Balik:** Pelapor memasukkan kode tiket `AMANAH-XXXXXX` pada halaman `/amanah/cek` untuk melihat riwayat tindak lanjut dari unit terkait serta memberikan umpan balik atas hasil penyelesaian laporan.

## 1.3 Sumber data
Pengumpulan data dalam analisis konteks dan perancangan arsitektur layanan AMANAH UMI dilakukan melalui empat sumber berikut tanpa menyertakan identitas pribadi:

1. **Pengalaman sebagai pengguna:** Menguji coba secara langsung antarmuka formulir pelaporan publik (`https://umi.ac.id/amanah`) dan halaman pelacakan status laporan (`https://umi.ac.id/amanah/cek`). Dari percobaan ditemukan bahwa sistem menyediakan 3 mode kerahasiaan (*Terbuka, Rahasia, Anonim*), 5 jenis laporan, 15 kategori permasalahan, unggahan bukti multimedia maksimal 10 MB (PDF, JPG, PNG, DOCX, MP4, MP3), serta pelacakan menggunakan kode tiket `AMANAH-XXXXXX`, namun belum menampilkan kepastian notifikasi otomatis saat status tiket berubah (dokumentasi tangkapan layar terlampir pada folder `bukti-data/`).
2. **Informasi publik:** Menelaah informasi resmi, struktur kategori pengaduan, dan unit kerja layanan pendukung pada situs resmi Universitas Muslim Indonesia (`umi.ac.id`).
3. **Wawancara singkat dengan *stakeholder* (5 responden):** Mewawancarai lima responden pengguna dan pengelola di lingkungan UMI tanpa mencantumkan identitas pribadi (rincian lengkap pada berkas `bukti-data/wawancara-01.md` s.d. `wawancara-05.md`), yang terdiri atas:
   - **R1 – Mahasiswa semester 5 (`wawancara-01.md`):** Menyampaikan kebutuhan akan petunjuk yang jelas dalam membedakan 5 jenis laporan dan 15 kategori permasalahan agar pelapor tidak salah memilih tujuan aduan, serta konfirmasi penerimaan tiket yang jelas.
   - **R2 – Mahasiswa semester 5 (`wawancara-02.md`):** Menyoroti kekhawatiran terkait kerahasiaan identitas dan isi lampiran bukti saat melaporkan kasus sensitif (seperti kekerasan seksual, perundungan, atau pelanggaran etika), sehingga menuntut pembatasan hak akses petugas dan kejelasan perbedaan mode *Terbuka, Rahasia*, serta *Anonim*.
   - **R3 – Mahasiswa semester 3 (`wawancara-03.md`):** Mengungkapkan kendala batas ukuran unggahan 10 MB untuk bukti video/dokumen, risiko gagal unggah saat jaringan tidak stabil, serta kebutuhan notifikasi otomatis agar pelapor tidak perlu memeriksa kode tiket `AMANAH-XXXXXX` berulang kali di halaman `/amanah/cek`.
   - **R4 – Staf admin pengelola layanan pengaduan (`wawancara-04.md`):** Menjelaskan kebutuhan verifikasi kelengkapan laporan, pengelompokan dan disposisi laporan ke unit kerja yang tepat sesuai tingkat urgensi, serta pencatatan riwayat perubahan status agar admin mengetahui unit mana yang sedang menangani tiket.
   - **R5 – Staf unit kerja penerima disposisi laporan (`wawancara-05.md`):** Menjelaskan kendala ketika menerima limpahan laporan yang informasinya kurang lengkap atau memerlukan koordinasi lintas-unit, sehingga membutuhkan riwayat disposisi terpusat, mekanisme pengalihan unit, serta pemantauan tenggat waktu tindak lanjut.
4. **Pengamatan langsung:** Mengamati alur pelaporan dan penanganan keluhan fasilitas maupun layanan administrasi pada unit-unit kerja di lingkungan kampus UMI.
