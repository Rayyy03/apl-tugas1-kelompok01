# BAB IV. Penutup

Penanggung jawab: Muhammad Widyadhana Rafi' Putra (@Kiano-Ksl)

## 4.1 Kesimpulan

Berdasarkan hasil analisis konteks, pemangku kepentingan, kebutuhan signifikan arsitektur, serta perancangan struktur dan karakteristik kualitas pada layanan pengaduan dan pelaporan **AMANAH UMI** (`https://umi.ac.id/amanah`), dapat disimpulkan empat poin utama berikut:

1. **Konteks, Stakeholder, dan Batasan Sistem (A1–A3):**
   Layanan AMANAH beroperasi pada empat konteks arsitektur yang saling terhubung: secara **teknis** berjalan sebagai aplikasi web publik tanpa *login* SSO di awal yang melayani unggahan berkas bukti hingga 10 MB (PDF, JPG, PNG, DOCX, MP4, MP3) dan pelacakan berbasis kode tiket `AMANAH-XXXXXX` di `/amanah/cek`; secara **siklus hidup proyek** membutuhkan pengembangan iteratif tanpa menghentikan operasional layanan; secara **bisnis** menuntut kepastian waktu tanggap (*SLA*) tindak lanjut lintas-unit dengan sumber daya TI internal yang efisien; dan secara **profesional** menuntut perlindungan kerahasiaan identitas pelapor (*Terbuka, Rahasia, Anonim*) pada 15 kategori permasalahan. Pemetaan 7 *stakeholder* pada matriks *Power/Interest* menempatkan Admin Pengelola, Unit Kerja/Fakultas Penerima Disposisi, Pimpinan Universitas, dan Satgas PPKS/Komite Etik pada kuadran *Manage Closely*, Tim Pengembang/PDTI pada kuadran *Keep Satisfied*, serta Pelapor pada kuadran *Keep Informed*.
2. **Kebutuhan Signifikan Arsitektur (ASR) dan Keputusan Arsitektur / ADR (A4–A5):**
   Perancangan sistem didorong oleh empat kebutuhan signifikan arsitektur, yaitu keamanan dan pengendalian akses data sensitif (**ASR-01**), keandalan pelacakan dan pengiriman notifikasi tiket (**ASR-02**), kinerja dan keandalan pengunggahan berkas bukti 10 MB (**ASR-03**), serta ketertelusuran alur disposisi lintas-unit (**ASR-04**). Keempat ASR tersebut dijawab melalui dua keputusan arsitektur utama pada folder `/adr`: (a) **ADR-001**, yang menetapkan pemisahan logis data identitas pelapor dari tabel isi laporan utama, penerapan *Role-Based Access Control* (RBAC), penyamaran identitas (*data masking*) pada mode *Rahasia*, dan pencatatan *audit log* disposisi; serta (b) **ADR-002**, yang menetapkan penggunaan antrean pesan (*message queue*) asinkron untuk notifikasi status tiket dan pemisahan penyimpanan fisik berkas bukti 10 MB ke *object/file storage*.
3. **Karakteristik Pendorong, Atribut Kualitas Terukur, dan Pemetaan ISO/IEC 25010 (B1, B2, B4):**
   Dari 9 kandidat karakteristik yang diidentifikasi, pengujian menggunakan tiga ciri karakteristik arsitektur menghasilkan **3 karakteristik pendorong utama (*driving characteristics*)**, yaitu: (1) **Keamanan dan Kerahasiaan (*Security & Confidentiality*)**, (2) **Keandalan dan Keterlacakan (*Reliability & Auditability*)**, serta (3) **Kemudahan Perawatan (*Maintainability*)**. Ketiganya telah diturunkan menjadi skenario atribut kualitas terukur secara kuantitatif serta dipetakan secara konsisten ke dalam standar mutu **ISO/IEC 25010** (*Security*, *Reliability*, *Functional Suitability*, *Maintainability*, dan *Performance Efficiency*).
4. **Tiga Struktur Desain dan Analisis *Trade-off* (B3 & B5):**
   Arsitektur layanan AMANAH divisualisasikan secara konsisten melalui **Struktur Modul**, **Struktur Komponen dan Konektor (C&C)**, serta **Struktur Alokasi** yang memisahkan lapisan antarmuka publik, pengelola tiket dan disposisi, pengendali privasi/RBAC, pekerja antrean notifikasi, basis data utama, dan penyimpanan objek bukti. Analisis *trade-off* menegaskan bahwa arsitektur ini memprioritaskan perlindungan kerahasiaan pelapor (*Security*) serta keutuhan jejak audit disposisi (*Reliability & Auditability*) di atas kecepatan pemrosesan sinkron langsung, dengan memitigasi beban waktu respons melalui antrean asinkron dan penyimpanan berkas terpisah.

## 4.2 Saran

Untuk pengembangan dan penyempurnaan arsitektur layanan pengaduan **AMANAH UMI** pada tahap selanjutnya, disarankan tiga langkah berikut:

1. **Integrasi Pengiriman Salinan Kode Tiket dan Notifikasi Multi-Kanal:**
   Mengimplementasikan pengiriman salinan kode tiket `AMANAH-XXXXXX` dan pemberitahuan perubahan status tindak lanjut secara otomatis melalui Email atau WhatsApp berbasis antrean pesan (*message queue*) bagi pelapor mode *Terbuka* dan *Rahasia*, sehingga mencegah risiko pelapor kehilangan akses pelacakan apabila lupa mencatat kode tiket di awal.
2. **Pembersihan Metadata Otomatis pada Lampiran Bukti (*Metadata Stripping*):**
   Menambahkan proses penghapusan metadata otomatis (seperti informasi nama penulis dokumen PDF/DOCX atau koordinat lokasi EXIF pada foto JPG/PNG) saat berkas diunggah oleh pelapor mode **Anonim** dan **Rahasia** ke *object storage*, guna menutup celah kebocoran identitas pelapor dari sisi file bukti.
3. **Fitur Pengingat dan Eskalasi Tenggat Waktu (*SLA Monitoring*) Lintas-Unit:**
   Menambahkan mekanisme pengingat otomatis dan eskalasi berjenjang pada komponen manajemen disposisi apabila laporan berurgensi **Tinggi** belum ditindaklanjuti oleh unit kerja penerima dalam batas waktu layanan yang ditetapkan kampus.
