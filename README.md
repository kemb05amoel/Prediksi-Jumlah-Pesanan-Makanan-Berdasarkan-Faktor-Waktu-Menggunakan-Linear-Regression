# Prediksi Jumlah Pesanan Makanan Berdasarkan Faktor Waktu Menggunakan Linear Regression

Proyek Data Science untuk menganalisis pola permintaan makanan (*food demand forecasting*) dan memprediksi jumlah pesanan berdasarkan faktor waktu serta informasi pusat distribusi dan produk makanan.

## Tujuan
1. Memahami karakteristik data historis pemesanan makanan.
2. Mengidentifikasi pola pesanan berdasarkan waktu dan karakteristik terkait.
3. Membangun model **Linear Regression** sebagai metode utama.
4. Membandingkan hasilnya dengan baseline, Ridge Regression, dan Random Forest.
5. Menyusun insight dan rekomendasi operasional berdasarkan hasil analisis.

## Dataset
Proyek menggunakan tiga dataset:

| File | Deskripsi | Kolom penting |
|---|---|---|
| `train.csv` | Riwayat pesanan | `id`, `week`, `center_id`, `meal_id`, `checkout_price`, `base_price`, `emailer_for_promotion`, `homepage_featured`, `num_orders` |
| `fulfilment_center_info.csv` | Informasi pusat distribusi | `center_id`, `city_code`, `region_code`, `center_type`, `op_area` |
| `meal_info.csv` | Informasi produk makanan | `meal_id`, `category`, `cuisine` |

Target prediksi adalah `num_orders`. Dataset digabungkan menggunakan `center_id` dan `meal_id`.

Ukuran data pada pengujian:
- Data pesanan: 456.548 baris, 9 kolom.
- Informasi pusat distribusi: 77 baris, 5 kolom.
- Informasi makanan: 51 baris, 3 kolom.
- Hasil penggabungan: sekitar 456.548 baris dengan informasi transaksi, pusat distribusi, dan makanan.

Dataset berkaitan dengan kompetisi *Food Demand Forecasting* Analytics Vidhya bersama Genpact (2018). Periksa kembali lisensi dan ketentuan atribusi dari sumber tempat dataset diperoleh.

## Metodologi
Alur proyek mengacu pada tahapan CRISP-DM:
1. **Business Understanding** — mendefinisikan masalah dan tujuan prediksi permintaan.
2. **Data Understanding** — memeriksa struktur, tipe data, distribusi, dan kualitas data.
3. **Data Preparation** — menggabungkan dataset, memeriksa data kosong/duplikat, menyiapkan fitur, encoding, scaling, dan feature engineering sesuai kebutuhan.
4. **Modeling** — melatih Linear Regression sebagai model utama serta model pembanding.
5. **Evaluation** — mengevaluasi model menggunakan MAE, RMSE, dan R².
6. **Recommendation** — menyusun insight dan rekomendasi berdasarkan hasil.

### Pembagian data
Pemisahan dilakukan berdasarkan urutan waktu. Pada salah satu pengujian, data pelatihan mencakup minggu 1–116 dan data uji minggu 117–145. Pelatihan menggunakan sampel 150.000 baris dari 361.348 baris pada periode pelatihan untuk efisiensi komputasi; data uji berjumlah 95.200 baris.

## Model dan Metrik
- **Linear Regression:** model utama proyek.
- **Ridge Regression:** pembanding dengan regularisasi.
- **Random Forest Regressor:** pembanding non-linear.
- **Dummy Regressor:** baseline sederhana.

Metrik:
- **MAE:** rata-rata kesalahan absolut prediksi.
- **RMSE:** akar rata-rata kuadrat kesalahan dan lebih sensitif terhadap kesalahan besar.
- **R²:** proporsi variasi target yang dapat dijelaskan model pada data evaluasi.

## Hasil Pengujian
Berikut hasil dari salah satu eksekusi notebook. Perbarui tabel ini jika konfigurasi atau hasil eksekusi berubah.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression (utama) | 148,06 | 256,83 | 0,5055 |
| Ridge Regression | 148,05 | 256,83 | 0,5055 |
| Random Forest Regressor | 96,49 | 195,90 | 0,7123 |
| Dummy Regressor (baseline) | 219,63 | 365,60 | -0,0021 |

Pada pengujian tersebut, Linear Regression lebih baik daripada baseline. Random Forest menghasilkan MAE dan RMSE lebih rendah serta R² lebih tinggi. Linear Regression tetap menjadi metode utama sesuai fokus proyek; Random Forest digunakan sebagai pembanding.

## Struktur Repository
```text
.
├── Arus_Bawah_Final_Data_Science.ipynb
├── train.csv
├── fulfilment_center_info.csv
├── meal_info.csv
├── README.md
└── .gitignore
```

Notebook mencari file CSV di folder `data/` atau direktori kerja saat ini. Dataset dapat disimpan di root repository seperti struktur di atas atau di folder `data/`.

## Instalasi dan Menjalankan
Disarankan menggunakan Python 3.11 atau 3.12.

1. Clone repository:
   ```bash
   git clone https://github.com/kemb05amoel/Prediksi-Jumlah-Pesanan-Makanan-Berdasarkan-Faktor-Waktu-Menggunakan-Linear-Regression.git
   cd Prediksi-Jumlah-Pesanan-Makanan-Berdasarkan-Faktor-Waktu-Menggunakan-Linear-Regression
   ```
2. Buat virtual environment (opsional):
   ```powershell
   # Windows PowerShell
   py -3.12 -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```
   ```bash
   # macOS/Linux
   python3.12 -m venv .venv
   source .venv/bin/activate
   ```
3. Instal dependensi:
   ```bash
   python -m pip install --upgrade pip
   python -m pip install pandas numpy matplotlib seaborn scikit-learn joblib jupyter ipykernel
   ```
4. Buka notebook `Arus_Bawah_Final_Data_Science.ipynb` di VS Code, pilih kernel virtual environment, lalu jalankan seluruh cell secara berurutan (**Run All**).
5. Pastikan ketiga CSV berada di root repository atau folder `data/`.

## Batasan dan Pengembangan
- Prediksi didasarkan pada pola historis sehingga perubahan pola permintaan dapat memengaruhi performa.
- Hasil yang dicantumkan menggunakan sampel data pelatihan; evaluasi dengan seluruh data pelatihan dapat dilakukan sebagai pengembangan.
- Linear Regression memiliki keterbatasan dalam menangkap hubungan non-linear yang kompleks.
- Pengembangan berikutnya dapat mencakup validasi beberapa jendela waktu (*time-series cross-validation*), tuning hyperparameter, dan pemantauan performa model.

## Tim
**ARUS BAWAH — Kelompok 64**

Muhammad Fatkhan Kurniadi 123240253
Auron Andrew Aqila 123240236

---
Proyek ini disusun untuk keperluan pembelajaran dan proyek akhir mata kuliah Data Science.
