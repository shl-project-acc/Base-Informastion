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

## Tips Penting
- Pastikan email yang dikonfigurasi sama dengan email GitHub/GitLab Anda
- Gunakan HTTPS atau SSH untuk koneksi ke remote repository
- Jika menggunakan token, simpan token dengan aman
- Selalu verifikasi remote sebelum push pertama kali

## Troubleshooting Umum
1. Authentication failed: Pastikan kredensial benar
2. Remote already exists: Gunakan `git remote remove origin` sebelum menambah remote baru
3. Branch conflicts: Pastikan branch lokal sesuai dengan remote