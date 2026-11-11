# A3. Batasan Sistem

**Penanggung Jawab:** Alif F. Fauzan  

## 1. Tujuan

Identifikasi batasan dilakukan untuk mengetahui faktor-faktor yang dapat memengaruhi pengembangan dan pengoperasian sistem AMANAH. Batasan dikelompokkan menjadi tiga kategori, yaitu batasan teknologi, bisnis, dan operasional.

## 2. Batasan Teknologi

Batasan teknologi merupakan faktor yang berkaitan dengan infrastruktur, perangkat lunak, keamanan, dan kemampuan teknis sistem.

| No. | Batasan Teknologi | Penjelasan | Dampak terhadap Arsitektur |
|---|---|---|---|
| 1 | Infrastruktur Server | Sistem membutuhkan server yang mampu menangani pengiriman laporan dan penyimpanan data. | Arsitektur harus mendukung penggunaan sumber daya server secara efisien. |
| 2 | Keamanan Data | Identitas pelapor dan isi laporan harus dilindungi dari akses tidak sah. | Membutuhkan autentikasi, otorisasi, dan pembatasan hak akses. |
| 3 | Penyimpanan Data | Sistem harus mampu menyimpan laporan dan berkas bukti yang diunggah pengguna. | Membutuhkan pengelolaan basis data dan penyimpanan berkas. |
| 4 | Koneksi Internet | Sistem berbasis web membutuhkan koneksi internet untuk mengakses layanan. | Antarmuka harus menangani kegagalan koneksi dan pengiriman data. |
| 5 | Kompatibilitas Perangkat | Sistem harus dapat digunakan melalui berbagai perangkat dan browser. | Tampilan perlu dirancang responsif dan kompatibel. |

## 3. Batasan Bisnis

Batasan bisnis merupakan faktor yang berkaitan dengan kebijakan kampus, kebutuhan pengguna, anggaran, dan proses pelayanan pengaduan.

| No. | Batasan Bisnis | Penjelasan | Dampak terhadap Arsitektur |
|---|---|---|---|
| 1 | Kebijakan Kampus | Sistem harus mengikuti kebijakan dan aturan pengelolaan pengaduan di lingkungan kampus. | Alur pengaduan harus dapat disesuaikan dengan kebijakan kampus. |
| 2 | Struktur Unit Kerja | Setiap laporan harus diarahkan kepada unit kerja yang sesuai dengan permasalahan. | Membutuhkan modul pengelolaan kategori dan disposisi laporan. |
| 3 | Kerahasiaan Pelapor | Identitas pelapor harus dijaga agar pengguna merasa aman ketika menyampaikan pengaduan. | Membutuhkan pengaturan akses berdasarkan peran. |
| 4 | Keterbatasan Anggaran | Pengembangan dan pemeliharaan sistem perlu mempertimbangkan biaya yang tersedia. | Pemilihan teknologi harus mempertimbangkan biaya implementasi dan pemeliharaan. |
| 5 | Akuntabilitas Pelayanan | Setiap laporan harus memiliki status dan riwayat penanganan yang jelas. | Membutuhkan kode tiket dan pencatatan riwayat aktivitas. |

## 4. Batasan Operasional

Batasan operasional merupakan faktor yang berkaitan dengan penggunaan, pemeliharaan, pengelolaan, dan aktivitas sehari-hari sistem.

| No. | Batasan Operasional | Penjelasan | Dampak terhadap Arsitektur |
|---|---|---|---|
| 1 | Ketersediaan Pengelola | Sistem membutuhkan petugas yang bertanggung jawab mengelola dan menindaklanjuti laporan. | Membutuhkan pembagian hak akses dan tanggung jawab pengguna. |
| 2 | Pemeliharaan Sistem | Sistem perlu diperbarui dan diperbaiki secara berkala. | Arsitektur harus memiliki modul yang mudah dipelihara. |
| 3 | Volume Pengaduan | Sistem dapat menerima banyak laporan dalam waktu bersamaan. | Membutuhkan pengelolaan proses penyimpanan dan pemrosesan laporan. |
| 4 | Kemampuan Pengguna | Pengguna memiliki tingkat pemahaman teknologi yang berbeda-beda. | Antarmuka harus sederhana dan mudah digunakan. |
| 5 | Penanganan Gangguan | Gangguan server atau jaringan dapat menghambat pelayanan. | Membutuhkan pencadangan data dan mekanisme pemulihan sistem. |

## 5. Hubungan Batasan dengan Karakteristik Pendorong

| No. | Batasan | Karakteristik Pendorong | Hubungan |
|---|---|---|---|
| 1 | Keamanan dan kerahasiaan data | Security & Confidentiality | Melindungi identitas dan informasi laporan. |
| 2 | Gangguan server dan kehilangan data | Reliability & Auditability | Menjaga laporan tetap tersimpan dan dapat ditelusuri. |
| 3 | Perubahan kategori dan unit kerja | Maintainability | Mempermudah perubahan aturan tanpa merusak modul lain. |
| 4 | Banyaknya laporan bersamaan | Reliability & Performance | Menjaga keberhasilan pencatatan dan waktu respons sistem. |
| 5 | Perbedaan kemampuan pengguna | Usability | Mempermudah pengguna dalam mengirim dan memantau laporan. |

## 6. Kesimpulan

Berdasarkan identifikasi yang dilakukan, sistem AMANAH memiliki batasan teknologi, bisnis, dan operasional yang harus diperhatikan dalam proses pengembangan.

Batasan teknologi berfokus pada keamanan, server, penyimpanan, dan koneksi internet. Batasan bisnis berhubungan dengan kebijakan kampus, struktur unit kerja, anggaran, dan kerahasiaan pelapor. Sementara itu, batasan operasional berhubungan dengan pengelolaan laporan, pemeliharaan sistem, kemampuan pengguna, dan penanganan gangguan.

Seluruh batasan tersebut menjadi pertimbangan dalam menentukan arsitektur agar sistem AMANAH dapat berjalan dengan aman, andal, dan mudah dikembangkan.

