# A5. Keputusan Arsitektur dan ADR

## Ringkasan keputusan
1. **ADR-001 — Pemisahan modul layanan:** logika pengaduan, penugasan, tindak lanjut, umpan balik, notifikasi, serta audit dan akses dipisahkan berdasarkan tanggung jawab. Tujuannya mempermudah perubahan, pengujian, dan pemeliharaan.
2. **ADR-002 — Keamanan dan audit:** menerapkan autentikasi, hak akses berbasis peran, HTTPS, dan pencatatan aktivitas penting untuk menjaga kerahasiaan serta ketertelusuran laporan.

ADR lengkap disimpan pada folder `adr/` di repository kelompok. Ringkasan ini dapat dimasukkan ke bagian A5 pada laporan utama.

## Rencana komunikasi
- **Penyimpanan:** `adr/ADR-001-pemisahan-modul.md` dan `adr/ADR-002-keamanan-dan-audit.md`; ringkasan A5 dimasukkan ke laporan utama.
- **Pemberitahuan:** setiap keputusan atau perubahan ADR diberitahukan melalui kanal komunikasi kelompok dengan tautan langsung ke berkas/commit. Anggota yang bertanggung jawab pada implementasi, pengujian, dokumentasi, dan integrasi wajib meninjau keputusan terkait.
- **Persetujuan dan perubahan:** perubahan substantif diajukan sebagai pull request atau perubahan yang dapat ditinjau, disertai alasan, dampak, dan pengujian. Status ADR diperbarui bila keputusan diganti.

## Cara menghindari tiga anti-pattern
- **Covering Your Assets:** keputusan tidak hanya ditulis untuk membuktikan bahwa seseorang pernah menyampaikan pendapat. ADR memuat konteks, alasan, konsekuensi positif dan negatif, serta bukti kepatuhan/pengujian.
- **Groundhog Day:** sebelum mengusulkan keputusan baru, anggota memeriksa folder `adr/` dan riwayat commit. Keputusan lama yang relevan ditautkan dan diperbarui, bukan dibahas ulang tanpa konteks.
- **Email-Driven Architecture:** email atau chat hanya dipakai sebagai notifikasi, bukan tempat utama keputusan. Versi resmi disimpan di repository, ditinjau melalui pull request/commit, dan perubahan dicatat dalam riwayat.

## Catatan validasi
Isi ADR di atas merupakan rekomendasi desain akademik berdasarkan ruang lingkup layanan dalam dokumen tugas. Struktur teknis dan kebijakan aktual AMANAH belum diverifikasi; kelompok perlu menyesuaikannya dengan hasil pengamatan, sumber publik, atau wawancara yang sah.

