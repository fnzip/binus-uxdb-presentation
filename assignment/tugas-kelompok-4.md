# Tugas Kelompok 4 — UX for Digital Business
## Week 10 — Presentasi Prototype

**Kelompok:**
- Hendrik — 2702452625
- Surya Angga — 2702347553
- Alfian Oktafireza Syahputra — 2702345333
- Poppy Citramelati — 2702348404
- Esther Gracieline Fechael — 2702343113

---

## 1. Konsep Desain Aplikasi

### Masalah yang Ditemukan

Berdasarkan observasi di lingkungan kantor dan masyarakat, khususnya pada kebiasaan belanja online mahasiswa dan pekerja muda usia 18-35 tahun, ditemukan beberapa permasalahan utama:

1. **Pencarian produk tidak akurat** — Pengguna harus scroll berjam-jam untuk menemukan produk yang diinginkan. Filter pencarian kurang presisi, terutama untuk spesifikasi teknis (contoh: "baterai >10.000mAh").

2. **Maraknya seller penipu & ulasan palsu** — Tidak ada sistem otomatis yang memverifikasi keaslian ulasan. Pengguna sering menerima produk yang tidak sesuai deskripsi.

3. **UI overload iklan dan promosi** — Beranda dipenuhi banner, pop-up, dan notifikasi promosi yang membebani kognitif pengguna dan mengalihkan dari tujuan utama belanja.

4. **Loading lambat di koneksi lemah** — Aplikasi berat, tidak optimal untuk pengguna di daerah dengan koneksi 4G lemah.

5. **Tidak ada jaminan belanja aman yang transparan** — Proses refund masih panjang dan membingungkan.

### Konsep Aplikasi: ShopSync — Belanja Pintar

ShopSync adalah fitur AI-powered yang ditambahkan ke dalam ekosistem Shopee untuk memberikan pengalaman belanja yang pintar, cepat, dan terpercaya. Fitur ini menjadikan Shopee sebagai e-commerce pertama di Indonesia dengan jaminan belanja aman 100%.

### User Requirements

#### Functional Requirements

| ID | Peran User | Tujuan / Fitur | Requirement |
|----|-----------|----------------|-------------|
| FR-01 | Pembeli | Rekomendasi AI Personal | Pembeli dapat melihat daftar produk relevan otomatis berdasarkan riwayat belanja dengan AI |
| FR-02 | Pembeli | Smart Search AI | Pembeli dapat mencari produk dengan natural language dan mendapat hasil akurat terfilter otomatis |
| FR-03 | Pembeli | Keranjang Belanja | Pembeli dapat tambah/hapus produk, lihat subtotal, dan checkout kapan saja |
| FR-04 | Pembeli | Pembayaran Aman | Pembeli dapat checkout dengan multi-metode (e-wallet, transfer, COD, paylater) dengan konfirmasi instan |
| FR-05 | Pembeli | Tracking Live | Pembeli dapat melihat status pesanan real-time dengan peta kurir dan ETA |
| FR-06 | Pembeli | AI Trust Score | Pembeli dapat melihat skor kepercayaan seller/produk (0-100) berbasis AI |
| FR-07 | Pembeli | Verified Reviews | Pembeli hanya melihat ulasan dari pembeli terverifikasi (badge centang biru) |
| FR-08 | Penjual | Upload Produk Verified | Penjual dapat upload foto/video 360° dengan verifikasi AI otomatis |
| FR-09 | Admin | Moderasi | Admin dapat approve ulasan, blokir seller bermasalah |

#### Non-Functional Requirements

| Jenis NFR | Deskripsi |
|-----------|-----------|
| Look and Feel | Mobile-first, homepage clean tanpa iklan overload, warna Shopee minimalis (orange) |
| Performance | Loading halaman < 3 detik, AI search response < 1 detik, handle 10.000 user simultan |
| Security | Enkripsi AES-256, autentikasi 2FA, deteksi penipu AI, compliance UU PDP 2022 |
| Usability | Bahasa Indonesia, tutorial onboarding singkat, aksesibel untuk koneksi lemah |
| Compliance | UU PDP 2022, PCI-DSS, transparansi harga asli, refund policy < 48 jam |

### Persona

| Atribut | Detail |
|---------|--------|
| **Nama** | Surya Angga |
| **Usia** | 30 tahun |
| **Jenis Kelamin** | Laki-laki |
| **Pekerjaan** | Karyawan Swasta |
| **Lokasi** | Jakarta, Indonesia |
| **Background** | Karyawan sibuk jadwal 9-5, sering belanja online gadget & baju kerja, gunakan Shopee 2-3 kali seminggu |
| **Goals** | Temukan produk cepat, seller terpercaya, checkout lancar |
| **Pain Points** | Pencarian tidak presisi, ulasan palsu, loading lambat, notifikasi bombardir |
| **Tech Savvy** | Tinggi — Android, ShopeePay, Google Assistant |

### Fitur yang Dibutuhkan

1. **AI Smart Search** — Pencarian natural language dengan auto-filter presisi
2. **AI Trust Score** — Skor kepercayaan 0-100 untuk setiap seller/produk
3. **Verified Reviews** — Ulasan hanya dari pembeli terverifikasi + foto/video real
4. **Personal Shopper AI** — Rekomendasi otomatis berdasarkan preferensi
5. **Express Checkout** — 3-step checkout dengan jaminan 100% uang kembali
6. **Tracking Live** — Peta real-time kurir + ETA akurat
7. **Clean UI** — Antarmuka minimalis tanpa iklan berlebih

---

## 2. Sketsa

Sketsa desain aplikasi dibuat menggunakan diagram Mermaid yang merepresentasikan:

1. **User Flow Diagram** — Alur navigasi utama dari login hingga tracking pesanan
2. **Sitemap** — Arsitektur informasi seluruh halaman aplikasi
3. **Wireframe Home** — Layout halaman utama (mobile)
4. **Wireframe Detail Produk** — Layout halaman detail dengan AI Trust Score
5. **Wireframe Keranjang** — Layout checkout express
6. **Wireframe Tracking** — Layout tracking live pesanan
7. **Sequence Diagram** — Alur interaksi user-system pada scenario "Belanja Charger Malam Hari"

> Sketsa lengkap tersedia di file `pres-2/sketsa-mermaid.md`

---

## 3. Prototype

Prototype dibangun menggunakan tech stack:
- **Nuxt 4** — Framework Vue.js untuk SSR/SSG
- **Nuxt UI** — Component library dengan design system
- **Tailwind CSS 4** — Utility-first CSS framework
- **Lucide Icons** — Icon library modern

### Halaman Prototype:

| Halaman | Fungsi | File |
|---------|--------|------|
| Home / Dashboard | Rekomendasi AI, Flash Sale, Quick Actions | `proto-2/app/pages/index.vue` |
| Pencarian | AI Smart Search + Filter Pintar | `proto-2/app/pages/pencarian.vue` |
| Detail Produk | AI Trust Score, Video 360°, Ulasan Verified | `proto-2/app/pages/produk.vue` |
| Keranjang | Checkout Express 3-step | `proto-2/app/pages/keranjang.vue` |
| Pesanan | Tracking Live + Status | `proto-2/app/pages/pesanan.vue` |
| Profil | Data diri, preferensi AI | `proto-2/app/pages/profil.vue` |

### Cara Menjalankan:
```bash
cd proto-2
pnpm install
pnpm dev
```

> Prototype tersedia di folder `proto-2/`

---

## Referensi

- Garrett, J. J. (2011). *The Elements of User Experience*. New Riders.
- Norman, D. (2013). *The Design of Everyday Things*. Basic Books.
- Krug, S. (2014). *Don't Make Me Think, Revisited*. New Riders.
- UU PDP No. 27 Tahun 2022 tentang Pelindungan Data Pribadi.
- OWASP Top 10 (2021). Web Application Security Risks.

---

*UX for Digital Business — BINUS Online Learning 2026*
