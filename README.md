# 🔐 BOT SYSTEM - WHITELIST GITHUB (UNIFIED VERSION)

## 📋 Cara Setup

### 1️⃣ Setup GitHub Repository

1. **Buat Repository Baru di GitHub**
   - Pergi ke https://github.com/new
   - Nama repository: terserah (misal: `roblox-bot-whitelist`)
   - Set sebagai **Public** (penting!)
   - Centang "Add a README file"
   - Klik "Create repository"

2. **Upload File `whitelist.json`**
   - Klik "Add file" → "Create new file"
   - Nama file: `whitelist.json`
   - Copy paste isi dari file `whitelist.json` yang sudah saya buatkan
   - Klik "Commit new file"

3. **Dapatkan Raw URL**
   - Buka file `whitelist.json` di GitHub
   - Klik tombol "Raw"
   - Copy URL dari address bar
   - Contoh format: `https://raw.githubusercontent.com/USERNAME/REPO/main/whitelist.json`

---

### 2️⃣ Setup di Roblox Studio

1. **Upload Bot System (All-in-One!):**
   - `BotSystem_Unified.lua` → masukkan ke **ServerScriptService**
   - Buka file tersebut
   - **GANTI** bagian ini dengan Raw URL kamu (sekitar baris 22):
     ```lua
     Whitelist.GITHUB_URL = "https://raw.githubusercontent.com/USERNAME/REPO/main/whitelist.json"
     ```
   - File ini sudah include whitelist module di dalamnya, jadi **TIDAK PERLU FILE TAMBAHAN!** ✅

2. **Enable HTTP Requests:**
   - Pergi ke **Home** → **Game Settings** → **Security**
   - Centang **"Allow HTTP Requests"**
   - Klik **Save**

---

### 3️⃣ Edit Whitelist (whitelist.json)

Format JSON untuk whitelist:

```json
{
  "users": [
    123456789,
    987654321,
    111222333
  ],
  "groups": [
    {
      "id": 12345678,
      "name": "My Group Name",
      "minRank": 0
    },
    {
      "id": 87654321,
      "name": "VIP Group",
      "minRank": 10
    }
  ],
  "lastUpdated": "2026-01-29",
  "notes": "Whitelist untuk Bot System"
}
```

**Penjelasan:**
- `users`: Array berisi User ID yang diizinkan
- `groups`: Array berisi Group yang diizinkan
  - `id`: Group ID di Roblox
  - `name`: Nama group (opsional, cuma untuk catatan)
  - `minRank`: Minimum rank yang diperlukan (0 = semua member)

---

### 4️⃣ Cara Mendapatkan User ID

**Via Website:**
1. Pergi ke https://www.roblox.com/users/PROFILE/profile
2. Lihat angka di URL (contoh: `/users/123456789/profile`)

**Via Script (di Command Bar):**
```lua
print(game.Players.LocalPlayer.UserId)
```

---

### 5️⃣ Cara Mendapatkan Group ID

1. Pergi ke halaman group di Roblox
2. Lihat URL: `https://www.roblox.com/groups/12345678/GROUP-NAME`
3. Angka `12345678` adalah Group ID

---

## ✏️ Update Whitelist

### Edit di GitHub:
1. Buka file `whitelist.json` di repository
2. Klik tombol "Edit" (icon pensil)
3. Edit list user/group
4. Klik "Commit changes"
5. **Whitelist akan auto-update dalam 5 menit** (karena cache)

### Force Refresh (Optional):
Jika ingin langsung update tanpa tunggu 5 menit, jalankan command ini di **Server Console**:
```lua
-- Script ini sudah ada di BotSystem_Unified.lua
-- Tinggal panggil function-nya via command atau buat admin command
```

---

## 🎯 Cara Kerja

1. **Player join game** → Bot system check whitelist
2. **Whitelist di-fetch dari GitHub** → disimpan di cache 5 menit
3. **Player spawn bot** → system check:
   - Apakah User ID ada di list `users`?
   - Apakah player member group yang ada di list `groups`?
   - Apakah rank player >= `minRank` (jika ada)?
4. **Jika pass** → bot spawn ✅
5. **Jika gagal** → spawn diabaikan, warning di console ⛔

---

## 📝 Contoh Penggunaan

### Whitelist by User ID:
```json
{
  "users": [
    123456789,
    987654321
  ],
  "groups": []
}
```

### Whitelist by Group (Semua Member):
```json
{
  "users": [],
  "groups": [
    {
      "id": 12345678,
      "name": "My Cool Group",
      "minRank": 0
    }
  ]
}
```

### Whitelist by Group (Rank 10+):
```json
{
  "users": [],
  "groups": [
    {
      "id": 12345678,
      "name": "VIP Group",
      "minRank": 10
    }
  ]
}
```

### Kombinasi User + Group:
```json
{
  "users": [
    123456789
  ],
  "groups": [
    {
      "id": 12345678,
      "name": "Staff Group",
      "minRank": 5
    }
  ]
}
```

---

## 🐛 Troubleshooting

### ❌ Error: "HTTP 404 (Not Found)"
- Pastikan repository bersifat **Public**
- Pastikan URL yang digunakan adalah **Raw URL**
- Cek spelling nama file (harus `whitelist.json`)

### ❌ Error: "HttpService is not enabled"
- Pergi ke Game Settings → Security
- Centang "Allow HTTP Requests"

### ❌ Whitelist tidak update
- Tunggu 5 menit (karena cache)
- Atau restart server untuk force reload

### ❌ Player tidak bisa spawn bot
- Cek **Server Console** untuk melihat pesan error
- Pastikan User ID atau Group ID benar
- Pastikan format JSON valid (gunakan https://jsonlint.com/)
- Pastikan HTTP Requests sudah enabled

---

## 🎁 Keuntungan Versi Unified

✅ **Hanya 1 File** - Tidak perlu upload WhitelistModule terpisah  
✅ **Lebih Simple** - Semua kode ada di satu tempat  
✅ **Easy Setup** - Tinggal edit 1 baris untuk GitHub URL  
✅ **No Dependencies** - Tidak perlu require module dari ReplicatedStorage  

---

## 🔒 Security Notes

- File `whitelist.json` bersifat **public** (siapa saja bisa lihat)
- Jangan masukkan informasi sensitif di file ini
- Hanya gunakan User ID & Group ID (data public)

---

## 📞 Support

Jika ada masalah, cek:
1. **Server Console** untuk error messages
2. Format JSON di https://jsonlint.com/
3. Raw URL sudah benar
4. HTTP Requests sudah enabled di Game Settings

---

Selamat menggunakan! 🎉
