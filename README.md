# Threat Modeling STRIDE — Studi Kasus A: Sistem Presensi Perkuliahan Berbasis QR Code

Repositori ini berisi model *threat modeling* berbasis **STRIDE** menggunakan **OWASP Threat Dragon** untuk mata kuliah **Keamanan Siber (CAK3CAB3)** — Studi Kasus A (*Sistem Presensi Perkuliahan Berbasis QR Code*).

## Anggota Kelompok

| Peran | Nama | NIM | Fokus Utama |
| :--- | :--- | :--- | :--- |
| **Anggota 1** | Muhammad Chaesar Pratama | `103072400119` | Lingkup, Asumsi, Pembuatan DFD & STRIDE (S, T) |
| **Anggota 2** | Hendra Dirga Dwi Saputra | `103072430018` | STRIDE (R, I) & Integrasi OWASP Threat Dragon |
| **Anggota 3** | Laura Chyndearni Saragih | `103072400049` | STRIDE (D, E), Kalibrasi Risiko, QA & Ekspor PDF |

## Struktur Repositori

- `ThreatDragonModels/STRIDE - Kasus A - Sistem Presensi QR Code/STRIDE - Kasus A - Sistem Presensi QR Code.json` — File model OWASP Threat Dragon v2 (7 elemen DFD, 3 zona *trust boundary*, 13 *data flow*, dan 8 ancaman STRIDE).
- `docs/Pembagian_Tugas_Kasus_A_Final.docx` — Dokumen pembagian tugas kelompok, panduan langkah pengerjaan, standar STRIDE, dan *checklist* QA.

## Ringkasan 8 Ancaman STRIDE

| No | Kategori | Elemen DFD | Judul Ancaman | Skor Risiko |
| :-: | :--- | :--- | :--- | :---: |
| 1 | Spoofing | `Mahasiswa` (Actor) | Pemalsuan Kehadiran Melalui Pembagian Kode QR Sesi Aktif | 6 (High) |
| 2 | Spoofing | `Layanan Autentikasi Kampus` (Process) | Penyamaran Akun Dosen Pengampu Melalui Pembajakan Token Sesi | 6 (High) |
| 3 | Tampering | `ID sesi, token QR & token auth` (Flow) | Manipulasi Parameter Identitas Sesi dan Token QR Saat Transit | 4 (Medium) |
| 4 | Repudiation | `Backend Presensi` (Process) | Penyangkalan Penutupan Sesi dan Status Kehadiran Akibat Ketiadaan Audit Log | 4 (Medium) |
| 5 | Information disclosure | `QR sesi, status hadir & data rekap` (Flow) | Penyadapan Data Rekap Kehadiran dan Identitas Mahasiswa pada Jaringan Publik | 6 (High) |
| 6 | Information disclosure | `Database Akademik` (Store) | Pembacaan Tidak Sah Data Akademik dan Riwayat Kehadiran pada Database Akademik | 3 (Medium) |
| 7 | Denial of service | `Backend Presensi` (Process) | Pembanjiran Permintaan Validasi Presensi pada Jendela Waktu Sesi 5 Menit | 6 (High) |
| 8 | Elevation of privilege | `Backend Presensi` (Process) | Pengambilalihan Otorisasi Buka Sesi atau Rekap Seluruh Kelas (Broken Access Control) | 6 (High) |

## Cara Membuka & Mengedit di OWASP Threat Dragon

1. Buka [https://www.threatdragon.com/](https://www.threatdragon.com/) dan pilih **Login to GitHub**.
2. Pilih repositori `kaizone787/threat-modeling-kasus-a` dan branch `main`.
3. Buka model **`STRIDE - Kasus A - Sistem Presensi QR Code`**.
4. Setiap perubahan yang disimpan lewat tombol **Save** akan otomatis ter-*commit* ke repositori ini.
5. Untuk mengekspor laporan PDF, buka menu **Report**, aktifkan seluruh opsi laporan, lalu pilih **Print → Save as PDF**.
