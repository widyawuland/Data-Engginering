# Data-Engginering-Kelompok-4

# Proyek : Dampak Fluktuasi Nilai Tukar terhadap Kinerja Ekspor dan Impor Indonesia

## Deskripsi Proyek
Proyek ini bertujuan untuk menganalisis dampak dari fluktuasi nilai tukar Rupiah terhadap kinerja ekspor dan impor Indonesia. Fokus utama adalah memahami keterkaitan antara perubahan nilai tukar terhadap volume perdagangan internasional Indonesia. Proyek ini mencakup proses ETL (Extract, Transform, Load) untuk integrasi data ekspor, impor, dan kurs Rupiah terhadap USD dalam periode 2020–2024.

## Manfaat Data / Use Case
- **Tujuan Proyek**:
  Membangun pipeline data yang mengintegrasikan data ekspor, impor, dan kurs rupiah, lalu melakukan analisis keterkaitannya melalui visualisasi dan model prediksi.
  
- **Manfaat**:
  - Menyediakan dataset yang bersih, terstruktur, dan siap analisis dari berbagai sumber ekonomi makro.
  - Mendukung pengambilan keputusan berbasis data oleh regulator dan pelaku ekspor-impor.
  - Menjadi landasan awal untuk sistem prediksi berbasis machine learning.
  - Memberikan wawasan tentang pengaruh kurs terhadap ekspor dan impor Indonesia.

## Serving Analisis
Data hasil ETL disimpan dalam format CSV yang telah dibersihkan dan distandardisasi, kemudian dimasukkan ke dalam PostgreSQL. Data ini dianalisis menggunakan visualisasi korelasi dan evaluasi model, serta dapat digunakan untuk dashboard interaktif di tools BI.

## Serving Machine Learning
Data gabungan kurs dan nilai ekspor-impor digunakan untuk membangun model supervised learning menggunakan algoritma Linear Regression dan Random Forest Regressor. Tujuannya adalah untuk:
- Mengukur kekuatan prediktif kurs terhadap ekspor dan impor.
- Menilai seberapa besar kontribusi kurs beli dan jual dalam menjelaskan variasi nilai perdagangan.
- Memprediksi nilai ekspor dan impor pada kondisi kurs tertentu.

# Pipeline

## Extract (Pengambilan Data)
- **Sumber Data:**
  - Ekspor Non-Migas Indonesia – [Kemendag RI](https://satudata.kemendag.go.id/data-informasi/perdagangan-luar-negeri/ekspor-non-migas-komoditi)
  - Impor Non-Migas Indonesia – [Kemendag RI](https://satudata.kemendag.go.id/data-informasi/perdagangan-luar-negeri/impor-non-migas-komoditi)
  - Kurs Rupiah terhadap USD – [Ortax/BI](https://datacenter.ortax.org/ortax/kursbi/show/USD?rentang_tanggal=2020-01-01,2024-12-31&show=USD)

- **Metode Pengambilan:**
  - Web Scraping menggunakan `pandas.read_html()` dan `requests`.
  - Data kurs diambil harian, sedangkan ekspor dan impor bersifat tahunan.

## Transform (Pembersihan & Transformasi)
- **Pembersihan:**
  - Menghapus data duplikat dan nilai kosong menggunakan `drop_duplicates()` dan `dropna()`.
  - Penyeragaman nama kolom (`rename()`).

- **Transformasi:**
  - Data kurs dikonversi menjadi rata-rata tahunan (`groupby`).
  - Filter tahun 2020–2024.
  - Penggabungan dataset berdasarkan kolom "Tahun".
  - Disimpan kembali sebagai CSV.

## Load (Pemindahan ke Target)
- **Target:**
  - File CSV bersih yang diunggah ke database PostgreSQL (Aiven Cloud) untuk keperluan eksplorasi lanjutan dan visualisasi.

- **Metode:**
  - Menggunakan `pandas.to_sql()` untuk menyimpan ke PostgreSQL dan `pd.read_sql()` untuk verifikasi.

## Arsitektur / Workflow ETL
- **Alur Modular:**
  - ETL dirancang modular menggunakan fungsi Python.
  - Disusun urut di Google Colab mulai dari scraping, cleaning, merging, hingga load ke database.

- **Tools yang Digunakan:**
  - Python 3.x
  - Library: `pandas`, `numpy`, `requests`, `matplotlib`, `seaborn`, `scikit-learn`
  - Jupyter/Google Colab sebagai environment utama

## Kode Program
- **Struktur Kode:**
  - Tersusun rapi per bagian: ETL, EDA, Visualisasi, Modeling
  - Penamaan variabel deskriptif, data pipeline terotomatisasi

- **Machine Learning:**
  - Dua model: `LinearRegression()` dan `RandomForestRegressor()`
  - Evaluasi performa menggunakan `r2_score`, `mean_squared_error`, dan `feature_importance_`
  - Visualisasi hasil dan prediksi regresi disiapkan dengan matplotlib/seaborn

- **Link Projek:**
  - ETL Pipeline: https://github.com/widyawuland/Data-Engginering/blob/main/Project/TeamProjek4.ipynb
  - Mechine Learning: https://github.com/widyawuland/Data-Engginering/blob/main/Project/Machine_Learning.ipynb
  - Visualisasi: https://github.com/widyawuland/Data-Engginering/blob/main/Project/Visualisasi.pbix

## Kontributor
| Nama Lengkap         | NIM         | Peran           |
|----------------------|-------------|-----------------|
| Widya Wulandari      | 234311056   | Data Engineer   |
| Veri Tri Anggoro     | 234311055   | Data Analyst    |
| Ikbal Dzakwan        | 234311043   | Data Analyst    |
| Dzaki Anwar Zulfahmi | 234311037   | Project Manager |
