<div align="center">

# Analisis Kesenjangan Digital Indonesia per Provinsi

### Studi statistik yang dapat direproduksi tentang hubungan antara akses internet dan tingkat kemiskinan di provinsi-provinsi Indonesia pada 2024

</div>

---

## 📌 Gambaran Umum

Repository ini berisi analisis statistik berbasis notebook mengenai hubungan antara akses internet dan tingkat kemiskinan di tingkat provinsi di Indonesia pada tahun 2024. Alur kerja mencakup pengambilan data, pembersihan, penggabungan dua tabel BPS, eksplorasi data, korelasi Pearson, regresi linear, uji chi-square, Fisher's exact test, serta analisis residual.

Proyek ini dirancang sebagai aset portofolio teknis yang menunjukkan kemampuan dalam data cleaning, validasi statistik, dan penyajian hasil yang transparan. Fokus utamanya adalah keterlacakan proses analisis dan kekuatan bukti, bukan deployment atau aplikasi interaktif.

---

## ❓ Pernyataan Masalah

**Konteks:**  
Data BPS menyediakan informasi terpisah tentang akses internet dan tingkat kemiskinan per provinsi, tetapi tabel mentah tersebut belum menjawab apakah kedua variabel ini bergerak bersama, seberapa kuat hubungannya, dan apakah pola tersebut tetap terlihat ketika dilihat dari sudut pandang numerik maupun kategorik.

**Kesenjangan:**  
Sekadar membaca tabel tidak cukup untuk keperluan portofolio teknis. Yang dibutuhkan adalah workflow statistik yang bisa dilacak, membersihkan data dengan konsisten, menyelaraskan unit analisis per provinsi, dan memvalidasi hubungan dengan lebih dari satu metode.

**Solusi:**  
Repository ini menggabungkan dua tabel BPS pada level provinsi, melakukan cleaning dan pemeriksaan kualitas data, lalu menguji hubungan antarbvariabel melalui korelasi, regresi linear, chi-square, Fisher's exact test, dan interpretasi residual. Hasilnya adalah studi hubungan yang ringkas tetapi berbasis bukti tentang kesenjangan digital antarprovinsi di Indonesia.

---

## 🎥 Demo & Screenshot

Visual di bawah sebaiknya diekspor dari notebook dan disimpan di `docs/img/`.

| Cuplikan Audit Data | Plot Regresi |
|:---:|:---:|
| ![Cuplikan audit data](docs/img/01_data_audit_snapshot.png) | ![Plot regresi](docs/img/02_regression_scatter.png) |
| Preview data bersih, penanganan missing value, dan jumlah provinsi final. | Scatter plot dengan garis regresi, persamaan, dan anotasi R². |

| Diagnostik Chi-Square | Ringkasan Fisher 2×2 |
|:---:|:---:|
| ![Diagnostik chi-square](docs/img/03_chi_square_diagnostics.png) | ![Ringkasan Fisher](docs/img/04_fisher_2x2_summary.png) |
| Observed, expected, dan standardized residual untuk tabel kontingensi. | Tabel 2×2 yang dipakai untuk Fisher's exact test. |

---

## 🛠️ Tech Stack

| Layer | Teknologi | Peran dalam Proyek |
|:---:|:---:|---|
| Language | Python 3 | Bahasa utama seluruh workflow analisis |
| Environment | Jupyter Notebook | Eksekusi interaktif, eksplorasi, dan pelaporan |
| Data Processing | Pandas, NumPy | Cleaning, transformasi, merging, dan tabulasi |
| Visualization | Matplotlib, Seaborn | Visualisasi distribusi, scatter plot, heatmap, dan diagnostik |
| Statistik / Modeling | SciPy, Scikit-learn | Korelasi, regresi, chi-square, dan uji asumsi |
| Version Control | Git + GitHub | Manajemen repo dan penyajian portofolio |

---

## 📊 Dataset

### Metadata

| Atribut | Detail |
|---|---|
| **Sumber** | Tabel statistik publik BPS |
| **Link** | Dicatat di notebook sumber |
| **Ukuran** | Raw: 39 × 4 dan 39 × 10; Final merged dataset: 37 × 5 |
| **Format** | CSV |
| **Lisensi** | Data publik; lisensi code dapat ditambahkan terpisah |
| **Cakupan Waktu** | 2024 |
| **Diakses pada** | Tidak dicantumkan di export notebook |

### Data Dictionary (Kolom Kunci)

| Kolom | Tipe Data | Deskripsi | Contoh Nilai |
|---|:---:|---|---|
| `Provinsi` | `str` | Nama provinsi, dipakai sebagai kunci merge | `ACEH` |
| `Internet_Perkotaan` | `float` | Persentase rumah tangga di wilayah perkotaan yang pernah mengakses internet dalam 3 bulan terakhir | `92.60` |
| `Internet_Perdesaan` | `float` | Persentase rumah tangga di wilayah perdesaan yang pernah mengakses internet dalam 3 bulan terakhir | `86.97` |
| `Internet_Total` | `float` | Persentase akses internet total per provinsi | `88.95` |
| `Kemiskinan_Persen` | `float` | Persentase penduduk miskin per provinsi | `14.23` |

> Data mentah disimpan di `data/raw/` dan data hasil pembersihan disimpan di `data/processed/`.

---

## 📈 Hasil & Temuan Utama

1. **Dataset final berisi 37 provinsi dan 5 variabel.**  
   Setelah merge dua tabel dan penanganan missing value, satu baris dihapus karena nilai `Internet_Perdesaan` untuk DKI Jakarta tidak tersedia. Dataset final tetap konsisten untuk analisis lanjutan.

2. **Akses internet dan kemiskinan menunjukkan hubungan linear negatif yang sangat kuat.**  
   Korelasi Pearson bernilai `r = -0.8215` dengan `p-value < 0.001`, yang berarti provinsi dengan tingkat kemiskinan lebih tinggi cenderung memiliki tingkat akses internet yang lebih rendah.

3. **Model regresi menjelaskan sebagian besar variasi akses internet.**  
   Persamaan regresi yang diperoleh adalah `Y = 108.1643 + (-1.9603)X`, dengan `R² = 0.6748` dan `Adjusted R² = 0.6655`. Secara praktis, kenaikan 1% tingkat kemiskinan dikaitkan dengan penurunan sekitar `1.9603%` akses internet pada data ini.

4. **Uji asumsi regresi tidak sepenuhnya bersih, sehingga model perlu dibaca sebagai hasil asosiasi, bukan kausalitas.**  
   Uji normalitas residual lolos (`Shapiro-Wilk p = 0.092351`), tetapi homoskedastisitas dan tidak adanya autokorelasi tidak terpenuhi (`Breusch-Pagan p = 0.000006`, `Durbin-Watson = 1.0366`). Artinya, model tetap informatif, tetapi tidak ideal untuk klaim inferensial yang terlalu jauh.

5. **Pendekatan kategorik mengonfirmasi pola yang sama.**  
   Uji chi-square menghasilkan `χ² = 20.1823` dengan `p = 0.000460`, sementara Cramer's V sebesar `0.5222` menunjukkan asosiasi yang kuat. Karena `77.8%` sel memiliki expected frequency di bawah 5, Fisher's exact test juga digunakan dan tetap signifikan (`p = 0.035853`).

6. **Sel dengan kontribusi terbesar adalah kombinasi kemiskinan tinggi dan akses internet rendah.**  
   Kategori `[Tinggi × Rendah]` menyumbang `42.50%` dari total statistik chi-square, sehingga menjadi sinyal paling kuat dalam tabel kontingensi.

---

## ⚠️ Catatan & Keterbatasan

- **Ruang lingkup** terbatas pada provinsi di Indonesia tahun 2024.
- **Satu baris data** dihapus karena nilai rural internet untuk DKI Jakarta hilang.
- **Regresi linear** menunjukkan hubungan yang kuat, tetapi asumsi residual belum sepenuhnya ideal.
- **Binning kategorik** pada uji chi-square mengurangi detail dibanding analisis numerik.
- **Faktor lain** seperti infrastruktur, kebijakan, urbanisasi, dan geografi belum dimodelkan secara eksplisit.

<div align="center">
  <sub>Disusun sebagai repository portofolio teknis untuk analisis data dan statistik terapan.</sub>
</div>
