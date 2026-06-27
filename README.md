# 🤖 WAGuard Bot v2.4

Bot WhatsApp premium untuk manajemen dan perlindungan grup secara otomatis.
Dibangun dengan **Baileys** (library WA non-official terpopuler).

---

## ✨ Fitur Utama

| Fitur | Keterangan |
|-------|-----------|
| 🛡️ Anti-Spam | Blokir link, kata kotor, stiker dewasa |
| 🌊 Flood Protection | Deteksi & peringatkan member yang spam pesan |
| ✅ Captcha Member Baru | Verifikasi otomatis saat join, kick jika tidak jawab |
| ⚠️ Sistem Peringatan | Peringatan bertahap → kick otomatis |
| 🚫 Blacklist Global | Blokir nomor di semua grup sekaligus |
| 👋 Pesan Sambutan | Welcome & goodbye custom per grup |
| 🔇 Mute/Unmute Grup | Kunci grup hanya untuk admin |
| 📢 Tag Semua Member | Mention seluruh anggota sekaligus |
| ⏰ Pesan Terjadwal | Broadcast otomatis via cron schedule |
| ⚙️ Toggle Per Fitur | Aktifkan/nonaktifkan fitur per grup |

---

## 🚀 Cara Instalasi

### Prasyarat
- **Node.js** versi 18 ke atas → [nodejs.org](https://nodejs.org)
- **npm** (sudah termasuk dengan Node.js)

### Langkah-langkah

```bash
# 1. Clone atau ekstrak folder ini
cd waguard-bot

# 2. Install semua dependensi
npm install

# 3. Jalankan bot
npm start
```

> Saat pertama kali dijalankan, QR Code akan muncul di terminal.  
> Buka WhatsApp → Perangkat Tertaut → Tautkan Perangkat → Scan QR.

---

## ⚙️ Konfigurasi

Edit file `src/config.js` sesuai kebutuhan:

```js
// Ganti dengan nomor WhatsApp owner (format internasional tanpa +)
OWNER: ['628123456789'],

// Prefix perintah bot
PREFIX: '!',

// Jumlah peringatan sebelum kick otomatis
MAX_WARNINGS: 3,

// Link yang diizinkan di grup
LINK_WHITELIST: ['wa.me', 'whatsapp.com', 'youtube.com'],
```

---

## 📋 Daftar Perintah

> Semua perintah dimulai dengan prefix `!` (bisa diubah di config)

### Perintah Admin

| Perintah | Keterangan |
|----------|-----------|
| `!help` | Tampilkan daftar perintah |
| `!warn @user [alasan]` | Beri peringatan ke member |
| `!kick @user` | Keluarkan member dari grup |
| `!ban @user` | Blacklist global + kick |
| `!unban @user` | Hapus dari blacklist |
| `!mute` | Kunci grup (hanya admin bisa kirim) |
| `!unmute` | Buka kunci grup |
| `!setwelcome [pesan]` | Set pesan sambutan custom |
| `!resetwarn @user` | Reset peringatan member ke 0 |
| `!warnlist` | Lihat daftar peringatan di grup |
| `!tagall [pesan]` | Mention semua member |
| `!info` | Status bot & konfigurasi grup |

### Toggle Fitur

```
!toggle antispam     → aktif/nonaktif anti-spam
!toggle link         → aktif/nonaktif blokir link
!toggle katakotor    → aktif/nonaktif filter kata kasar
!toggle sticker      → aktif/nonaktif anti stiker dewasa
!toggle captcha      → aktif/nonaktif captcha member baru
!toggle flood        → aktif/nonaktif flood protection
!toggle welcome      → aktif/nonaktif pesan sambutan
!toggle goodbye      → aktif/nonaktif pesan perpisahan
```

---

## 📁 Struktur File

```
waguard-bot/
├── src/
│   ├── index.js              # Entry point & koneksi bot
│   ├── config.js             # Semua pengaturan utama
│   ├── handlers/
│   │   ├── antispam.js       # Logika anti-spam & peringatan
│   │   ├── group.js          # Event join/leave/captcha
│   │   ├── commands.js       # Semua perintah admin
│   │   └── scheduler.js      # Pesan terjadwal (node-cron)
│   └── utils/
│       ├── database.js       # Database JSON lokal
│       └── helpers.js        # Fungsi bantuan umum
├── data/
│   └── db.json               # Database (otomatis dibuat)
├── sessions/                 # File sesi WA (jangan dihapus!)
├── package.json
└── README.md
```

---

## 🔒 Keamanan

- **Jangan bagikan folder `sessions/`** ke siapapun — berisi data login WA kamu
- **Jangan gunakan nomor utama** untuk bot; gunakan nomor cadangan
- Bot ini menggunakan protokol WhatsApp non-resmi — risiko ban ada jika digunakan berlebihan
- Selalu perbarui Baileys ke versi terbaru: `npm update @whiskeysockets/baileys`

---

## 🐞 Troubleshooting

| Masalah | Solusi |
|---------|--------|
| QR tidak muncul | Pastikan terminal mendukung output teks |
| Bot terputus terus | Periksa koneksi internet; bot akan auto-reconnect |
| Error `sessions` | Hapus folder `sessions/`, jalankan ulang & scan QR baru |
| Perintah tidak jalan | Pastikan bot adalah **admin grup** |
| Link tidak terdeteksi | Periksa pengaturan `LINK_WHITELIST` di config.js |

---

## 📝 Lisensi

Bebas digunakan & dimodifikasi untuk keperluan pribadi/komunitas.  
Jangan digunakan untuk spam atau tindakan yang melanggar syarat layanan WhatsApp.
