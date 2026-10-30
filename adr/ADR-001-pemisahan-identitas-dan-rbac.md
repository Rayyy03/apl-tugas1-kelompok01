# ADR-001: Pemisahan Data Identitas Pelapor dan Kontrol Akses Berbasis Peran (RBAC)

- **Status:** Diterima
- **Tanggal:** 25-10-2026
- **Pengambil keputusan:** AMUHAMMAD WIDYADHANA RAFI PUTRA

## Context
Layanan pengaduan AMANAH UMI menyediakan tiga pilihan kerahasiaan identitas (Terbuka, Rahasia, dan Anonim) tanpa login SSO di awal serta menangani 15 kategori permasalahan, termasuk laporan sensitif seperti kekerasan seksual, perundungan, diskriminasi, gratifikasi, dan korupsi. Pada mode Rahasia, pelapor tetap mengisi data diri (Nama, NIM/NIP, nomor HP/WhatsApp, dan email), namun identitas tersebut tidak boleh diketahui oleh unit kerja atau pihak yang dilaporkan. Batasan operasional dan etika kampus menuntut perlindungan ketat terhadap saksi/pelapor (terhubung dengan kebutuhan signifikan **ASR-01** pada bagian A4 terkait keamanan dan kerahasiaan data).

## Decision
Kami akan memisahkan penyimpanan data identitas pelapor dari tabel utama isi laporan secara logis pada basis data, menerapkan kontrol akses berbasis peran (*Role-Based Access Control* / RBAC), serta melakukan penyamaran identitas otomatis (*data masking*) ketika laporan berstatus Rahasia diteruskan (*disposisi*) ke unit kerja penerima laporan. Kami juga akan membatasi akses unduhan berkas bukti pendukung (maksimal 10 MB) hanya bagi petugas berwenang dan mencatat setiap aktivitas pembacaan laporan sensitif ke dalam *audit log*.

## Consequences
- **Dampak positif (Untung):** Kerahasiaan identitas pelapor pada mode Rahasia dan Anonim terlindungi dari akses unit kerja yang tidak berwenang, meningkatkan kepercayaan sivitas akademika untuk melapor, serta menyediakan jejak audit (*audit trail*) atas setiap akses laporan sensitif.
- **Dampak negatif dan *trade-off* (Rugi):** Menambah kompleksitas kueri pemisahan data dan pengecekan otorisasi pada setiap permintaan halaman disposisi (sedikit menambah waktu pemrosesan dibandingkan tanpa pemeriksaan berlapis), serta mengharuskan pengelola sistem/PDTI mengatur hak akses peran tiap unit secara disiplin.

## Compliance
Keputusan ini dipastikan kepatuhannya melalui tinjauan skema basis data dan pengujian otorisasi (*access control testing*) menggunakan akun simulasi staf unit kerja untuk memverifikasi bahwa kolom identitas pelapor berstatus Rahasia tidak muncul pada antarmuka maupun respons API unit kerja, serta pemantauan pencatatan *audit log* setiap kali laporan sensitif dibuka.
