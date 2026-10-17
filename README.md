# Hybrid SVAR + XGBoost untuk Prediksi Kurs JPY/IDR dan KRW/IDR

Notebook ini membandingkan **XGBoost baseline** dengan **Hybrid SVAR + XGBoost** untuk memprediksi kurs JPY/IDR dan KRW/IDR. SVAR menangkap hubungan dinamis antarkurs; XGBoost memodelkan pola nonlinier dari fitur teknikal, lag harga, dan output SVAR.

Proyek ini menggunakan data kurs historis harian dari Investing.com untuk periode **2 Januari 2002 sampai 1 Januari 2026**. Paper proyek melaporkan 6.260 observasi setelah kedua seri kurs digabungkan berdasarkan tanggal.

## Struktur repository

```text
hybrid-svar-xgboost-jpy-krw-idr/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── hybrid_svar_xgboost_jpy_krw_idr.ipynb
├── data/
│   ├── Kurs Transaksi JPY_IDR.csv
│   └── Kurs Transaksi KRW_IDR.csv
└── references/
    ├── README.md
    └── paper-hybrid-svar-xgboost-jpy-krw-idr.pdf
```

## Jalankan di Google Colab

Notebook menggunakan dialog upload Google Colab untuk mengambil CSV dari komputer.

1. Buka notebook di Google Colab.
2. Jalankan cell **Import Library**.
3. Jalankan cell **Load dan Preprocessing Data**.
4. Pilih file `Kurs Transaksi JPY_IDR.csv` dan `Kurs Transaksi KRW_IDR.csv` saat diminta.
5. Lanjutkan dengan **Runtime → Run all** atau jalankan cell satu per satu.

Nama file harus mengandung `JPY` atau `KRW` karena notebook mencari file berdasarkan nama tersebut. Kalau notebook dibuka dari GitHub, CSV tetap perlu dipilih saat dialog upload muncul.

## Format CSV yang diterima

Setiap CSV wajib memiliki tanggal, harga penutupan, pembukaan, tertinggi, terendah, dan perubahan persen. Notebook menerima nama kolom Investing.com berbahasa Inggris maupun terjemahan Indonesia:

| Kolom yang dikenali | Alternatif |
|---|---|
| `Tanggal` | `Date` |
| `Terakhir` | `Close`, `Last`, `Price` |
| `Pembukaan` | `Open` |
| `Tertinggi` | `High` |
| `Terendah` | `Low` |
| `Perubahan%` | `ChangePct`, `Change%`, `Change %` |

`Vol.` atau `Volume` bersifat opsional dan akan dihapus saat preprocessing. Angka dengan koma desimal seperti `106,44` dan angka dengan titik desimal seperti `106.44` didukung.

## Dependensi

Daftar package ada di [`requirements.txt`](requirements.txt): NumPy, pandas, Matplotlib, Seaborn, scikit-learn, XGBoost, dan statsmodels.

Untuk instalasi lokal:

```bash
python -m pip install -r requirements.txt
```

Notebook ditujukan untuk Google Colab karena memakai `google.colab.files.upload()`. Untuk menjalankannya secara lokal, ganti cell upload agar membaca CSV dari path lokal.

## Keluaran notebook

Notebook menghasilkan file berikut di lingkungan tempat notebook dijalankan:

- `dataset_clean_JPY_KRW_IDR.csv` — dataset gabungan setelah preprocessing.
- `predictions_all_models.csv` — nilai aktual dan prediksi model.
- `evaluation_results.csv` — tabel metrik evaluasi.
- Grafik `.png` yang dibuat notebook.

Keluaran tersebut tidak perlu ditambahkan ke repository untuk menjalankan analisis; unggah jika ingin membagikannya sebagai artefak hasil.

## Sumber data

Paper proyek menyebut sumber dataset sebagai file CSV historis dari **Investing.com**:

- [JPY/IDR Historical Data](https://www.investing.com/currencies/jpy-idr-historical-data)
- [KRW/IDR Historical Data](https://www.investing.com/currencies/krw-idr-historical-data)

Data yang dipakai dalam paper mencakup periode 2 Januari 2002–1 Januari 2026. Halaman sumber dapat berubah seiring waktu. Untuk mereproduksi hasil, gunakan CSV asli yang dipakai dalam analisis dan catat tanggal unduhnya. Periksa ketentuan sumber sebelum membagikan salinan CSV di repository publik.

## Paper proyek

Sanjiro Ozara Liu Tama, “Model Hybrid SVAR-XGBoost untuk Prediksi dan Analisis Keterkaitan Dinamis Kurs JPY/IDR dan KRW/IDR Periode 2002–2026,” manuskrip.

PDF disimpan di [`references/paper-hybrid-svar-xgboost-jpy-krw-idr.pdf`](references/paper-hybrid-svar-xgboost-jpy-krw-idr.pdf). Sebelum membuat repository publik, pastikan Anda memang berhak membagikan PDF tersebut dan nyaman dengan informasi kontak yang tercetak di dalamnya.

## Lisensi

Belum ditentukan. Tambahkan file `LICENSE` jika ingin menetapkan izin penggunaan ulang untuk kode dan materi yang haknya Anda miliki. Pastikan ketentuan itu tidak diterapkan ke dataset atau karya pihak lain tanpa izin.
