# 🛍️ Analisis Sentimen Ulasan E-Commerce Indonesia
### Shopee · Lazada · Tokopedia

Proyek Big Data untuk menganalisis sentimen ulasan pengguna dari tiga platform e-commerce terbesar di Indonesia menggunakan teknik **Hybrid Labeling** dan model **Naive Bayes**.

---

## 📌 Deskripsi Proyek

Penelitian ini mengumpulkan dan menganalisis ulasan pengguna dari Google Play Store untuk aplikasi **Shopee**, **Lazada**, dan **Tokopedia**, lalu melakukan klasifikasi sentimen (positif/negatif) menggunakan pendekatan hybrid yang menggabungkan analisis rating dengan analisis teks berbasis lexicon.

---

## 🔄 Alur Pipeline

```
Scraping Data (Google Play)
        ↓
EDA & Eksplorasi
        ↓
Hybrid Labeling (Rating + Lexicon)
        ↓
Analisis Konsistensi
        ↓
Preprocessing & Feature Extraction
        ↓
WordCloud & Bigram Analysis
        ↓
Training Model (Naive Bayes)
        ↓
Evaluasi & Perbandingan Platform
        ↓
Insight & Kesimpulan
```

---

## 📂 Struktur File

```
├── BIG_DATA_UAS.ipynb           # Notebook utama
├── shopee_reviews.csv           # Data ulasan Shopee (hasil scraping)
├── lazada_reviews.csv           # Data ulasan Lazada (hasil scraping)
├── tokopedia_reviews.csv        # Data ulasan Tokopedia (hasil scraping)
├── data_mismatch_analisis.csv   # Data dengan label mismatch (untuk analisis)
└── README.md
```

---

## 🗃️ Dataset

Data diambil menggunakan library `google-play-scraper` dari Google Play Store Indonesia.

| Platform  | App ID                | Bahasa | Jumlah Target |
|-----------|----------------------|--------|---------------|
| Shopee    | `com.shopee.id`       | ID     | 10.000 ulasan |
| Lazada    | `com.lazada.android`  | ID     | 10.000 ulasan |
| Tokopedia | `com.tokopedia.tkpd`  | ID     | 10.000 ulasan |

**Kolom yang digunakan:** `reviewId`, `userName`, `content`, `score`, `at`

---

## 🏷️ Metode Hybrid Labeling

Pelabelan dilakukan secara otomatis tanpa anotasi manual, menggunakan dua sumber informasi:

### 1. Label dari Rating
- Rating ≥ 4 → **Positif**
- Rating ≤ 2 → **Negatif**
- Rating = 3 → **Dihapus** (ambigu)

### 2. Label dari Teks (Lexicon-Based)
Menggunakan kamus kata positif/negatif bahasa Indonesia & Inggris dengan deteksi negasi (contoh: *"tidak bagus"* → negatif).

### 3. Hybrid Logic
| Rating Label | Comment Label | Hasil       |
|-------------|---------------|-------------|
| Positif     | Positif       | ✅ Positif  |
| Negatif     | Negatif       | ✅ Negatif  |
| Apapun      | Unknown       | Ikut rating |
| Berbeda     | Berbeda       | ⚠️ Mismatch (dibuang) |

---

## 🤖 Model Machine Learning

Model yang digunakan: **Multinomial Naive Bayes**

Evaluasi dilakukan pada data test masing-masing platform menggunakan metrik:
- Accuracy
- Precision (weighted)
- Recall (weighted)
- F1-Score (weighted)
- Confusion Matrix

---

## 📊 Visualisasi yang Dihasilkan

- `1_distribusi_sentimen_keseluruhan.png` — Bar chart sentimen gabungan
- `3_pie_sentimen_per_platform.png` — Pie chart per platform
- `wordcloud_analysis.png` — WordCloud (semua/positif/negatif) per platform
- Confusion Matrix & bar chart evaluasi model

---

## 🛠️ Instalasi & Menjalankan

### Prasyarat
- Python 3.8+
- Jupyter Notebook / Google Colab

### Install dependencies

```bash
pip install google-play-scraper pandas numpy matplotlib seaborn scikit-learn nltk wordcloud
```

### Urutan menjalankan notebook

1. **Scraping Data** — Jalankan sel scraping untuk mengumpulkan ulasan (atau gunakan CSV yang sudah ada)
2. **EDA** — Eksplorasi dan ringkasan statistik data
3. **Hybrid Labeling** — Proses pelabelan otomatis
4. **Analisis Konsistensi** — Cek keselarasan rating vs komentar
5. **Feature Extraction & Model** — Preprocessing, TF-IDF, training Naive Bayes
6. **Evaluasi & Insight** — Perbandingan performa antar platform

---

## ⚠️ Limitasi

- Label awal masih bergantung pada rating pengguna yang bersifat subjektif
- Lexicon sederhana belum mampu memahami konteks kalimat secara penuh
- Bahasa slang, singkatan, dan sarkasme masih sulit dikenali model

---

## 👥 Tim

Dibuat sebagai proyek  mata kuliah **Big Data**

| Steffany Claussia Fernanda | 24083010026 | 

| Laudya Meitaneia Sianturi  | 24083010089 | 

| Alysha Khanza Dwi Avianti  | 24083010123 | 

---

