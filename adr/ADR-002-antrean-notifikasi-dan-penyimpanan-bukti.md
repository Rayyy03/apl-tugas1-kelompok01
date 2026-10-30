# ADR-002: Antrean Pesan untuk Notifikasi Status Tiket dan Pemisahan Penyimpanan Bukti

- **Status:** Diterima
- **Tanggal:** 25-10-2026
- **Pengambil keputusan:** MUHAMMAD WIDYADHANA RAFI PUTRA

## Context
Pelapor melacak tindak lanjut laporan pada halaman `/amanah/cek` menggunakan kode tiket `AMANAH-XXXXXX` dan dapat mengunggah berkas bukti pendukung (PDF, JPG, PNG, DOCX, MP4, MP3) dengan batas maksimal 10 MB. Pelapor berisiko kehilangan kode tiket jika tidak ada pengiriman notifikasi otomatis saat laporan dikirim atau saat status disposisi berubah. Akan tetapi, jika pengiriman notifikasi eksternal (Email/WhatsApp) diproses secara sinkron saat pengajuan laporan dan berkas multimedia 10 MB disimpan langsung di dalam basis data utama, server akan mengalami pelambatan (*bottleneck*) atau kegagalan simpan ketika terjadi lonjakan pelaporan maupun gangguan jaringan (terhubung dengan kode **ASR-02** dan **ASR-03** pada bagian A4).

## Decision
Kami akan menggunakan antrean pesan (*message queue*) berbasis peristiwa untuk memproses pengiriman kode tiket `AMANAH-XXXXXX` serta notifikasi perubahan status secara asinkron di latar belakang yang dilengkapi mekanisme percobaan ulang (*retry*) otomatis, serta memisahkan penyimpanan fisik berkas bukti pendukung (maksimal 10 MB) ke layanan penyimpanan berkas terpisah (*object/file storage*) dengan hanya menyimpan metadata dan tautan terenkripsinya di dalam basis data utama.

## Consequences
- **Dampak positif (Untung):** Proses pengiriman laporan, unggah bukti hingga 10 MB, dan pembaruan status tindak lanjut oleh unit kerja tetap cepat dan andal meskipun layanan pengirim pesan eksternal sedang lambat, serta menjaga ukuran basis data utama tetap ringan dan mudah dicadangkan.
- **Dampak negatif dan *trade-off* (Rugi):** Menambah komponen infrastruktur yang harus dikelola (*worker* antrean pesan dan *object storage*), ada jeda waktu beberapa detik (*eventual consistency*) sebelum notifikasi diterima pelapor, serta membutuhkan validasi kebersihan berkas jika pengunggahan dibatalkan.

## Compliance
Keputusan ini dipastikan kepatuhannya melalui tinjauan kode (*code review*) untuk memastikan tidak ada penyimpanan berkas biner (BLOB) di dalam tabel basis data utama, uji beban (*load testing*) pada pengunggahan berkas bukti mendekati 10 MB, serta pengujian simulasi gangguan layanan notifikasi untuk memverifikasi berjalannya mekanisme *retry* pada antrean pesan.
