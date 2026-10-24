# BAB I. Pendahuluan

## 1.1 Gambaran layanan inti
Layanan pengaduan dan pelaporan **AMANAH** merupakan salah satu layanan inti pada subsistem **Layanan Pendukung Kampus** di lingkungan Universitas Muslim Indonesia (UMI). Layanan ini berfungsi sebagai kanal resmi bagi sivitas akademika (mahasiswa, dosen, tenaga kependidikan) maupun pemangku kepentingan terkait untuk menyampaikan aspirasi, keluhan, dan pelaporan kendala layanan di lingkungan kampus secara terpusat. Secara arsitektural, layanan inti AMANAH mencakup empat alur proses utama, yaitu: (1) pengiriman laporan oleh pelapor, (2) verifikasi dan penugasan (*disposisi*) laporan ke unit kerja terkait, (3) penanganan serta pembaruan tindak lanjut oleh unit kerja, dan (4) penyampaian umpan balik (*feedback*) atas penyelesaian laporan kepada pelapor.

## 1.2 Ruang lingkup (3-5 kasus penggunaan)
Ruang lingkup analisis dan perancangan arsitektur pada laporan ini dibatasi pada empat kasus penggunaan (*use cases*) utama sesuai alur layanan inti AMANAH:

1. **Pengiriman Laporan dan Bukti Pendukung:** Pelapor mengakses portal AMANAH (`umi.ac.id/amanah`), memilih kategori laporan, mengisi uraian pengaduan, melampirkan berkas bukti pendukung (seperti foto atau dokumen), dan mengirimkan laporan ke dalam sistem untuk mendapatkan tanda terima/nomor tiket pelaporan.
2. **Verifikasi dan Penugasan ke Unit Terkait (*Disposisi*):** Pengelola/Admin AMANAH memeriksa kelengkapan dan validitas laporan yang masuk, lalu meneruskan (*assign*) laporan tersebut ke unit kerja yang berwenang di lingkungan UMI (misalnya PDTI untuk kendala jaringan/akun, Biro Umum untuk fasilitas, atau pihak Fakultas).
3. **Pelaksanaan dan Pembaruan Tindak Lanjut:** Staf unit kerja penerima penugasan menerima notifikasi laporan, melakukan penanganan di lapangan atau pada sistem terkait, serta memperbarui status progres dan bukti penyelesaian tindak lanjut di dalam sistem AMANAH.
4. **Penyampaian Umpan Balik (*Feedback*) dan Penutupan Laporan:** Pelapor memantau status perkembangan tindak lanjut laporannya dan memberikan umpan balik atau penilaian kepuasan setelah laporan dinyatakan selesai oleh unit terkait.

## 1.3 Sumber data
Pengumpulan data untuk analisis konteks, kebutuhan arsitektural, dan perancangan struktur layanan AMANAH dilakukan melalui empat sumber berikut tanpa menyertakan identitas pribadi responden:

1. **Pengalaman sebagai pengguna:** Mencoba secara langsung alur antarmuka pada laman layanan AMANAH UMI (`https://umi.ac.id/amanah`) untuk mengamati formulir pengajuan laporan, kategori pengaduan, mekanisme lampiran bukti, serta alur pelacakan status laporan. `[CEK LAPANGAN: Tambahkan 1 kalimat kendala/temuan nyata saat kamu membuka webnya]`.
2. **Informasi publik:** Menelaah informasi resmi, panduan layanan pengaduan, serta struktur unit layanan pendukung yang dipublikasikan melalui situs web resmi Universitas Muslim Indonesia (`umi.ac.id`).
3. **Wawancara singkat dengan *stakeholder* (5 responden):** Melakukan wawancara dan kuesioner singkat kepada 5 orang responden di lingkungan UMI yang identitasnya disamarkan menjadi kode **R1 sampai R5**, terdiri atas:
   - **R1, R2, dan R3 (Mahasiswa UMI):** Menggali pengalaman dan ekspektasi terkait kemudahan pelaporan, kecepatan tanggapan, transparansi status tindak lanjut, serta jaminan kerahasiaan identitas pelapor. `[CEK LAPANGAN: Sesuaikan dengan hasil wawancara nyata kelompokmu]`.
   - **R4 dan R5 (Staf/Pengelola Unit Layanan di lingkungan UMI):** Menggali proses penerimaan limpahan laporan dari sistem AMANAH, kendala koordinasi lintas unit, serta kebutuhan pencatatan bukti tindak lanjut. `[CEK LAPANGAN: Sesuaikan dengan hasil wawancara nyata kelompokmu]`.
4. **Pengamatan langsung:** Mengamati alur penyelesaian keluhan layanan fasilitas dan administrasi secara langsung di lingkungan kampus UMI.
