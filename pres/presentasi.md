# EcoLink Community
## Platform Kolaboratif Manajemen Sampah Komunitas

---

## 1. Latar Belakang Masalah

Indonesia menghasilkan **67,8 juta ton sampah per tahun** (SIPSN 2023), dan hanya sekitar **37%** yang terkelola dengan baik. Di tingkat rumah tangga, permasalahan utama meliputi:

- **Pencampuran sampah** organik dan anorganik dalam satu wadah
- **Ketidakjelasan jadwal** pengangkutan sampah oleh petugas
- **Minimnya edukasi** tentang pemilahan sampah yang benar
- **Tidak ada insentif** bagi warga untuk memilah sampah
- **Komunikasi searah** antara pengelola sampah dan warga

Dampaknya: penumpukan sampah menjadi sarang penyakit (demam berdarah, diare), pencemaran tanah & air, serta menurunkan estetika lingkungan.

---

## 2. Solusi: EcoLink Community

Aplikasi platform kolaboratif yang menghubungkan **warga**, **pengelola sampah (TPS/Bank Sampah)**, dan **pengumpul/pengangkut sampah** untuk mendigitalisasi manajemen sampah di tingkat komunitas (RT/RW/Perumahan).

### Visi
> Mewujudkan komunitas zero-waste melalui teknologi yang memberdayakan setiap warga.

### Value Proposition
| Untuk | Nilai |
|-------|-------|
| Warga | Kemudahan, edukasi, dan insentif finansial |
| Pengelola | Transparansi data, efisiensi operasional |
| Lingkungan | Pengurangan sampah yang masuk TPA |

---

## 3. Persona Pengguna

### Persona 1: Budi (35 tahun) — Warga Perumahan
- **Pekerjaan:** Karyawan swasta
- **Konteks:** Sibuk bekerja, sering lupa jadwal angkut sampah
- **Frustasi:** Tidak tahu cara memilah sampah dengan benar, sampah sering menumpuk di depan rumah
- **Kebutuhan:** Pengingat otomatis, panduan simpel pemilahan
- **Motivasi:** Lingkungan bersih, tidak dikenai denda RT

### Persona 2: Ibu Ani (45 tahun) — Ibu Rumah Tangga
- **Pekerjaan:** Ibu rumah tangga
- **Konteks:** Punya waktu luang, ingin lingkungan bersih
- **Frustasi:** Ingin menyetor sampah terpilah tapi tidak tahu ke mana dan kapan
- **Kebutuhan:** Informasi lokasi Bank Sampah, jadwal setor, dan reward
- **Motivasi:** Penghasilan tambahan dari sampah daur ulang

### Persona 3: Pak RT / Pengelola Sampah
- **Pekerjaan:** Ketua RT / Pengelola TPS
- **Konteks:** Bertanggung jawab atas kebersihan lingkungan
- **Frustasi:** Sulit mendata partisipasi warga, jadwal penjemputan sering berubah, iuran tidak transparan
- **Kebutuhan:** Dashboard pengelolaan, laporan otomatis, komunikasi massal
- **Motivasi:** Efisiensi kerja, lingkungan tertib

### Persona 4: Mas Joko (28 tahun) — Pengumpul Sampah
- **Pekerjaan:** Driver pengangkut sampah
- **Konteks:** Perlu rute efisien dan jadwal jelas
- **Frustasi:** Warga sering tidak siap saat jadwal angkut, sampah tercampur
- **Kebutuhan:** Navigasi rute, notifikasi kesiapan warga
- **Motivasi:** Efisiensi waktu dan pendapatan

---

## 4. User Requirements

### Functional Requirements
| ID | Kebutuhan | Prioritas |
|----|-----------|-----------|
| FR-01 | Sistem notifikasi jadwal penjemputan sampah | Tinggi |
| FR-02 | Panduan edukasi pemilahan sampah (visual + chatbot) | Tinggi |
| FR-03 | Sistem poin reward untuk setoran sampah terpilah | Tinggi |
| FR-04 | Dashboard pelacakan status sampah | Sedang |
| FR-05 | Fitur laporan sampah liar dengan foto & GPS | Sedang |
| FR-06 | Komunikasi langsung warga ↔ pengelola | Sedang |
| FR-07 | Manajemen iuran kebersihan digital | Rendah |
| FR-08 | Rute optimasi untuk pengangkut sampah | Rendah |

### Non-Functional Requirements
| ID | Kebutuhan | Detail |
|----|-----------|--------|
| NFR-01 | Performa | Halaman load < 3 detik |
| NFR-02 | Usability | Dapat digunakan usia 15-65 tahun |
| NFR-03 | Aksesibilitas | Kontras warna WCAG AA, font minimal 14sp |
| NFR-04 | Platform | Progressive Web App (PWA) — Android & iOS |
| NFR-05 | Bahasa | Bahasa Indonesia sebagai default |

---

## 5. Fitur Utama

### 5.1 Jadwal & Notifikasi
- Kalender jadwal penjemputan per zona/RT
- Push notification H-1 dan H-hari
- Status real-time petugas (sedang menuju / selesai)
- Reschedule request oleh warga

### 5.2 Edukasi Pemilahan
- Panduan visual bergambar per kategori sampah
- Scan sampah via kamera (AI-powered identification)
- Quiz harian dengan reward poin
- Tips pengolahan sampah organik (kompos)

### 5.3 Pelacakan Sampah (Track & Trace)
- Status setoran: Dikumpulkan → Dijemput → Dipilah → Didaur Ulang
- Riwayat setoran bulanan per warga
- Statistik dampak lingkungan personal (CO₂ tersimpan, pohon diselamatkan)

### 5.4 Saku Digital (EcoPoin)
- Poin per kg sampah terpilah yang disetor
- Konversi poin → saldo e-wallet (GoPay, OVO, Dana)
- Diskon iuran kebersihan
- Leaderboard komunitas bulanan

### 5.5 Laporan Komunitas
- Foto + pin lokasi penumpukan sampah liar
- Voting prioritas pembersihan oleh warga lain
- Status penanganan oleh pengelola (real-time)
- Riwayat laporan terselesaikan

### 5.6 Komunikasi & Pengumuman
- Chat group komunitas (per RT/RW)
- Broadcast pengumuman dari pengelola
- Fitur voting untuk keputusan komunitas

---

## 6. Information Architecture

```
EcoLink Community
├── Home (Dashboard)
│   ├── Ringkasan Poin
│   ├── Jadwal Terdekat
│   ├── Tips Hari Ini
│   └── Quick Actions
├── Jadwal
│   ├── Kalender Bulanan
│   ├── Detail Jadwal
│   └── Request Reschedule
├── Edukasi
│   ├── Panduan Pemilahan
│   ├── Scan Sampah
│   └── Quiz & Tips
├── Setor Sampah
│   ├── Catat Setoran
│   ├── Riwayat
│   └── Statistik Dampak
├── Laporan
│   ├── Buat Laporan
│   ├── Laporan Saya
│   └── Laporan Komunitas
├── Saku Digital
│   ├── Saldo Poin
│   ├── Riwayat Transaksi
│   └── Tukar Poin
└── Profil
    ├── Data Diri
    ├── Pengaturan Notifikasi
    └── Bantuan
```

---

## 7. User Flow

### Flow Utama: Setor Sampah & Dapat Poin

1. Warga memilah sampah di rumah
2. Buka app → cek jadwal penjemputan
3. Konfirmasi kesiapan setor
4. Petugas menjemput & menimbang sampah
5. Petugas input data setoran di app
6. Sistem otomatis hitung & tambahkan poin
7. Warga terima notifikasi poin masuk
8. Warga tukar poin → saldo e-wallet

---

## 8. Design Principles

1. **Simplicity First** — Interface minimalis, satu aksi utama per layar
2. **Gamification** — Poin, badge, leaderboard untuk engagement
3. **Trust & Transparency** — Status real-time, riwayat lengkap
4. **Inclusive** — Aksesibel untuk semua usia dan tingkat literasi digital
5. **Local Context** — Bahasa Indonesia, ikon familiar, warna alam (hijau)

---

## 9. Tech Stack (Prototype)

| Layer | Teknologi |
|-------|-----------|
| Frontend | Nuxt 4 + Nuxt UI + Tailwind CSS 4 |
| Icons | Lucide Icons |
| Deployment | Vercel / Netlify (SSG) |
| Design System | Nuxt UI Color System (Primary: Green) |

---

## 10. Competitive Analysis

| Fitur | EcoLink | Octopus (SG) | Waste4Change | Mallsampah |
|-------|---------|--------------|--------------|------------|
| Jadwal Sampah | ✅ | ✅ | ❌ | ❌ |
| Edukasi Pemilahan | ✅ | ❌ | ✅ | ❌ |
| Reward Poin | ✅ | ✅ | ❌ | ✅ |
| Laporan Sampah Liar | ✅ | ❌ | ❌ | ❌ |
| Komunitas Chat | ✅ | ❌ | ❌ | ❌ |
| Pelacakan Real-time | ✅ | ✅ | ✅ | ❌ |

---

## 11. Business Model

- **Freemium:** Fitur dasar gratis, fitur premium (analytics lanjutan) untuk pengelola
- **Partnership:** Kerjasama dengan e-wallet untuk konversi poin
- **CSR Funding:** Pendanaan dari program CSR perusahaan
- **Data Insights:** Insight anonim untuk pemerintah daerah (perencanaan kebijakan)

---

## 12. Roadmap

| Fase | Timeline | Deliverable |
|------|----------|-------------|
| MVP | Bulan 1-3 | Jadwal, Edukasi, Setor Sampah, Poin |
| V1.0 | Bulan 4-6 | Laporan Komunitas, Chat, Leaderboard |
| V2.0 | Bulan 7-12 | AI Scan, Rute Optimasi, Partnership e-wallet |

---

*Dibuat untuk mata kuliah UX Database — BINUS University, 2026*
