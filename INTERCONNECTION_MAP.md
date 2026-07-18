# WedInvite — Peta Interkoneksi Halaman & Tema

## Daftar File

| File | Fungsi |
|------|--------|
| `index.html` | Landing page / beranda publik |
| `auth.html` | Login & registrasi pengguna |
| `dashboard.html` | Dashboard pengguna dengan statistik |
| `create-invitation.html` | Form wizard pembuatan undangan (3 langkah) |
| `editor.html` | Editor undangan dengan live preview |
| `invitation.html` | Undangan publik — tema Royal Navy Gold |
| `invitation-rustic.html` | Undangan publik — tema Rustic Garden |
| `themes.html` | Galeri pemilihan template/tema |
| `guests.html` | Daftar tamu & RSVP |
| `settings.html` | Pengaturan akun & undangan |
| `share.html` | Bagikan link & QR code |
| `subscription.html` | Pilih & perpanjang paket |
| `checkout.html` | Pembayaran |
| `help.html` | Pusat bantuan & FAQ |

---

## Diagram Alur Navigasi

```
                    ┌─────────────┐
                    │  index.html │ ← Beranda publik
                    └──────┬──────┘
                           │ CTA: Buat Undangan / Login
           ┌───────────────┼───────────────┐
           ▼               ▼               ▼
    ┌────────────┐  ┌────────────┐  ┌────────────┐
    │  auth.html │  │create-inv. │  │  help.html │
    │ (Masuk/Daftar)│  │ (Wizard)   │  │ (Bantuan)  │
    └──────┬─────┘  └─────┬──────┘  └────────────┘
           │              │
           │              ▼
           │         ┌────────────┐
           │         │ editor.html│ ← Pilih tema di sini
           │         │  ?theme=   │
           │         └─────┬──────┘
           │               │
           ▼               ▼
    ┌────────────┐  ┌────────────┐
    │dashboard.  │  │invitation. │ ← Tema aktif
    │   html     │  │  html      │    Royal Navy Gold
    └─────┬──────┘  └────────────┘
          │         ┌────────────┐
          │         │invitation- │ ← Tema baru
          │         │rustic.html │    Rustic Garden
          │         └────────────┘
          │
    ┌─────┴──────┬────────────┬────────────┐
    ▼            ▼            ▼            ▼
┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
│themes. │ │guests. │ │settings│ │ share. │
│ html   │ │ html   │ │.html   │ │ html   │
└───┬────┘ └────────┘ └────────┘ └────────┘
    │
    ▼
┌────────────┐
│subscription│
│   .html    │
└─────┬──────┘
      ▼
┌────────────┐
│ checkout.  │
│   html     │
└────────────┘
```

---

## Tema yang Tersedia

### 1. Royal Navy Gold (Default)
- **File**: `invitation.html`
- **Palet**: Navy `#0a0a1a`, Gold `#c9a96e`, Cream `#faf7f2`
- **Nuansa**: Elegan, klasik, mewah
- **Akses**: `invitation.html?theme=royal-navy-gold`

### 2. Rustic Garden (Baru)
- **File**: `invitation-rustic.html`
- **Palet**: Sage `#4a5d48`, Terracotta `#c67b5c`, Warm Cream `#f5f0e6`
- **Nuansa**: Alami, vintage, hangat, botanical
- **Akses**: `invitation-rustic.html`
- **Fitur khusus**:
  - Floral SVG dividers
  - Warna earthy & organic
  - Background image garden/rustic
  - Border dekoratif pada opening
  - Accent garis vertikal pada event cards

---

## Titik Hubungan Antar-Halaman

### Dari Beranda (index.html)
- `Dashboard` → `dashboard.html`
- `Buat Undangan` → `create-invitation.html`
- `Lihat Template` → `themes.html`
- `Bantuan` → `help.html`
- `Pilih Premium` → `checkout.html?plan=premium`

### Dari Auth (auth.html)
- `Beranda` → `index.html`
- Setelah login → `dashboard.html`

### Dari Dashboard (dashboard.html)
- `Buat Undangan` → `create-invitation.html`
- `Template` → `themes.html`
- `Daftar Tamu` → `guests.html`
- `Pengaturan` → `settings.html`
- `Bantuan` → `help.html`
- `Edit Undangan` → `editor.html?id=1`
- `Bagikan` → `share.html?id=1`
- `Beranda` → `index.html`

### Dari Create Invitation (create-invitation.html)
- `Dashboard` → `dashboard.html`
- `Selanjutnya` → `editor.html?theme={selected}`

### Dari Editor (editor.html)
- `Dashboard` → `dashboard.html`
- `Pratinjau` → `invitation.html` (atau `invitation-rustic.html` untuk rustic)
- `Simpan` → menyimpan ke localStorage
- `Pengaturan` → `settings.html`
- `Aktivasi` → `subscription.html`
- `Sebar` → `share.html`

### Dari Themes (themes.html)
- `Dashboard` → `dashboard.html`
- `Buat Baru` → `create-invitation.html`
- `Pilih Tema Royal Navy` → `editor.html?theme=royal-navy-gold`
- `Pratinjau Royal Navy` → `invitation.html?theme=royal-navy-gold`
- `Pilih Tema Rustic` → `editor.html?theme=rustic-garden`
- `Pratinjau Rustic` → `invitation-rustic.html`

### Dari Invitation (Publik)
- **Royal Navy**: `invitation.html` (dengan switcher ke Rustic)
- **Rustic Garden**: `invitation-rustic.html` (dengan switcher ke Royal Navy)
- Keduanya memiliki navigasi tema untuk demo

### Dari Settings (settings.html)
- `Editor` → `editor.html`

### Dari Share (share.html)
- `Dashboard` → `dashboard.html`

### Dari Subscription (subscription.html)
- `Editor` → `editor.html`
- `Perpanjang` → `checkout.html?plan=premium`

### Dari Checkout (checkout.html)
- `Aktivasi` → `subscription.html`
- Setelah bayar → `dashboard.html`

### Dari Guests (guests.html)
- `Dashboard` → `dashboard.html`

### Dari Help (help.html)
- `Beranda` → `index.html`
- `WhatsApp` → `https://wa.me/6281234567890`

---

## Implementasi Tema di Editor

Editor (`editor.html`) sekarang mendukung switching tema dinamis:

1. **URL Parameter**: `editor.html?theme=rustic-garden`
2. **CSS Variables**: `applyTheme()` mengoverride variabel `:root`
3. **Preview Update**: Background, warna section, dan accent disesuaikan
4. **Badge Tema**: Indikator tema aktif di topbar editor

### Variabel yang Dioverride (Rustic)
| Variabel | Royal Navy | Rustic Garden |
|----------|-----------|---------------|
| `--navy` | `#0a0a1a` | `#4a5d48` |
| `--navy-light` | `#141428` | `#5c6b56` |
| `--gold` | `#c9a96e` | `#c67b5c` |
| `--gold-light` | `#e8d5b0` | `#e8a87c` |
| `--cream` | `#faf7f2` | `#f5f0e6` |
| `--gray` | `#8a8a9a` | `#7a7a6a` |

---

## Catatan Teknis

- **Redirect Otomatis**: `invitation.html?theme=rustic-garden` akan redirect ke `invitation-rustic.html`
- **Theme Switcher**: Kedua file undangan memiliki tombol switch tema untuk demo
- **LocalStorage**: Data user & undangan disimpan di browser (demo mode)
- **Responsive**: Semua halaman mobile-first dengan breakpoint 640px
