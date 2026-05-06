# Sketsa Aplikasi ShopSync — Belanja Pintar
## Mermaid Diagrams

---

## 1. User Flow Diagram — Alur Utama Aplikasi

```mermaid
flowchart TD
    A[Buka Aplikasi] --> B{Sudah Login?}
    B -->|Tidak| C[Halaman Login]
    C --> D[Login via ShopeePay / Email]
    D --> E[Dashboard Home]
    B -->|Ya| E

    E --> F[AI Smart Search]
    E --> G[Rekomendasi AI]
    E --> H[Keranjang]
    E --> I[Pesanan Saya]
    E --> J[Profil]

    F --> F1[Ketik Kata Kunci Natural]
    F1 --> F2[AI Filter Otomatis]
    F2 --> F3[Hasil Produk Terverifikasi]
    F3 --> F4[Detail Produk]

    F4 --> F4A[Video 360°]
    F4 --> F4B[AI Trust Score]
    F4 --> F4C[Ulasan Verified]
    F4 --> F4D[Chat AI Produk]

    F4 --> H

    G --> G1[Produk Personal]
    G --> G2[Flash Sale Verified]
    G --> G3[Trending Items]

    H --> H1[Review Keranjang]
    H1 --> H2[Pilih Alamat]
    H2 --> H3[Pilih Pembayaran]
    H3 --> H4[Konfirmasi & Bayar]
    H4 --> I

    I --> I1[Tracking Live Kurir]
    I --> I2[Status Pesanan]
    I --> I3[Riwayat Transaksi]
```

---

## 2. Sitemap / Information Architecture

```mermaid
graph TD
    ROOT[ShopSync App] --> HOME[Home / Dashboard]
    ROOT --> SEARCH[Pencarian AI]
    ROOT --> CART[Keranjang]
    ROOT --> ORDER[Pesanan Saya]
    ROOT --> PROFILE[Profil]

    HOME --> HOME1[Rekomendasi AI Personal]
    HOME --> HOME2[Flash Sale Terverifikasi]
    HOME --> HOME3[Trending Produk]
    HOME --> HOME4[Quick Actions]

    SEARCH --> S1[AI Search Bar]
    SEARCH --> S2[Filter Pintar]
    SEARCH --> S3[Hasil Terfilter]
    SEARCH --> S4[Riwayat Pencarian]

    S3 --> DETAIL[Detail Produk]
    DETAIL --> D1[Video 360°]
    DETAIL --> D2[AI Trust Score]
    DETAIL --> D3[Ulasan Verified]
    DETAIL --> D4[Chat AI Produk]

    CART --> C1[Daftar Produk]
    CART --> C2[Voucher & Subtotal]
    CART --> C3[Checkout Express]

    ORDER --> O1[Tracking Live]
    ORDER --> O2[Status Pesanan]
    ORDER --> O3[Riwayat]

    PROFILE --> P1[Data Diri]
    PROFILE --> P2[Preferensi AI]
    PROFILE --> P3[Notifikasi]
    PROFILE --> P4[Bantuan]
```

---

## 3. Wireframe — Halaman Home (Mobile)

```mermaid
block-beta
    columns 1
    block:HEADER
        columns 3
        A["☰"] B["ShopSync"] C["🛒"]
    end
    space
    block:SEARCH
        columns 1
        D["🔍 Cari produk dengan AI..."]
    end
    space
    block:RECO
        columns 1
        E["📦 Rekomendasi untuk Anda"]
    end
    block:PRODUCTS
        columns 3
        F["Anker 33W\nRp150rb\n⭐ 4.9"] G["Samsung Case\nRp50rb\n⭐ 4.8"] H["Earphone\nRp120rb\n⭐ 4.7"]
    end
    space
    block:FLASH
        columns 1
        I["⚡ Flash Sale Terverifikasi"]
    end
    block:FLASHITEMS
        columns 3
        J["Produk 1\n🏷️ 50% OFF"] K["Produk 2\n🏷️ 30% OFF"] L["Produk 3\n🏷️ 40% OFF"]
    end
    space
    block:NAV
        columns 5
        M["🏠\nHome"] N["🔍\nCari"] O["🛒\nKeranjang"] P["📦\nPesanan"] Q["👤\nProfil"]
    end
```

---

## 4. Wireframe — Halaman Detail Produk

```mermaid
block-beta
    columns 1
    block:HEADER2
        columns 3
        A2["← Back"] B2["Anker Nano 33W"] C2["🛒"]
    end
    space
    block:IMAGE
        columns 1
        D2["📸 Video 360° Produk"]
    end
    space
    block:INFO
        columns 2
        E2["Rp 150.000"] F2["AI Trust: 95/100 ✅"]
    end
    block:SELLER
        columns 1
        G2["🏪 TechStore Official — Seller Emas ⭐"]
    end
    space
    block:REVIEWS
        columns 1
        H2["📝 Ulasan Verified (234 ulasan)"]
    end
    block:REVIEW1
        columns 1
        I2["⭐⭐⭐⭐⭐ 'Fast charging mantap!' — Buyer ✓"]
    end
    space
    block:ACTIONS
        columns 2
        J2["💬 Chat AI"] K2["🛒 Tambah Keranjang"]
    end
```

---

## 5. Wireframe — Halaman Keranjang & Checkout

```mermaid
block-beta
    columns 1
    block:HEADER3
        columns 1
        A3["🛒 Keranjang Belanja (2 item)"]
    end
    space
    block:ITEM1
        columns 3
        B3["📦"] C3["Anker Nano 33W\nRp150.000\nQty: 1"] D3["🗑️"]
    end
    block:ITEM2
        columns 3
        E3["📦"] F3["Samsung Case\nRp50.000\nQty: 1"] G3["🗑️"]
    end
    space
    block:VOUCHER
        columns 1
        H3["🎫 Voucher: Gratis Ongkir J&T"]
    end
    block:SUBTOTAL
        columns 2
        I3["Subtotal:"] J3["Rp 200.000"]
    end
    space
    block:CHECKOUT
        columns 1
        K3["✅ Checkout Express (3 langkah)"]
    end
```

---

## 6. Wireframe — Halaman Tracking Pesanan

```mermaid
block-beta
    columns 1
    block:HEADER4
        columns 1
        A4["📦 Pesanan #1234 — Tracking Live"]
    end
    space
    block:MAP
        columns 1
        B4["🗺️ Peta Real-time Kurir J&T"]
    end
    space
    block:STATUS
        columns 1
        C4["Status: Dalam Pengiriman 🚚"]
    end
    block:ETA
        columns 1
        D4["ETA: Besok, 09:00 WIB"]
    end
    space
    block:TIMELINE
        columns 1
        E4["✅ Pesanan Dikonfirmasi — 21:05\n✅ Sedang Dikemas — 21:30\n✅ Dikirim ke Kurir — 22:00\n⏳ Dalam Perjalanan — ..."]
    end
    space
    block:GUARANTEE
        columns 1
        F4["🛡️ Jaminan 100% — Uang kembali jika barang KW"]
    end
```

---

## 7. User Scenario Flow — "Belanja Charger Malam Hari"

```mermaid
sequenceDiagram
    participant S as Surya (User)
    participant A as ShopSync App
    participant AI as AI Engine
    participant Seller as Seller Verified
    participant K as Kurir J&T

    S->>A: Buka app & login ShopeePay
    A->>AI: Load preferensi user
    AI->>A: Tampilkan rekomendasi personal
    A->>S: Homepage clean + "Charger 33W untuk Samsung Anda"

    S->>A: Ketik "charger fast charging 33W Samsung"
    A->>AI: Proses natural language search
    AI->>A: 12 produk terfilter (rating >4.8, verified)
    A->>S: Tampilkan hasil + Smart Filter

    S->>A: Klik "Anker Nano 33W"
    A->>S: Detail: Video 360°, Trust Score 95/100
    S->>A: Chat AI "Cocok Samsung A54?"
    AI->>S: "Ya, support PD 3.0 ✓"

    S->>A: Tambah ke Keranjang
    S->>A: Checkout Express (3-step)
    A->>Seller: Order confirmed
    A->>S: Notifikasi "Pesanan diproses"

    Seller->>K: Serahkan paket
    K->>A: Update tracking real-time
    A->>S: "Paket dalam perjalanan, ETA 09:00"
    K->>S: Paket sampai ✓
```
