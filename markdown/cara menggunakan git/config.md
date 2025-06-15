# Konfigurasi Git untuk Menghubungkan Repository Lokal ke Remote

## Langkah-langkah Dasar Konfigurasi Git

### 1. Konfigurasi Identitas
```bash
git config --global user.name "Nama Anda"
git config --global user.email "email@example.com"
```

### 2. Mengecek Konfigurasi
```bash
git config --list
```

### 3. Menghubungkan dengan Remote Repository

#### A. Membuat Repository Baru
```bash
# Inisialisasi git di folder lokal
git init

# Menambahkan remote repository
git remote add origin https://github.com/username/repository.git

# Verifikasi remote
git remote -v
```

#### B. Clone Repository yang Sudah Ada
```bash
git clone https://github.com/username/repository.git
```

### 4. Konfigurasi Branch
```bash
# Set branch default ke main/master
git branch -M main

# Push ke remote repository pertama kali
git push -u origin main
```

### 5. Mengatur Kredensial (Opsional)
```bash
# Menyimpan kredensial
git config --global credential.helper store

# Atau menyimpan kredensial sementara (cache)
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
```

## Mengganti User Git (Ketika Ada Multiple User)
```bash
# Hapus kredensial yang tersimpan di sistem
git config --global --unset user.name
git config --global --unset user.email
git config --global --unset credential.helper

# Untuk Windows, hapus kredensial dari Credential Manager
# Buka Control Panel > Credential Manager > Windows Credentials
# Cari git atau github kemudian hapus

# Set kredensial baru
git config --global user.name "Nama Baru"
git config --global user.email "email.baru@example.com"

# Verifikasi perubahan
git config --list

# Pada push berikutnya, Git akan meminta kredensial baru
```

### Tips Mengganti User
- Pastikan sudah backup kode sebelum mengganti user
- Jika menggunakan token, generate token baru di GitHub/GitLab
- Untuk repository spesifik, bisa set config tanpa --global:
```bash
git config user.name "Nama Baru"
git config user.email "email.baru@example.com"
```

## Contoh Kasus: Pindah ke Akun shl-project-acc
```bash
# 1. Hapus kredensial yang ada
git config --global --unset user.name
git config --global --unset user.email
git config --global --unset credential.helper

# 2. Buka Windows Credential Manager
# - Buka Start Menu > ketik "Credential Manager"
# - Pilih "Windows Credentials"
# - Cari kredensial yang berkaitan dengan github.com
# - Hapus semua kredensial github yang ada

# 3. Set kredensial baru untuk shl-project-acc
git config --global user.name "shl-project-acc"
git config --global user.email "email_shl_project@example.com"

# 4. Verifikasi konfigurasi baru
git config --list

# 5. Coba push ulang
# Git akan meminta username dan password/token baru
git push origin main
```

### Catatan Penting
- Pastikan Anda memiliki akses ke repository shl-project-acc
- Gunakan Personal Access Token dari akun shl-project-acc
- Token bisa dibuat di GitHub: Settings > Developer settings > Personal access tokens
- Saat push pertama kali, masukkan username 'shl-project-acc' dan token sebagai password

## Tips Penting
- Pastikan email yang dikonfigurasi sama dengan email GitHub/GitLab Anda
- Gunakan HTTPS atau SSH untuk koneksi ke remote repository
- Jika menggunakan token, simpan token dengan aman
- Selalu verifikasi remote sebelum push pertama kali

## Troubleshooting Umum
1. Authentication failed: Pastikan kredensial benar
2. Remote already exists: Gunakan `git remote remove origin` sebelum menambah remote baru
3. Branch conflicts: Pastikan branch lokal sesuai dengan remote

## Troubleshooting Error 403 (Permission Denied)
Jika muncul error: `Permission to shl-project-acc/Base-Informastion.git denied to aryakenzo`, ikuti langkah berikut:

```bash
# 1. Hapus semua cache git credential di Windows
cmdkey /delete:git:https://github.com

# 2. Hapus semua konfigurasi git global
git config --global --unset-all user.name
git config --global --unset-all user.email
git config --global --unset-all credential.helper

# 3. Hapus cache credential di git
git config --system --unset credential.helper

# 4. Set ulang konfigurasi untuk shl-project-acc
git config --global user.name "shl-project-acc"
git config --global user.email "email_shl_project@example.com"

# 5. Set credential helper untuk Windows
git config --global credential.helper wincred

# 6. Coba push ulang (akan diminta login)
git push origin main
```

### Langkah Tambahan jika Masih Error:
1. Buka Windows Credential Manager
   - Tekan Win + R
   - Ketik "control /name Microsoft.CredentialManager"
   - Atau cari "Credential Manager" di Start Menu
2. Pilih "Windows Credentials"
3. Cari dan hapus SEMUA credential yang berhubungan dengan:
   - github.com
   - git
   - GitHub for Windows
4. Restart Git Bash atau Command Prompt
5. Coba push ulang, akan diminta memasukkan credentials baru

### Penting:
- Saat diminta login, gunakan username: shl-project-acc
- Untuk password, gunakan Personal Access Token, BUKAN password GitHub
- Jika belum punya token, buat di:
  GitHub.com > Settings > Developer Settings > Personal Access Tokens > Generate New Token
- Pilih scope minimal: `repo` dan `workflow`