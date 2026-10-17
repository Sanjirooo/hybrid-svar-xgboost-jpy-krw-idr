# Upload project ke GitHub lewat Git Bash

Panduan ini untuk upload folder proyek lokal ke repository GitHub baru.

## 1. Buat repository kosong di GitHub

1. Buka GitHub dan pilih **New repository**.
2. Isi nama repository: `hybrid-svar-xgboost-jpy-krw-idr`.
3. Tentukan visibilitas **Private** atau **Public**.
4. Jangan centang pembuatan README, `.gitignore`, atau lisensi. File-file itu sudah ada di folder proyek lokal; repository kosong mencegah konflik saat push pertama.
5. Klik **Create repository**, lalu salin URL HTTPS repository, misalnya `https://github.com/USERNAME/hybrid-svar-xgboost-jpy-krw-idr.git`.

## 2. Buka Git Bash di folder proyek

Jalankan Git Bash, lalu masukkan:

```bash
cd "/c/Users/Liutama/Documents/Codex/2026-10-18/gw-m/outputs/hybrid-svar-xgboost-jpy-krw-idr"
pwd
ls
```

Kalau folder proyek lo ada di lokasi lain, sesuaikan path pada perintah `cd`. Pastikan terlihat file `README.md`, `requirements.txt`, folder `notebooks`, `data`, dan `references`.

## 3. Buat commit pertama dan push

Ganti `USERNAME` dengan username GitHub lo, atau tempel URL HTTPS yang tadi disalin:

```bash
git init
git branch -M main
git add README.md GIT_BASH_GUIDE.md requirements.txt .gitignore notebooks data references
git status
git commit -m "Add JPY KRW IDR forecasting project"
git remote add origin https://github.com/USERNAME/hybrid-svar-xgboost-jpy-krw-idr.git
git remote -v
git push -u origin main
```

Sebelum `git commit`, `git status` akan menampilkan file yang akan masuk ke commit. Pastikan dua dataset CSV terlihat di daftar itu. Saat `git push` pertama, ikuti jendela login browser jika Git Credential Manager memintanya; GitHub tidak menerima password akun sebagai password Git lewat HTTPS.

## 4. Upload perubahan berikutnya

Setelah mengubah README, notebook, atau dataset, jalankan dari folder proyek:

```bash
git add .
git status
git commit -m "Update project files"
git push
```

## Nama dataset dan Colab

CSV yang saat ini ada di `data/` bernama:

- `Kurs Transaksi JPY_IDR.csv`
- `Kurs Transaksi KRW_IDR.csv`

Nama dengan spasi ini tetap terbaca notebook karena notebook mencari `JPY` dan `KRW` pada nama file. Saat notebook dijalankan di Google Colab, cell upload tetap meminta kedua file dipilih dari komputer; file di repository tidak otomatis masuk ke sesi Colab.

Sebelum memilih repository **Public**, cek isi PDF pada `references/` karena halaman judulnya memuat informasi kontak. Pertimbangkan **Private** atau hilangkan PDF jika informasi itu tidak ingin dipublikasikan.
