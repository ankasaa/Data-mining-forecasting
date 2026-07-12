# 🏍️ Sistem Peramalan Jumlah Penyewaan Motor

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)

## 📋 Daftar Isi
- [Tentang Proyek](#-tentang-proyek)
- [Fitur](#-fitur)
- [Dataset](#-dataset)
- [Metodologi](#-metodologi)
- [Hasil dan Evaluasi](#-hasil-dan-evaluasi)
- [Cara Penggunaan](#-cara-penggunaan)
- [Output yang Dihasilkan](#-output-yang-dihasilkan)
- [Kontribusi](#-kontribusi)

## 📌 Tentang Proyek

Proyek ini merupakan tugas akhir mata kuliah **Data Mining** yang bertujuan untuk mengembangkan sistem peramalan (forecasting) jumlah penyewaan motor menggunakan berbagai metode time series dan machine learning. Sistem ini dirancang untuk membantu perusahaan penyewaan motor dalam memprediksi permintaan di masa depan sehingga dapat mengoptimalkan manajemen inventaris dan sumber daya.

### Tujuan Proyek
- Menganalisis pola penyewaan motor berdasarkan data historis
- Mengimplementasikan berbagai metode forecasting (ARIMA, SARIMA, Exponential Smoothing, Prophet, Random Forest)
- Membandingkan performa setiap model menggunakan metrik evaluasi yang tepat
- Memilih model terbaik untuk implementasi
- Melakukan peramalan untuk 12 bulan ke depan


**Mata Kuliah:** Data Analytics - I
**Tahun:** 2025

## ✨ Fitur

- ✅ **Preprocessing Data**: Pembersihan dan transformasi data
- ✅ **Analisis Stasioneritas**: Uji Dickey-Fuller (ADF) untuk menguji stasioneritas data
- ✅ **Differencing**: Transformasi data untuk mencapai stasioneritas
- ✅ **Multi-Model Forecasting**: Implementasi 5 model berbeda
- ✅ **Evaluasi Komprehensif**: Perhitungan MAE, MSE, RMSE, dan MAPE
- ✅ **Analisis Residual**: Pemeriksaan white noise dan normalitas residual
- ✅ **Visualisasi**: Grafik interaktif untuk analisis data dan hasil forecasting
- ✅ **Forecasting**: Prediksi untuk 12 periode ke depan
- ✅ **Export Results**: Penyimpanan hasil dalam format CSV

## 📊 Dataset

Dataset yang digunakan dalam proyek ini adalah **Data Penyewaan Motor** yang berisi informasi penyewaan dari Januari 2019 hingga Desember 2024.

### Struktur Dataset

| Kolom | Deskripsi | Tipe Data |
|-------|-----------|-----------|
| Tanggal | Tanggal penyewaan | Date |
| Jenis_Motor | Tipe motor yang disewa | String |
| Unit_Tersedia | Jumlah unit yang tersedia | Integer |
| Hari_Libur | Indikator hari libur (Ya/Tidak) | String |
| Promo | Indikator ada promo (Ya/Tidak) | String |
| Jumlah_Penyewaan | Total penyewaan pada tanggal tersebut | Integer |

### Statistik Dataset
- **Total Data**: 288 records (bulanan)
- **Periode**: Januari 2019 - Desember 2024 (72 bulan untuk analisis agregat)
- **Variabel Target**: Jumlah_Penyewaan
- **Frekuensi**: Bulanan (Monthly)

## 🔬 Metodologi

### 1. Pengumpulan Data
Data dikumpulkan dari sistem pencatatan penyewaan motor dan diagregasi menjadi data bulanan.

### 2. Preprocessing Data
- **Handling Missing Values**: Pengecekan dan penanganan data yang hilang
- **Agregasi**: Penggabungan data harian menjadi bulanan
- **Transformasi**: Konversi tipe data dan normalisasi jika diperlukan

### 3. Analisis Stasioneritas
Menggunakan **Augmented Dickey-Fuller (ADF) Test** untuk menguji stasioneritas data time series:
- **Hipotesis Null (H0)**: Data tidak stasioner
- **Hipotesis Alternatif (H1)**: Data stasioner
- Jika p-value > 0.05, dilakukan differencing

### 4. Pembagian Data
- **Training Set**: 80% data (57 bulan)
- **Testing Set**: 20% data (15 bulan)

### 5. Pemodelan
Implementasi 5 model forecasting:
1. Auto ARIMA
2. SARIMA
3. Exponential Smoothing (Holt-Winters)
4. Prophet (Facebook)
5. Random Forest Regressor

### 6. Evaluasi Model
Menggunakan metrik:
- **MAE** (Mean Absolute Error)
- **MSE** (Mean Squared Error)
- **RMSE** (Root Mean Squared Error)
- **MAPE** (Mean Absolute Percentage Error)

### 7. Analisis Residual
- Uji Ljung-Box untuk white noise
- Plot histogram untuk normalitas
- Plot residual vs waktu

##  Model yang Digunakan

### 1. Auto ARIMA
Automatic ARIMA yang secara otomatis mencari parameter (p,d,q) dan (P,D,Q,m) terbaik berdasarkan nilai AIC (Akaike Information Criterion).

**Keunggulan:**
- Otomatis menentukan parameter optimal
- Tidak perlu trial and error manual

### 2. SARIMA (Seasonal ARIMA)
Model ARIMA dengan komponen musiman untuk menangani pola musiman dalam data.

**Parameter:**
- Order: (p, d, q) - komponen non-musiman
- Seasonal Order: (P, D, Q, m) - komponen musiman
- m = 12 (data bulanan)

### 3. Exponential Smoothing (Holt-Winters)
Metode smoothing yang mempertimbangkan trend dan musiman.

**Komponen:**
- Level (α)
- Trend (β)
- Seasonal (γ)

### 4. Prophet
Model forecasting yang dikembangkan oleh Facebook, cocok untuk data dengan pola musiman yang kuat.

**Fitur:**
- Menangani missing values dengan baik
- Robust terhadap outliers
- Fleksibel dalam menangani musiman

### 5. Random Forest Regressor
Ensemble learning method yang menggunakan multiple decision trees.

**Feature Engineering:**
- year, month, quarter
- month_sin, month_cos (cyclical features)
- lag_1, lag_2, lag_3, lag_6, lag_12

## 📈 Hasil dan Evaluasi

### Perbandingan Performa Model

| Model | MAE | MSE | RMSE | MAPE (%) |
|-------|-----|-----|------|----------|
| **SARIMA** | **28.13** | **1582.00** | **39.77** | **4.08** |
| Auto ARIMA | 55.60 | 4995.38 | 70.68 | 7.54 |
| Exponential Smoothing | 74.04 | 9852.67 | 99.26 | 9.68 |
| Random Forest | 87.68 | 13189.77 | 114.85 | 11.88 |
| Prophet | 137.86 | 23933.77 | 154.71 | 23.46 |

### 🏆 Model Terbaik: **SARIMA**

**Parameter Optimal:**
- Order: (0, 1, 0)
- Seasonal Order: (0, 1, 1, 12)
- AIC: 552.236

**Alasan Pemilihan:**
1. RMSE terendah (39.77)
2. MAPE terendah (4.08%) - akurasi ~96%
3. Mampu menangkap pola musiman dengan baik
4. Residual bersifat white noise (tidak ada autokorelasi)

### Analisis Residual Model SARIMA
- ✅ Residual berdistribusi normal
- ✅ Tidak ada autokorelasi (Ljung-Box test p-value > 0.05)
- ✅ Varians konstan (homoskedastisitas)
- ✅ Mean residual mendekati nol

## ️ Instalasi

### Prasyarat
- Python 3.8 atau lebih tinggi
- pip (Python Package Manager)

### Langkah Instalasi

1. **Clone repository ini:**
```bash
git clone https://github.com/username/forecasting-penyewaan-motor.git
cd forecasting-penyewaan-motor
```

2. **Buat virtual environment (direkomendasikan):**
```bash
# Untuk Windows
python -m venv venv
venv\Scripts\activate

# Untuk Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

Atau install manual:
```bash
pip install pandas numpy matplotlib seaborn
pip install statsmodels pmdarima prophet
pip install scikit-learn
pip install jupyter
```

### File requirements.txt
```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
statsmodels>=0.12.0
pmdarima>=1.8.0
prophet>=1.0.0
scikit-learn>=0.24.0
jupyter>=1.0.0
```

## 📖 Cara Penggunaan

### 1. Persiapan Data

Pastikan file dataset berada di direktori yang sesuai:
```
Data Penyewaan Motor Rapih - Data Penyewaan Motor Rapih.csv
```

Atau ubah path file di notebook:
```python
file_path = 'path/ke/file/dataset.csv'
```

### 2. Menjalankan Notebook

**Menggunakan Jupyter Notebook:**
```bash
jupyter notebook UAS-Data-Mining.ipynb
```

**Menggunakan JupyterLab:**
```bash
jupyter lab UAS-Data-Mining.ipynb
```

**Menggunakan Google Colab:**
1. Upload file `UAS-Data-Mining.ipynb` ke Google Drive
2. Buka dengan Google Colab
3. Upload dataset ke Colab atau mount Google Drive

### 3. Eksekusi Kode

Jalankan setiap cell secara berurutan:
1. **Installation & Import** - Install dan import library
2. **Load Dataset** - Memuat dan mengeksplorasi data
3. **Data Preprocessing** - Agregasi dan cleaning data
4. **Stationarity Test** - Uji stasioneritas ADF
5. **Data Splitting** - Pembagian train-test data
6. **Modeling** - Training 5 model forecasting
7. **Evaluation** - Evaluasi dan perbandingan model
8. **Residual Analysis** - Analisis residual model terbaik
9. **Forecasting** - Peramalan 12 bulan ke depan
10. **Export Results** - Menyimpan hasil ke CSV

### 4. Interpretasi Hasil

Setelah menjalankan semua cell, Anda akan mendapatkan:
- Visualisasi data dan pola musiman
- Hasil uji stasioneritas
- Perbandingan performa 5 model
- Analisis residual model terbaik
- Forecast untuk 12 periode ke depan
- File CSV dengan hasil lengkap

##  Struktur Folder

```
forecasting-penyewaan-motor/
│
├── README.md                           # Dokumentasi proyek
├── requirements.txt                    # Dependencies
├── UAS-Data-Mining.ipynb              # Jupyter notebook utama
│
├── data/
│   └── Data Penyewaan Motor Rapih.csv  # Dataset asli
│
├── output/
│   ├── data_agregasi_bulanan.csv       # Data agregasi bulanan
│   ├── hasil_evaluasi_model.csv        # Hasil evaluasi semua model
│   ├── analisis_residual.csv           # Analisis residual
│   ├── model_terbaik.csv               # Parameter model terbaik
│   ├── forecast_12_bulan.csv           # Hasil forecast 12 bulan
│   └── deployment_prediction.csv       # Format untuk deployment
│
└── images/
    ├── data_visualization.png          # Visualisasi data
    ├── model_comparison.png            # Perbandingan model
    ├── residual_analysis.png           # Analisis residual
    └── forecast_result.png             # Hasil forecast
```

## 📤 Output yang Dihasilkan

Proyek ini menghasilkan 6 file CSV:

### 1. data_agregasi_bulanan.csv
Data yang telah diagregasi per bulan dengan kolom:
- ds (tanggal)
- y (jumlah penyewaan)

### 2. hasil_evaluasi_model.csv
Perbandingan metrik evaluasi untuk semua model:
- Model name
- MAE, MSE, RMSE, MAPE

### 3. analisis_residual.csv
Detail residual model terbaik:
- Tanggal
- Nilai Aktual
- Nilai Prediksi
- Residual

### 4. model_terbaik.csv
Parameter model terbaik:
- Nama model
- RMSE
- Order (p,d,q)
- Seasonal Order (P,D,Q,m)

### 5. forecast_12_bulan.csv
Hasil peramalan 12 bulan ke depan:
- Tanggal
- Prediksi Penyewaan

### 6. deployment_prediction.csv
Format siap deployment dengan:
- ds
- yhat (prediksi)
- yhat_lower (batas bawah confidence interval)
- yhat_upper (batas atas confidence interval)

## 🔧 Troubleshooting

### Error: "ModuleNotFoundError"
**Solusi:** Pastikan semua dependencies sudah terinstall
```bash
pip install -r requirements.txt
```

### Error: "FileNotFoundError"
**Solusi:** Periksa path file dataset
```python
# Gunakan absolute path atau relative path yang benar
file_path = '/content/Data Penyewaan Motor Rapih.csv'  # Untuk Colab
# atau
file_path = './data/dataset.csv'  # Untuk lokal
```

### Error: "Singular Matrix" pada SARIMA
**Solusi:** Model sudah dihandle dengan parameter:
```python
enforce_stationarity=False
enforce_invertibility=False
```

### Warning: Convergence
**Solusi:** Warning ini normal untuk beberapa model. Hasil tetap valid.

## 🤝 Kontribusi

Kontribusi sangat diterima! Untuk berkontribusi:

1. Fork repository ini
2. Buat branch fitur (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buka Pull Request

### Guidelines Kontribusi:
- Gunakan PEP 8 style guide untuk Python
- Tambahkan komentar pada kode yang kompleks
- Update dokumentasi jika ada perubahan signifikan
- Test kode sebelum submit


##  Ucapan Terima Kasih

Terima kasih kepada:
- Dosen mata kuliah Data Analytics - I atas bimbingannya
- Semua pihak yang telah membantu dalam penyelesaian proyek ini

---
-Andika
