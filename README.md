# Threat Modeling STRIDE — Kasus A (Kelompok 10)

Repositori ini berisi model *threat modeling* berbasis **STRIDE** menggunakan **OWASP Threat Dragon** untuk mata kuliah **Keamanan Siber (CAK3CAB3)** — **Kelompok 10**, Studi Kasus A (*Sistem Presensi Perkuliahan Berbasis QR Code*), dosen pengampu **Kharisma Monika Dian Pertiwi**.

## Anggota Kelompok & Pembagian Tugas

| Peran               | Nama                     | NIM              | Fokus Utama & Tanggung Jawab                                                                                                                     |
| :------------------ | :----------------------- | :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Anggota 1** | Muhammad Chaesar Pratama | `103072400119` | **DFD & Threat Analysis (S, T)**: Identifikasi aset/aktor, penyusunan DFD, trust boundary, serta analisis ancaman T01, T02, T03.           |
| **Anggota 2** | Hendra Dirga Dwi Saputra | `103072430018` | **Authentication & Data Security (R, I)**: Analisis alur autentikasi, integrasi Threat Dragon, serta analisis ancaman T04, T05, T06, T07.  |
| **Anggota 3** | Laura Chyndearni Saragih | `103072400049` | **Validation & Admin Security (D, E)**: Analisis validasi backend, kalibrasi risiko, QA, ekspor PDF, serta analisis ancaman T08, T09, T10. |

## Pembagian Beban Kerja

| Pekerjaan                            |   Anggota 1   | Anggota 2 | Anggota 3 |
| :----------------------------------- | :-----------: | :-------: | :-------: |
| Identifikasi aset, aktor, dan asumsi |      ✓      |    ✓    |    ✓    |
| Penyusunan DFD & Trust Boundary      | ✓ *(Lead)* |  Review  |  Review  |
| Analisis STRIDE & Risk Assessment    |   3 Ancaman   | 4 Ancaman | 3 Ancaman |
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

- `ThreatDragonModels/STRIDE - Kasus A - Kelompok 10/STRIDE - Kasus A - Kelompok 10.json`File model OWASP Threat Dragon v2.6.2 (7 elemen DFD, 3 zona *trust boundary*, 13 *data flow*, dan 10 ancaman STRIDE).
- `docs/Laporan_Threat_Modeling_Kasus_A_Kelompok_10.pdf`Laporan hasil ekspor fitur Report OWASP Threat Dragon: diagram DFD, properti elemen, dan detail 10 ancaman STRIDE (11 halaman).
- `docs/Pembagian_Tugas.docx`Dokumen kerja kelompok: identitas & ringkasan Kasus A, pembagian tugas detail 3 anggota (S–T / R–I / D–E), panduan pengerjaan Tahap 0–5, referensi 7 elemen DFD & trust boundary, contoh asumsi teknis, rubrik risiko (K×D skala 1–3), dan checklist QA 7 item sebelum pengumpulan.
- `README.md`
  Dokumentasi utama repositori ini.

## Ringkasan 10 Ancaman STRIDE

|      No      | Kategori        | Elemen DFD                                    | Judul Ancaman                                                                        |     Skor Risiko     |
| :----------: | :-------------- | :-------------------------------------------- | :----------------------------------------------------------------------------------- | :------------------: |
| **1** | Spoofing        | `Mahasiswa` (Actor)                         | Pemalsuan Kehadiran Melalui Pembagian Kode QR Sesi Aktif                             |  **6** (High)  |
| **2** | Spoofing        | `Layanan Autentikasi` (Process)             | Penyamaran Akun Dosen Pengampu Melalui Pembajakan Token Sesi                         |  **6** (High)  |
| **3** | Tampering       | `ID sesi, token QR & token auth` (Flow)     | Manipulasi Parameter Identitas Sesi dan Token QR Saat Transit                        | **4** (Medium) |
| **4** | Repudiation     | `Backend Presensi` (Process)                | Penyangkalan Penutupan Sesi dan Status Kehadiran Akibat Ketiadaan Audit Log          | **4** (Medium) |
| **5** | Info Disclosure | `QR sesi, status hadir & data rekap` (Flow) | Penyadapan Data Rekap Kehadiran dan Identitas Mahasiswa pada Jaringan Publik         |  **6** (High)  |
| **6** | Info Disclosure | `Database Akademik` (Store)                 | Pembacaan Tidak Sah Data Akademik dan Riwayat Kehadiran pada Database                | **3** (Medium) |
| **7** | DoS             | `Backend Presensi` (Process)                | Pembanjiran Permintaan Validasi Presensi pada Jendela Waktu Sesi 5 Menit             |  **6** (High)  |
| **8** | EoP             | `Backend Presensi` (Process)                | Pengambilalihan Otorisasi Buka Sesi atau Rekap Seluruh Kelas (Broken Access Control) |  **6** (High)  |
| **9** | Tampering       | `Database Akademik` (Store)                 | Modifikasi Tidak Sah Catatan Kehadiran dan Status Sesi pada Database Akademik        | **3** (Medium) |
| **10** | DoS             | `Layanan Autentikasi` (Process)             | Gangguan Layanan Login Melalui Percobaan Masuk Massal (Brute-Force)                  | **4** (Medium) |

## Cara Membuka & Mengedit di OWASP Threat Dragon

1. Buka [https://www.threatdragon.com/](https://www.threatdragon.com/) dan pilih **Login to GitHub**.
2. Pilih repositori `kaizone787/threat-modeling-kasus-a` dan branch `main`.
3. Buka model **`STRIDE - Kasus A - Kelompok 10`**.
4. Setiap perubahan yang disimpan lewat tombol **Save** akan otomatis ter-*commit* ke repositori ini.
5. Untuk mengekspor laporan PDF, buka menu **Report**, aktifkan seluruh opsi laporan, lalu pilih **Print → Save as PDF**.
