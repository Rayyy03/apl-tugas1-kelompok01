# BAB IV. Penutup

## 4.1 Kesimpulan

Berdasarkan hasil analisis konteks, pemangku kepentingan, kebutuhan arsitektural, serta perancangan struktur dan karakteristik kualitas pada layanan pengaduan dan pelaporan **AMANAH UMI** (`https://umi.ac.id/amanah`), dapat ditarik kesimpulan sebagai berikut:

1. **Konteks, Stakeholder, dan Batasan Arsitektur (Bagian A1–A3):**
   Layanan AMANAH beroperasi pada empat konteks yang saling berkaitan: secara **teknis** berjalan sebagai portal web publik tanpa *login* SSO yang melayani unggahan bukti multimedia hingga 10 MB dan pelacakan berbasis kode tiket `AMANAH-XXXXXX`; secara **siklus hidup proyek** memerlukan pengembangan iteratif tanpa menghentikan layanan aktif; secara **bisnis** menuntut akuntabilitas tindak lanjut lintas-unit kerja dengan sumber daya TI internal yang efisien; dan secara **profesional** menuntut perlindungan etika serta kerahasiaan identitas pelapor (*Terbuka, Rahasia, Anonim*) pada 15 kategori permasalahan. Pemetaan 7 *stakeholder* ke dalam matriks *Power/Interest* menempatkan Admin Pengelola, Unit Kerja Penerima Disposisi, Pimpinan Universitas, dan Satgas/Komite Etik pada kuadran *Manage Closely*, sedangkan Pelapor berada pada kuadran *Keep Informed*.
2. **Kebutuhan Signifikan (ASR) dan Keputusan Arsitektur / ADR (Bagian A4–A5):**
   Kebutuhan arsitektural paling kritis pada layanan AMANAH berfokus pada perlindungan kerahasiaan data pelapor dan bukti sensitif, keandalan pelacakan status tiket beserta notifikasinya, kinerja unggahan berkas bukti maksimal 10 MB, serta ketertelusuran alur disposisi antar-unit. Untuk menjawab kebutuhan tersebut, ditetapkan keputusan arsitektur berupa: (a) **ADR-001**, yaitu pemisahan logis data identitas pelapor dari isi laporan utama yang dikombinasikan dengan *Role-Based Access Control* (RBAC), *data masking* untuk mode *Rahasia*, dan pencatatan *audit log*; serta (b) **ADR-002**, yaitu penerapan antrean pesan (*message queue*) asinkron untuk pengiriman notifikasi status tiket dan pemisahan penyimpanan fisik lampiran bukti ke *object/file storage*.
3. **Karakteristik Pendorong, Atribut Terukur, dan Standar ISO/IEC 25010 (Bagian B1, B2, B4):**
   Dari 9 kandidat karakteristik yang diidentifikasi, pengujian menggunakan tiga ciri karakteristik arsitektur menetapkan **3 karakteristik pendorong utama (*driving characteristics*)**, yaitu: (1) **Keamanan dan Kerahasiaan (*Security & Confidentiality*)**, (2) **Keandalan dan Keterlacakan (*Reliability & Auditability*)**, serta (3) **Kemudahan Perawatan (*Maintainability*)**. Ketiga karakteristik ini telah dijabarkan ke dalam skenario atribut kualitas yang terukur secara kuantitatif serta dipetakan secara konsisten ke dalam karakteristik dan subkarakteristik standar mutu internasional **ISO/IEC 25010**.
4. **Struktur Desain dan Analisis *Trade-off* (Bagian B3 & B5):**
   Arsitektur layanan AMANAH direpresentasikan secara konsisten melalui tiga struktur desain—**Struktur Modul**, **Struktur Komponen dan Konektor (C&C)**, serta **Struktur Alokasi**—yang memisahkan tanggung jawab antara antarmuka publik, layanan manajemen tiket dan disposisi, pengelola privasi/RBAC, pekerja antrean notifikasi, basis data utama, dan penyimpanan objek bukti. Analisis *trade-off* menunjukkan bahwa demi menjamin kepercayaan sivitas akademika dan akuntabilitas penanganan aduan, arsitektur ini secara sadar memprioritaskan **keamanan berlapis (*Security*) dan keandalan jejak audit (*Reliability/Auditability*)** di atas kesederhanaan kueri dan kecepatan pemrosesan sinkron seketika, dengan memitigasi beban kinerja melalui pemrosesan latar belakang (*asynchronous queue*) dan penyimpanan berkas terpisah.

---

## 4.2 Saran

Untuk pengembangan dan penyempurnaan layanan pengaduan **AMANAH UMI** ke depan, disarankan langkah-langkah tindak lanjut berikut:

1. **Implementasi Notifikasi Tiket Otomatis Multi-Kanal:**
   Menambahkan fitur pengiriman salinan kode tiket `AMANAH-XXXXXX` dan pemberitahuan perubahan status tindak lanjut secara otomatis melalui Email atau WhatsApp menggunakan mekanisme antrean pesan (*message queue*) bagi pelapor mode *Terbuka* dan *Rahasia*, sehingga pelapor tidak kehilangan akses pelacakan apabila lupa menyimpan kode tiket di awal.
2. **Penerapan Pembersihan Metadata Berkas Bukti (*EXIF/Metadata Stripping*):**
   Pada laporan dengan mode **Anonim** dan **Rahasia**, sistem disarankan menghapus metadata tersembunyi (seperti nama pembuat dokumen pada file PDF/DOCX atau koordinat lokasi dan tipe perangkat pada foto JPG/PNG) secara otomatis saat berkas diunggah ke *object storage*, guna mencegah kebocoran identitas pelapor secara tidak sengaja melalui berkas lampiran.
3. **Penyediaan Dasbor Pemantauan Tenggat Waktu (*SLA Monitoring*) Lintas-Unit:**
   Mengembangkan fitur pengingat dan eskalasi otomatis pada modul disposisi apabila laporan berurgensi **Tinggi** belum ditindaklanjuti oleh unit kerja penerima melewati batas waktu layanan yang ditetapkan, guna meningkatkan kepastian tindak lanjut dan umpan balik bagi sivitas akademika UMI.
