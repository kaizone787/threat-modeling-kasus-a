# Threat Modeling STRIDE — Kasus A (Kelompok 10)

Repositori ini berisi model *threat modeling* berbasis **STRIDE** menggunakan **OWASP Threat Dragon** untuk mata kuliah **Keamanan Siber (CAK3CAB3)** — **Kelompok 10**, Studi Kasus A (*Sistem Presensi Perkuliahan Berbasis QR Code*), dosen pengampu **Kharisma Monika Dian Pertiwi**.

## Anggota Kelompok & Pembagian Tugas

| Peran               | Nama                     | NIM              | Fokus Utama & Tanggung Jawab                                                                                                                     |
| :------------------ | :----------------------- | :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Anggota 1** | Muhammad Chaesar Pratama | `103072400119` | **DFD & Threat Analysis (S, T)**: Identifikasi aset/aktor, penyusunan DFD, trust boundary, serta analisis ancaman T01, T02, T03, T09.       |
| **Anggota 2** | Hendra Dirga Dwi Saputra | `103072430018` | **Authentication & Data Security (R, I)**: Analisis alur autentikasi, integrasi Threat Dragon, serta analisis ancaman T04, T05, T06, T11.  |
| **Anggota 3** | Laura Chyndearni Saragih | `103072400049` | **Validation & Admin Security (D, E)**: Analisis validasi backend, kalibrasi risiko, QA, ekspor PDF, serta analisis ancaman T07, T08, T10. |

## Pembagian Beban Kerja

| Pekerjaan                            |   Anggota 1   | Anggota 2 | Anggota 3 |
| :----------------------------------- | :-----------: | :-------: | :-------: |
| Identifikasi aset, aktor, dan asumsi |      ✓      |    ✓    |    ✓    |
| Penyusunan DFD & Trust Boundary      | ✓ *(Lead)* |  Review  |  Review  |
| Analisis STRIDE & Risk Assessment    |   4 Ancaman   | 4 Ancaman | 3 Ancaman |
| Perumusan Mitigasi Spesifik          |      ✓      |    ✓    |    ✓    |
| Input Ancaman ke Threat Dragon       |      ✓      |    ✓    |    ✓    |
| Review Konsistensi & QA Akhir        |      ✓      |    ✓    |    ✓    |
| Ekspor Laporan (JSON & PDF)          |    Bersama    |  Bersama  |  Bersama  |

## Alur Pengerjaan Bersama

1. **Tahap 1 – Diskusi Bersama**: Memahami kasus, mengidentifikasi aset, aktor, alur data, dan merumuskan asumsi teknis.
2. **Tahap 2 – Penyusunan DFD**: Anggota 1 membuat DFD awal, Anggota 2 & 3 memberikan masukan alur sistem dan *trust boundary*.
3. **Tahap 3 – Analisis STRIDE**: Setiap anggota mengerjakan ancaman sesuai pembagian tugas (skenario, dampak, skor risiko, mitigasi).
4. **Tahap 4 – Input Threat Dragon**: Semua anggota memasukkan ancaman ke elemen DFD yang relevan di OWASP Threat Dragon.
5. **Tahap 5 – Review & Pengumpulan**: Pemeriksaan konsistensi DFD, ancaman, skor, mitigasi, serta ekspor final ke format JSON dan PDF.

## Struktur Repositori

- `ThreatDragonModels/STRIDE - Kasus A - Kelompok 10/STRIDE - Kasus A - Kelompok 10.json`File model OWASP Threat Dragon v2.6.2 (7 elemen DFD, 3 zona *trust boundary*, 13 *data flow*, dan 11 ancaman STRIDE).
- `report/Laporan_Threat_Modeling_Kasus_A_Kelompok_10.pdf`Laporan hasil ekspor fitur Report OWASP Threat Dragon: diagram DFD, properti elemen, dan detail 11 ancaman STRIDE (ekspor ulang dari JSON final).
- `docs/Pembagian_Tugas.docx`Dokumen kerja kelompok: identitas & ringkasan Kasus A, pembagian tugas 3 anggota (S–T / R–I / D–E), panduan Tahap 0–5, referensi DFD & asumsi, rubrik risiko, dan checklist QA.
- `README.md`
  Dokumentasi utama repositori ini.

## Ringkasan 11 Ancaman STRIDE

|      No      | Kategori        | Elemen DFD                                    | Judul Ancaman                                                                        |     Skor Risiko     |
| :----------: | :-------------- | :-------------------------------------------- | :----------------------------------------------------------------------------------- | :------------------: |
| **1** | Spoofing        | `Mahasiswa` (Actor)                         | Pemalsuan Kehadiran Melalui Pembagian Kode QR Sesi Aktif                             |  **6** (High)  |
| **2** | Spoofing        | `Browser / Aplikasi Web` (Process)          | Penyamaran Akun Dosen Pengampu Melalui Pembajakan Token Sesi                         |  **6** (High)  |
| **3** | Tampering       | `ID sesi, token QR & token auth` (Flow)     | Manipulasi Parameter Identitas Sesi dan Token QR Saat Transit                        | **4** (Medium) |
| **4** | Repudiation     | `Backend Presensi` (Process)                | Penyangkalan Penutupan Sesi dan Status Kehadiran Akibat Ketiadaan Audit Log          | **4** (Medium) |
| **5** | Info Disclosure | `QR sesi, status hadir & data rekap` (Flow) | Penyadapan Data Rekap Kehadiran dan Identitas Mahasiswa pada Jaringan Publik         |  **6** (High)  |
| **6** | Info Disclosure | `Database Akademik` (Store)                 | Pembacaan Tidak Sah Data Akademik dan Riwayat Kehadiran pada Database                |  **6** (High)  |
| **7** | DoS             | `Backend Presensi` (Process)                | Pembanjiran Permintaan Validasi Presensi pada Jendela Waktu Sesi 5 Menit             |  **6** (High)  |
| **8** | EoP             | `Backend Presensi` (Process)                | Pengambilalihan Otorisasi Buka Sesi atau Rekap Seluruh Kelas (Broken Access Control) |  **6** (High)  |
| **9** | Tampering       | `Database Akademik` (Store)                 | Modifikasi Tidak Sah Catatan Kehadiran dan Status Sesi pada Database Akademik        | **3** (Medium) |
| **10** | DoS             | `Layanan Autentikasi` (Process)             | Gangguan Layanan Login Melalui Percobaan Masuk Massal (Brute-Force)                  | **4** (Medium) |
| **11** | Info Disclosure | `Kredensial akun kampus` (Flow)             | Penyadapan Kredensial Akun Kampus pada Alur Login di Jaringan Publik                 |  **6** (High)  |

## Cara Membuka & Mengedit di OWASP Threat Dragon

1. Buka [https://www.threatdragon.com/](https://www.threatdragon.com/) dan pilih **Login to GitHub**.
2. Pilih repositori `kaizone787/threat-modeling-kasus-a` dan branch `main`.
3. Buka model **`STRIDE - Kasus A - Kelompok 10`**.
4. Setiap perubahan yang disimpan lewat tombol **Save** akan otomatis ter-*commit* ke repositori ini.
5. Untuk mengekspor laporan PDF, buka menu **Report**, aktifkan seluruh opsi laporan, lalu pilih **Print → Save as PDF**.

## Ringkasan Distribusi Risiko

Skala risiko: Kemungkinan (1-3) × Dampak (1-3); skor 1-2 = Rendah, 3-4 = Sedang, 6-9 = Tinggi.

| Severity | Jumlah | Nomor Ancaman              |
| :------- | :----: | :------------------------- |
| High     |   7    | T01, T02, T05, T06, T07, T08, T11 |
| Medium   |   4    | T03, T04, T09, T10         |

## Daftar Asumsi Teknis

1. TLS/HTTPS serta pengamanan cookie/token pada komunikasi Browser dan layanan kampus belum dirinci.
2. QR di kelas statis selama 5 menit dan tanpa verifikasi lokasi fisik.
3. Audit log terstruktur (aksi sesi, validasi, akses rekap, perubahan data di tingkat database) belum dinyatakan tersedia.
4. Rate limiting pada endpoint validasi presensi dan endpoint login belum disebutkan.
5. Penegakan otorisasi di server, isolasi jaringan database, least privilege akun database, dan enkripsi data-at-rest belum dijelaskan.
