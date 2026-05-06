# Sketsa Aplikasi EcoLink Community
## Mermaid Diagrams

---

## 1. User Flow Diagram — Alur Utama Aplikasi

```mermaid
flowchart TD
    A[Buka Aplikasi] --> B{Sudah Login?}
    B -->|Tidak| C[Halaman Login/Register]
    C --> D[Isi Data Diri & Alamat]
    D --> E[Verifikasi OTP]
    E --> F[Dashboard Home]
    B -->|Ya| F

    F --> G[Jadwal Sampah]
    F --> H[Edukasi Pemilahan]
    F --> I[Setor Sampah]
    F --> J[Laporan Komunitas]
    F --> K[Saku Digital / Poin]

    G --> G1[Lihat Kalender]
    G --> G2[Terima Notifikasi]
    G --> G3[Konfirmasi Kesiapan]

    H --> H1[Panduan Visual]
    H --> H2[Scan Sampah AI]
    H --> H3[Quiz Harian]

    I --> I1[Catat Setoran]
    I1 --> I2[Petugas Jemput & Timbang]
    I2 --> I3[Poin Otomatis Masuk]

    J --> J1[Ambil Foto]
    J1 --> J2[Pin Lokasi GPS]
    J2 --> J3[Kirim Laporan]
    J3 --> J4[Voting Prioritas]

    K --> K1[Cek Saldo Poin]
    K --> K2[Tukar ke E-Wallet]
    K --> K3[Lihat Leaderboard]
```

---

## 2. Sitemap / Information Architecture

```mermaid
graph TD
    ROOT[EcoLink Community] --> HOME[Home / Dashboard]
    ROOT --> JADWAL[Jadwal]
    ROOT --> EDUKASI[Edukasi]
    ROOT --> SETOR[Setor Sampah]
    ROOT --> LAPORAN[Laporan]
    ROOT --> POIN[Saku Digital]
    ROOT --> PROFIL[Profil]

    HOME --> HOME1[Ringkasan Poin]
    HOME --> HOME2[Jadwal Terdekat]
    HOME --> HOME3[Tips Hari Ini]
    HOME --> HOME4[Quick Actions]

    JADWAL --> J1[Kalender Bulanan]
    JADWAL --> J2[Detail Jadwal]
    JADWAL --> J3[Request Reschedule]

    EDUKASI --> E1[Panduan Pemilahan]
    EDUKASI --> E2[Scan Sampah]
    EDUKASI --> E3[Quiz & Tips]

    SETOR --> S1[Catat Setoran Baru]
    SETOR --> S2[Riwayat Setoran]
    SETOR --> S3[Statistik Dampak]

    LAPORAN --> L1[Buat Laporan Baru]
    LAPORAN --> L2[Laporan Saya]
    LAPORAN --> L3[Laporan Komunitas]

    POIN --> P1[Saldo & Riwayat]
    POIN --> P2[Tukar Poin]
    POIN --> P3[Leaderboard]

    PROFIL --> PR1[Data Diri]
    PROFIL --> PR2[Pengaturan]
    PROFIL --> PR3[Bantuan]
```

---

## 3. Wireframe — Halaman Dashboard (Mobile)

```mermaid
block-beta
    columns 1
    block:HEADER
        columns 3
        A["☰ Menu"] B["EcoLink Community"] C["🔔"]
    end
    space
    block:GREETING
        columns 1
        D["Halo, Budi! 👋"]
        E["EcoPoin: 1.250 pts"]
    end
    space
    block:SCHEDULE
        columns 1
        F["📅 Jadwal Berikutnya"]
        G["Rabu, 7 Mei 2026 — 07:00"]
        H["Status: Terjadwal ✅"]
    end
    space
    block:QUICKACTIONS
        columns 4
        I["📅 Jadwal"]
        J["📖 Edukasi"]
        K["♻️ Setor"]
        L["📢 Laporan"]
    end
    space
    block:TIPS
        columns 1
        M["💡 Tips Hari Ini"]
        N["Kulit pisang bisa jadi kompos dalam 2 minggu!"]
    end
    space
    block:NAVBAR
        columns 5
        O["🏠"] P["📅"] Q["♻️"] R["🏆"] S["👤"]
    end
```

---

## 4. Wireframe — Halaman Jadwal

```mermaid
block-beta
    columns 1
    block:HEADER2
        columns 3
        A2["← Back"] B2["Jadwal Sampah"] C2["🔔"]
    end
    space
    block:CALENDAR
        columns 7
        D2["Sen"] E2["Sel"] F2["Rab"] G2["Kam"] H2["Jum"] I2["Sab"] J2["Min"]
        K2["5"] L2["6"] M2["7 🟢"] N2["8"] O2["9"] P2["10 🟢"] Q2["11"]
    end
    space
    block:DETAIL
        columns 1
        R2["📋 Detail Jadwal"]
        S2["Rabu, 7 Mei — Sampah Organik"]
        T2["Sabtu, 10 Mei — Sampah Anorganik"]
    end
    space
    block:ACTION2
        columns 1
        U2["[✅ Konfirmasi Siap Setor]"]
    end
    space
    block:NAVBAR2
        columns 5
        V2["🏠"] W2["📅"] X2["♻️"] Y2["🏆"] Z2["👤"]
    end
```

---

## 5. Wireframe — Halaman Edukasi Pemilahan

```mermaid
block-beta
    columns 1
    block:HEADER3
        columns 3
        A3["← Back"] B3["Edukasi"] C3["🔍"]
    end
    space
    block:CATEGORIES
        columns 3
        D3["🟢 Organik"]
        E3["🔵 Anorganik"]
        F3["🔴 B3"]
    end
    space
    block:CONTENT3
        columns 1
        G3["🟢 Sampah Organik"]
        H3["Sisa makanan, daun, kulit buah"]
        I3["Bisa dijadikan kompos"]
    end
    space
    block:SCAN
        columns 1
        J3["📷 Scan Sampah"]
        K3["Arahkan kamera ke sampah untuk identifikasi otomatis"]
    end
    space
    block:QUIZ
        columns 1
        L3["🎯 Quiz Hari Ini"]
        M3["Jawab 5 soal, dapatkan 10 poin!"]
    end
    space
    block:NAVBAR3
        columns 5
        N3["🏠"] O3["📅"] P3["♻️"] Q3["🏆"] R3["👤"]
    end
```

---

## 6. Wireframe — Halaman Setor Sampah

```mermaid
block-beta
    columns 1
    block:HEADER4
        columns 3
        A4["← Back"] B4["Setor Sampah"] C4["📊"]
    end
    space
    block:STATS
        columns 3
        D4["Total: 25kg"] E4["Bulan ini: 8kg"] F4["Poin: 1.250"]
    end
    space
    block:NEWSETOR
        columns 1
        G4["➕ Catat Setoran Baru"]
        H4["Jenis: [Organik ▼]"]
        I4["Berat: [___] kg"]
        J4["Foto: [📷 Ambil Foto]"]
    end
    space
    block:HISTORY
        columns 1
        K4["📜 Riwayat Setoran"]
        L4["3 Mei — Plastik 2kg — +50 poin"]
        M4["1 Mei — Organik 3kg — +30 poin"]
    end
    space
    block:NAVBAR4
        columns 5
        N4["🏠"] O4["📅"] P4["♻️"] Q4["🏆"] R4["👤"]
    end
```

---

## 7. Wireframe — Halaman Saku Digital (Poin)

```mermaid
block-beta
    columns 1
    block:HEADER5
        columns 3
        A5["← Back"] B5["Saku Digital"] C5["ℹ️"]
    end
    space
    block:BALANCE
        columns 1
        D5["💰 Saldo EcoPoin"]
        E5["1.250 Poin"]
        F5["≈ Rp 12.500"]
    end
    space
    block:ACTIONS5
        columns 2
        G5["🔄 Tukar Poin"] H5["📊 Riwayat"]
    end
    space
    block:LEADERBOARD
        columns 1
        I5["🏆 Leaderboard RT 05"]
        J5["1. Ibu Ani — 3.200 pts"]
        K5["2. Budi — 1.250 pts"]
        L5["3. Pak Darto — 980 pts"]
    end
    space
    block:REDEEM
        columns 1
        M5["Tukar ke:"]
        N5["[GoPay] [OVO] [Dana]"]
    end
    space
    block:NAVBAR5
        columns 5
        O5["🏠"] P5["📅"] Q5["♻️"] R5["🏆"] S5["👤"]
    end
```

---

## 8. Wireframe — Halaman Laporan Komunitas

```mermaid
block-beta
    columns 1
    block:HEADER6
        columns 3
        A6["← Back"] B6["Laporan"] C6["➕"]
    end
    space
    block:FILTER
        columns 3
        D6["Semua"] E6["Menunggu"] F6["Selesai"]
    end
    space
    block:REPORT1
        columns 1
        G6["📍 Jl. Melati No.5"]
        H6["Tumpukan sampah dekat selokan"]
        I6["⬆️ 12 votes | Status: Diproses"]
    end
    space
    block:REPORT2
        columns 1
        J6["📍 Taman RT 03"]
        K6["Sampah plastik berserakan"]
        L6["⬆️ 8 votes | Status: Menunggu"]
    end
    space
    block:FABBUTTON
        columns 1
        M6["[📷 + Buat Laporan Baru]"]
    end
    space
    block:NAVBAR6
        columns 5
        N6["🏠"] O6["📅"] P6["♻️"] Q6["🏆"] R6["👤"]
    end
```

---

## 9. Sequence Diagram — Proses Setor Sampah

```mermaid
sequenceDiagram
    participant W as Warga
    participant App as EcoLink App
    participant P as Petugas
    participant S as Server
    participant EW as E-Wallet

    W->>App: Pilah sampah & catat jenis
    App->>S: Simpan data setoran (pending)
    W->>App: Konfirmasi siap dijemput
    App->>P: Notifikasi: Warga siap setor
    P->>W: Jemput & timbang sampah
    P->>App: Input berat aktual
    App->>S: Update setoran + hitung poin
    S->>App: Poin berhasil ditambahkan
    App->>W: Notifikasi: +50 poin diterima!
    W->>App: Tukar poin
    App->>S: Request redemption
    S->>EW: Transfer saldo
    EW->>W: Saldo masuk
```

---

## 10. State Diagram — Status Laporan Sampah

```mermaid
stateDiagram-v2
    [*] --> Dilaporkan
    Dilaporkan --> Diverifikasi: Admin review
    Diverifikasi --> Dijadwalkan: Assign petugas
    Dijadwalkan --> Diproses: Petugas berangkat
    Diproses --> Selesai: Foto bukti selesai
    Selesai --> [*]

    Dilaporkan --> Ditolak: Laporan tidak valid
    Ditolak --> [*]
```

---

## 11. Entity Relationship Diagram

```mermaid
erDiagram
    WARGA {
        int id PK
        string nama
        string alamat
        string telepon
        string rt_rw
        int total_poin
    }
    SETORAN {
        int id PK
        int warga_id FK
        string jenis_sampah
        float berat_kg
        int poin_diperoleh
        datetime tanggal
        string status
    }
    JADWAL {
        int id PK
        string zona
        string jenis_sampah
        date tanggal
        time waktu
        string status
    }
    LAPORAN {
        int id PK
        int warga_id FK
        string lokasi
        string deskripsi
        string foto_url
        int votes
        string status
    }
    POIN_TRANSAKSI {
        int id PK
        int warga_id FK
        int jumlah
        string tipe
        string keterangan
        datetime tanggal
    }
    PETUGAS {
        int id PK
        string nama
        string zona_tugas
        string telepon
    }

    WARGA ||--o{ SETORAN : "menyetor"
    WARGA ||--o{ LAPORAN : "melaporkan"
    WARGA ||--o{ POIN_TRANSAKSI : "memiliki"
    PETUGAS ||--o{ SETORAN : "menjemput"
    JADWAL ||--o{ PETUGAS : "ditugaskan"
```

---

## 12. Component Diagram — Arsitektur Sistem

```mermaid
graph LR
    subgraph Frontend
        A[Nuxt 4 PWA]
        B[Nuxt UI Components]
        C[Service Worker]
    end

    subgraph Backend
        D[REST API]
        E[Auth Service]
        F[Notification Service]
        G[Points Engine]
    end

    subgraph External
        H[Google Maps API]
        I[Firebase FCM]
        J[E-Wallet API]
        K[AI Image Recognition]
    end

    subgraph Database
        L[(PostgreSQL)]
        M[(Redis Cache)]
    end

    A --> D
    B --> A
    C --> I
    D --> L
    D --> M
    E --> D
    F --> I
    G --> J
    A --> H
    A --> K
```

---

*Sketsa dibuat menggunakan Mermaid Diagram — UX Database BINUS 2026*
