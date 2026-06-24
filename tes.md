<div align="center">

# Indonesia Digital Divide Analytics

### Mengidentifikasi pola kesenjangan digital regional menggunakan uji statistika komplementer untuk mengevaluasi dampak kemiskinan terhadap akses internet rumah tangga.

<br>

[![Status](https://img.shields.io/badge/status-completed-blue?style=flat-square)]()
[![Python](https://img.shields.io/badge/python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/jupyter-notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](notebooks/)

</div>

---

## 📌 Overview

Analisis ini bertujuan untuk memetakan dan mengukur derajat kesenjangan digital (digital divide) antarprovinsi di Indonesia pada tahun 2024. Melalui integrasi data makroekonomi dan sosio-digital dari Badan Pusat Statistik (BPS), proyek ini secara spesifik meneliti bagaimana tingkat kemiskinan daerah memengaruhi batas penetrasi akses internet rumah tangga. Studi ini dirancang sebagai studi kasus teknis bagi pembuat kebijakan publik, ekonom, dan praktisi data untuk memahami hambatan struktural inklusi digital. Output akhir dari proyek ini berupa kerangka analisis statistik replikabel yang menggabungkan permodelan linear numerik OLS dan pengujian asosiasi kategorik non-parametrik.

---

## ❓ Problem Statement

**Konteks:** Transformasi digital di Indonesia berkembang pesat, namun laju penetrasinya tidak merata di seluruh wilayah kedaulatan ekonomi. Berdasarkan agregat sektoral nasional, terdapat variasi ekstrem di mana persentase rumah tangga yang mengakses internet berkisar antara 12.15% hingga 97.57%, sementara tingkat kemiskinan regional berfluktuasi dari 4.00% hingga 32.97%.

**Gap:** Pendekatan evaluasi inklusi digital sering kali hanya melihat metrik deskriptif rata-rata tanpa menguji kekuatan hubungan struktural antar-variabel. Belum ada pembuktian kuantitatif yang menguji apakah kemiskinan bertindak sebagai pembatas mutlak dalam kepemilikan akses internet, atau sejauh mana pengelompokan wilayah miskin secara signifikan terperangkap dalam klaster isolasi digital.

**Solusi:** Proyek ini menerapkan pendekatan statistik komplementer menggunakan Ordinary Least Squares (OLS) Linear Regression untuk mengukur nilai elastisitas dampak numerik, serta Uji Chi-Square dan Fisher's Exact Test untuk membedah struktur kontingensi wilayah. Analisis ini memberikan basis bukti kuantitatif untuk memprioritaskan intervensi infrastruktur digital pada area yang memiliki kontribusi deviasi tertinggi.

---

## 🎥 Demo & Screenshots

> 📓 **Notebook:** &nbsp;[[Lihat Dokumentasi Notebook](notebooks/indonesia_digital_divide_eda.ipynb)]

<br>

| Hubungan Linier Tren Kemiskinan vs Internet | Permodelan Matriks Diagnostik Residual OLS |
|:---:|:---:|
| [Placeholder: Tempatkan Grafik scatter_plot dengan regression_line dari docs/img/correlation_trendline.png] | [Placeholder: Tempatkan Grafik 2x2 subplot OLS_diagnostic_plots dari docs/img/OLS_diagnostic_plots.png] |
| *Hubungan negatif yang kuat antara kemiskinan daerah dengan tingkat penetrasi internet tahun 2024.* | *Evaluasi visual untuk uji asumsi normalitas histogram, Q-Q plot, dan Scale-Location.* |

<br>

| Distribusi Klaster Kategori Variabel | Frekuensi Observasi vs Ekspektasi Kontingensi |
|:---:|:---:|
| [Placeholder: Tempatkan Grafik pie_charts distribusi kategori dari docs/img/contingency_pie_charts.png] | [Placeholder: Matriks visualisasi tabel kontingensi 2x2 atau barchart dari Fisher's Exact Test] |
| *Proporsi pembagian klaster wilayah berdasarkan kuartil Q25 dan Q75.* | *Visualisasi kesenjangan mutlak: Nol provinsi di kategori kemiskinan tinggi yang menembus akses internet tinggi.* |

---

## 🛠️ Tech Stack

| Layer | Teknologi | Peran dalam Project |
|:---:|:---:|---|
| Language | Python 3.10 | Bahasa pemrograman utama untuk membangun seluruh pipeline pemrosesan data dan komputasi statistik. |
| Environment | Jupyter Notebook | Media eksekusi interaktif, visualisasi terintegrasi, dan penyusunan narasi laporan analitis. |
| Data Processing | Pandas, NumPy | Melakukan ingestion data BPS, standarisasi nama wilayah, penyelarasan baris data, dan penanganan nilai pencilan (outliers). |
| Visualization | Matplotlib, Seaborn | Membangun visualisasi statistik formal termasuk scatter plot dengan trendline, matriks diagnosa, dan diagram distribusi. |
| ML / Modeling | Scikit-learn, Scipy Stats | Melakukan fitting regresi linear OLS, komputasi skor R-squared, uji signifikansi F-test/t-test, serta eksekusi uji non-parametrik Chi-Square. |
| Version Control | Git + GitHub | Melakukan pelacakan perubahan kode secara berkala dan manajemen dokumentasi artefak repositori. |

---

## 📊 Dataset

### Metadata

| Atribut | Detail |
|---|---|
| **Sumber** | Badan Pusat Statistik (BPS) Republik Indonesia |
| **Link** | [Dataset Akses Internet 2024](https://www.bps.go.id/id/statistics-table/2/Mzk4IzI=/persentase-rumah-tangga-yang-pernah-mengakses-internet-dalam-3-bulan-terakhir-menurut-provinsi-dan-klasifikasi-daerah.html) \| [Dataset Kemiskinan P0 2024](https://www.bps.go.id/id/statistics-table/2/MTkyIzI=/persentase-penduduk-miskin--p0--menurut-provinsi-dan-daerah.htmlh) |
| **Ukuran** | 37 baris × 5 kolom (Setelah pembersihan data pencilan dan baris agregat nasional) |
| **Format** | CSV (Comma-Separated Values) |
| **Lisensi** | Open Data BPS / Public Domain |
| **Cakupan Waktu** | Tahun Kalender 2024 (Temporal Match: Internet 3 Bulan Terakhir & Kemiskinan Semester 1 Maret) |
| **Diakses pada** | 2026-06-24 |

### Data Dictionary (Kolom Kunci)

| Kolom | Tipe Data | Deskripsi | Contoh Nilai |
|---|:---:|---|---|
| `Provinsi` | `str` | Nama entitas wilayah administratif tingkat satu di Indonesia (dibersihkan dan dikonversi ke huruf kapital). | `"ACEH"`, `"SUMATERA UTARA"` |
| `Internet_Total` | `float` | **Variabel Dependen (Y)**: Persentase total rumah tangga di provinsi tersebut yang mengakses internet. | `88.95` |
| `Kemiskinan_Persen` | `float` | **Variabel Independen (X)**: Persentase total penduduk miskin (indeks P0) berdasarkan survei bulan Maret. | `14.23` |
| `Kategori_Kemiskinan`| `str` | Klasifikasi wilayah berdasarkan nilai kuartil data kemiskinan daerah. | `"Rendah"`, `"Sedang"`, `"Tinggi"` |
| `Kategori_Internet`  | `str` | Klasifikasi wilayah berdasarkan nilai kuartil data penetrasi internet daerah. | `"Rendah"`, `"Sedang"`, `"Tinggi"` |

> Data mentah disimpan pada direktori `data/raw/` dan dataset hasil transformasi akhir disimpan di `data/processed/`.

---

## 📈 Results & Performance

### Performa Model Regresi Linear

| Metrik | Model Utama OLS | Baseline | Delta vs Baseline |
|---|:---:|:---:|:---:|
| Accuracy (R² Score) | 0.6748 (67.48%) | 0.0000 | +67.48% |
| F-Statistic | 72.6233 (p-value = 0.000000) | — | — |
| t-Statistic (Slope) | -8.5219 (p-value = 0.000000) | — | — |
| Intercept (β₀) | 108.1643 | — | — |
| Slope Koefisien (β₁) | -1.9603 | — | — |

### Temuan Utama

1. **Hubungan Terbalik yang Signifikan secara Statistik:** Pemodelan regresi membuktikan adanya korelasi negatif yang sangat kuat antara tingkat kemiskinan dan akses internet dengan nilai Pearson $r = -0.8215$. Persamaan regresi $\hat{Y} = 108.16 - 1.9603X$ menunjukkan setiap kenaikan tingkat kemiskinan sebesar 1% di suatu provinsi berkorelasi langsung dengan penurunan akses internet rumah tangga sebesar 1.96%.
2. **Daya Penjelas Model yang Kuat:** Nilai Koefisien Determinasi ($R^2 = 0.6748$) menandakan bahwa 67.48% variabilitas penetrasi internet antar-provinsi di Indonesia dapat dijelaskan secara linier oleh variabel kemiskinan tunggal. Sisa sebesar 32.52% variansi dipengaruhi oleh faktor eksternal di luar model penelitian.
3. **Kesenjangan Struktural Ekstrem:** Pengujian Chi-Square ($20.1823, p = 0.000460$) dan Fisher's Exact Test ($p = 0.035853$) mengonfirmasi adanya dependensi kategoris yang kuat dengan nilai Cramer's V sebesar 0.5222 (Kategori Sangat Kuat).
4. **Analisis Deviasi Matriks Kontingensi:** Sel `[Kemiskinan Tinggi × Internet Rendah]` memberikan kontribusi terbesar terhadap nilai total Chi-Square yaitu sebesar 42.50% dengan Standardized Residual positif yang masif (+2.929). Secara riil terdapat 7 provinsi yang berada di klaster ini dibandingkan nilai ekspektasi teoritis yang hanya sebesar 2.4 provinsi.
5. **Ketiadaan Anomali Klaster Atas:** Ditemukan fenomena batas mutlak di mana frekuensi pada sel `[Kemiskinan Tinggi × Internet Tinggi]` bernilai 0. Ini memberikan bukti empiris berharga bagi pengambil kebijakan bahwa tidak ada satu pun daerah dengan tingkat kemiskinan tinggi di Indonesia yang mampu mencapai tingkat penetrasi internet kategori tinggi secara organik tanpa intervensi eksternal khusus.

> 📂 Seluruh hasil penghitungan numerik lengkap diekspor secara otomatis ke dalam berkas direktori `results/ringkasan_analisis_statistika.txt`.

---

## ⚠️ Notes / Limitations

- **Scope:** Ruang lingkup analisis ini terbatas pada agregasi data tingkat provinsi di Indonesia untuk tahun kalender 2024. Hasil temuan mencerminkan pola spasial makro-wilayah dan tidak dapat diasumsikan secara langsung merepresentasikan perilaku unit rumah tangga individual secara mikro (potensi *Ecological Fallacy*).
- **Data:** Dataset yang bersumber dari BPS memiliki karakteristik spasial yang terbatas pada 38 provinsi administratif asal, yang kemudian disaring menjadi 37 entitas setelah pembersihan pencilan. Keterbatasan jumlah sampel ($n = 37$) berpotensi memengaruhi sensitivitas pengujian parameter tertentu pada pengujian sub-grup terkecil.
- **Asumsi Analisis:** Berdasarkan hasil Uji Asumsi Klasik OLS, residual model terbukti berdistribusi normal (Shapiro-Wilk $p = 0.092 > 0.05$). Namun, ditemukan pelanggaran serius pada asumsi Homoskedastisitas melalui Breusch-Pagan Test ($LM = 20.4326, p = 0.000006 < 0.05$). Hal ini menandakan terjadinya variansi residual yang tidak konstan (Heteroskedastisitas) akibat sebaran variansi yang melebar pada tingkat kemiskinan ekstrem.
- **Generalisasi:** Temuan pemodelan linier sederhana ini hanya mencakup deteksi pola korelasi dan asosiasi statis pada titik waktu tertentu. Hasil analisis belum divalidasi silang menggunakan data longitudinal (panel data) untuk tahun-tahun sebelumnya atau sesudahnya, sehingga klaim kausalitas mutlak yang bersifat dinamis memerlukan penelitian eksternal lebih lanjut.

<div align="center">
  <sub>
    ⭐ Jika analisis ini bermanfaat, pertimbangkan untuk memberikan star!
    <br>
    Made with ❤️ by Student Portofolio Portfolio Analytics · 2026-06
  </sub>
</div>
