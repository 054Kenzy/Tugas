<div align="center">

# Analisis Inferensial Kesenjangan Digital Indonesia

**Menguji hubungan statistik antara tingkat kemiskinan dan akses internet antarprovinsi di Indonesia menggunakan pendekatan triangulasi numerik dan kategorikal.**

![Status](https://img.shields.io/badge/status-completed-blue?style=flat-square)
![Python](https://img.shields.io/badge/python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/jupyter-notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Last Commit](https://img.shields.io/github/last-commit/username/idn-digital-divide-inference?style=flat-square)

</div>

## 📌 Overview

Proyek ini merupakan analisis inferensial tingkat lanjut yang mengevaluasi hubungan antara tingkat kemiskinan dan akses internet di 37 provinsi Indonesia tahun 2024. Berfokus pada validitas statistik, analisis ini tidak hanya mengandalkan korelasi numerik, tetapi melakukan triangulasi menggunakan uji independensi kategorikal. Output utama berupa laporan diagnostik lengkap yang mencakup pemodelan regresi linear, uji asumsi klasik, hingga fallback metodologis menggunakan Fisher's Exact Test. Hasil penelitian ini ditujukan untuk analis kebijakan, peneliti sosial, dan praktisi data science yang membutuhkan bukti empiris mengenai kesenjangan digital.

## ❓ Problem Statement

**Konteks:** Kesenjangan digital merupakan hambatan struktural bagi pemerataan ekonomi di Indonesia. Meskipun penetrasi internet meningkat, disparitas antarwilayah masih sangat tinggi, terutama antara wilayah Jawa-Bali dengan kawasan timur Indonesia.

**Gap:** Banyak analisis data sosial hanya berhenti pada perhitungan korelasi permukaan atau visualisasi heatmap tanpa menguji signifikansi statistik secara ketat. Pendekatan ini sering mengabaikan pelanggaran asumsi model dan risiko kesalahan interpretasi pada data agregat.

**Solusi:** Proyek ini menerapkan kerangka inferensial yang ketat. Analisis dimulai dari pemodelan regresi linear sederhana untuk mengukur efek numerik, dilanjutkan dengan uji asumsi klasik. Ketika asumsi Chi-Square dilanggar pada data kategorikal, analisis melakukan fallback ke Fisher's Exact Test. Pendekatan ini memastikan bahwa klaim hubungan antarvariabel didukung oleh bukti statistik yang robust, bukan sekadar kebetulan sampel.

## 🎥 Demo & Screenshots

📓 **Notebook:** [Lihat di nbviewer](https://nbviewer.org/github/username/idn-digital-divide-inference/blob/main/notebooks/01_inferential_analysis_digital_divide.ipynb) | ![Open in Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)

| Distribusi Akses Internet vs Kemiskinan | Peta Korelasi dan Regresi Linear |
| --- | --- |
| ![Scatter Plot](outputs/figures/scatter_regression.png) | ![Crosstab Heatmap](outputs/figures/crosstab_heatmap.png) |
| *Hubungan negatif yang kuat antara persentase kemiskinan dan akses internet, dengan garis regresi dan interval kepercayaan.* | *Matriks kontingensi yang menunjukkan konsentrasi provinsi kemiskinan tinggi pada kategori akses internet rendah.* |

| Diagnostik Asumsi OLS | Fisher's Exact Test (Fallback) |
| --- | --- |
| ![Diagnostic Plots](outputs/figures/diagnostic_plots.png) | ![Fisher Exact](outputs/figures/fisher_exact_2x2.png) |
| *Residual vs Fitted dan Q-Q Plot untuk mengevaluasi validitas asumsi homoskedastisitas dan normalitas.* | *Heatmap tabel 2x2 biner yang membuktikan tidak ada provinsi kemiskinan tinggi dengan akses internet tinggi.* |

## 🛠️ Tech Stack

| Layer | Teknologi | Peran dalam Project |
| --- | --- | --- |
| Language | Python 3.10 | Bahasa utama untuk seluruh pipeline analisis dan inferensi |
| Environment | Jupyter Notebook | Eksekusi interaktif, eksplorasi data, dan pelaporan |
| Data Processing | Pandas, NumPy | Pembersihan data, merging dataset BPS, dan kategorisasi kuartil |
| Visualization | Matplotlib, Seaborn | Visualisasi distribusi, scatter plot, heatmap, dan diagnostik residual |
| Statistical Modeling | SciPy, Scikit-learn | Uji korelasi, regresi linear, Chi-Square, Fisher's Exact, dan uji asumsi |

## 📊 Dataset

### Metadata
| Atribut | Detail |
| --- | --- |
| Sumber | Badan Pusat Statistik (BPS) Indonesia |
| Link | [Dataset Akses Internet](https://www.bps.go.id) & [Dataset Kemiskinan](https://www.bps.go.id) |
| Ukuran | 37 baris × 5 kolom utama (setelah cleaning) |
| Format | CSV |
| Cakupan Waktu | Maret 2024 (Semester 1) |
| Diakses pada | 2024 |

### Data Dictionary (Kolom Kunci)
| Kolom | Tipe Data | Deskripsi | Contoh Nilai |
| --- | --- | --- | --- |
| `Provinsi` | str | Nama provinsi di Indonesia | "JAWA BARAT" |
| `Internet_Total` | float | Persentase rumah tangga dengan akses internet | 88.95 |
| `Kemiskinan_Persen` | float | Persentase penduduk miskin (P0) | 14.23 |
| `Kategori_Internet` | str | Kategorisasi berbasis kuartil (Rendah, Sedang, Tinggi) | "Sedang" |
| `Kategori_Kemiskinan` | str | Kategorisasi berbasis kuartil (Rendah, Sedang, Tinggi) | "Tinggi" |

Data mentah tersimpan di `data/raw/` dan data yang telah digabungkan serta dibersihkan tersimpan di `data/processed/`.

## 📈 Results & Performance

### Performa Model Numerik (Regresi Linear Sederhana)
| Metrik | Nilai | Interpretasi |
| --- | --- | --- |
| R-Squared (R²) | 0.6748 | Model menjelaskan 67.48% variasi akses internet |
| Slope (β₁) | -1.9603 | Setiap kenaikan 1% kemiskinan, akses internet turun 1.96% |
| F-Statistic | 72.6233 | Model signifikan secara statistik (p < 0.001) |
| Pearson's r | -0.8215 | Korelasi negatif yang sangat kuat |

### Performa Model Kategorikal (Uji Independensi)
| Metrik | Nilai | Interpretasi |
| --- | --- | --- |
| Chi-Square (χ²) | 20.1823 | Signifikan (p = 0.00046), namun asumsi expected frequency dilanggar |
| Cramer's V | 0.5222 | Ukuran efek asosiasi kategorikal yang Sangat Kuat |
| Fisher's Exact (p) | 0.0358 | Signifikan (p < 0.05) pada tabel 2x2 biner |
| Odds Ratio | 0.0000 | Tidak ada provinsi dengan kemiskinan tinggi yang memiliki akses internet tinggi |

### Temuan Utama
1. **Dampak Substansial Kemiskinan:** Setiap kenaikan 1% tingkat kemiskinan di suatu provinsi dikaitkan dengan penurunan akses internet sebesar 1.96%. Model regresi mampu menjelaskan hampir 68% varians akses internet hanya dari satu variabel prediktor ini.
2. **Kesenjangan Ekstrem (The Digital Divide):** Uji Fisher's Exact menghasilkan Odds Ratio = 0. Ini adalah bukti empiris yang sangat kuat bahwa pada tahun 2024, tidak ada satupun provinsi dengan kategori kemiskinan "Tinggi" yang mampu mencapai kategori akses internet "Tinggi".
3. **Pencilan Wilayah Papua:** Provinsi-provinsi di wilayah Papua (Papua Pegunungan, Papua Tengah) teridentifikasi sebagai outlier ekstrem baik pada variabel kemiskinan maupun akses internet, yang mendrive sebagian besar varians dan pelanggaran asumsi model.
4. **Triangulasi Metodologis:** Pendekatan numerik (Pearson & Regresi) dan kategorikal (Cramer's V & Fisher) menghasilkan kesimpulan yang konsisten, memvalidasi bahwa hubungan ini bukan artefak dari cara pengelompokan data.

## ⚠️ Notes / Limitations

**Scope:** Analisis ini terbatas pada data agregat tingkat provinsi di Indonesia pada tahun 2024. Temuan tidak serta merta mencerminkan dinamika kesenjangan digital di tingkat kabupaten/kota atau tingkat individu.

**Data:** Data bersifat cross-sectional, sehingga analisis ini hanya dapat mengklaim korelasi dan asosiasi, bukan hubungan kausalitas. Faktor perancu (confounding variables) seperti topografi geografis atau kebijakan infrastruktur lokal tidak dimasukkan dalam model.

**Asumsi Analisis:** Uji asumsi klasik pada model OLS menunjukkan bahwa asumsi normalitas terpenuhi, namun asumsi homoskedastisitas (Uji Breusch-Pagan, p < 0.05) dan autokorelasi (Durbin-Watson = 1.03) dilanggar. Hal ini mengindikasikan bahwa standard error dari koefisien regresi mungkin bias, dan prediksi untuk provinsi dengan karakteristik ekstrem (seperti Papua) memiliki tingkat ketidakpastian yang tinggi.

**Generalisasi:** Karena adanya pelanggaran asumsi homoskedastisitas dan keberadaan outlier spasial, model regresi ini sebaiknya tidak digunakan untuk memprediksi akses internet di luar sampel provinsi yang diamati tanpa penyesuaian robust standard errors atau pemodelan spasial.

<div align="center">
<sub>
⭐ Jika analisis ini bermanfaat, pertimbangkan untuk memberikan star!
<br>
Made with ❤️ by <a href="https://github.com/username">[Nama Anda]</a> · 2024-06
</sub>
</div>
