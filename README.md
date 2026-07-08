# Dimensionality Reduction: Visualisasi Tingkat Stres Mahasiswa dengan PCA & t-SNE

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Ryynghh/Dimensionality-Reduction-Student-Stress/blob/main/Dimensionality_Reduction_Student_Stress.ipynb)

Tugas praktik pertemuan ke-25 mata kuliah *Fundamen Sains Data* — penerapan **Principal Component Analysis (PCA)** dan **t-Distributed Stochastic Neighbor Embedding (t-SNE)** untuk mereduksi dan memvisualisasikan data tingkat stres mahasiswa berdimensi tinggi.

## Anggota Kelompok

| Nama | NIM |
|---|---|
| Muhamad Rafi Raditya | 24523231 |
| Hidayat Nur Hijrah | 24523201 |
| Rayyan Galih Indarto | 24523224 |

---

## 1. Deskripsi Kasus

### Masalah yang Dihadapi
Dataset yang digunakan memiliki **21 kolom** (20 fitur + 1 target), sehingga tergolong data berdimensi tinggi. Memahami dan mengeksplorasi hubungan antar fitur secara langsung sangat sulit dilakukan oleh manusia — visualisasi 21 dimensi sekaligus tidak mungkin dilakukan, dan pendekatan *pair plot* untuk setiap kombinasi fitur akan menghasilkan terlalu banyak grafik yang sulit diinterpretasikan.

### Mengapa Dimensionality Reduction Dibutuhkan
1. **Kemampuan Visualisasi** — mereduksi 21 dimensi menjadi 2D memungkinkan data ditampilkan dalam scatter plot yang mudah dibaca, sehingga struktur internal data (cluster, sebaran, outlier) dapat teramati.
2. **Pemahaman Data** — visualisasi hasil reduksi membantu membangun intuisi awal tentang bagaimana fitur-fitur saling berinteraksi.
3. **Identifikasi Pola** — memudahkan penemuan tren atau sub-kelompok tersembunyi, misalnya karakteristik mahasiswa dengan tingkat stres tinggi vs rendah.

## 2. Dataset yang Digunakan

**[Student Stress Factors: A Comprehensive Analysis](https://www.kaggle.com/datasets/rxnach/student-stress-factors-a-comprehensive-analysis)** (Kaggle, file: `StressLevelDataset.csv`), dimuat melalui `kagglehub`.

- **Jumlah fitur:** 20 fitur numerik (mis. `anxiety_level`, `self_esteem`, `depression`, `sleep_quality`, `academic_performance`, `study_load`, `future_career_concerns`, `social_support`, dll.)
- **Target:** `stress_level` (kategori tingkat stres mahasiswa)
- Fitur (`X`) dan target (`y`) dipisahkan sebelum proses reduksi dimensi diterapkan.

## 3. Ringkasan Metode

| Aspek | PCA | t-SNE |
|---|---|---|
| Sifat | Linier | Non-linier |
| Fokus | Mempertahankan varians global terbesar | Mempertahankan struktur/kedekatan lokal |
| Output | Komponen utama (PC1, PC2) — kombinasi linear fitur asli | Koordinat 2D hasil embedding berdasarkan kemiripan lokal |
| Parameter kunci | `n_components=2` | `n_components=2`, `perplexity=30`, `random_state=42`, `max_iter=1000` |
| Kelebihan | Cepat, hasil dapat diinterpretasi (arah varians) | Sangat baik mengungkap cluster tersembunyi |
| Keterbatasan | Bisa kurang jelas untuk hubungan non-linier | Jarak antar cluster tidak selalu bermakna literal, lebih mahal secara komputasi |

Kedua metode diterapkan pada fitur yang sama (`X`, 20 dimensi) lalu divisualisasikan dalam scatter plot 2D dengan pewarnaan berdasarkan `stress_level`.

## 4. Hasil & Visualisasi

### Hasil PCA (2D)
Data 20 dimensi diproyeksikan ke dua komponen utama (PC1 & PC2) yang menangkap varians terbesar. Titik-titik dengan `stress_level` yang sama cenderung membentuk kelompok, namun karena sifatnya yang linier, batas antar kelompok pada beberapa area masih terlihat tumpang tindih.

### Hasil t-SNE (2D)
t-SNE menghasilkan pengelompokan yang secara umum lebih rapat dan lebih terpisah dibanding PCA, karena metode ini secara eksplisit mempertahankan kedekatan lokal antar observasi yang mirip. Individu dengan tingkat stres yang sama lebih cenderung membentuk "pulau" tersendiri pada plot.

> Visualisasi lengkap (scatter plot PCA dan t-SNE) dapat dilihat pada notebook `Dimensionality_Reduction_Student_Stress.ipynb`.

## 5. Analisis: PCA vs t-SNE

**PCA** unggul dalam mempertahankan struktur *global* data dan mudah diinterpretasikan karena berbasis kombinasi linear fitur asli, tetapi kurang optimal ketika hubungan antar fitur bersifat non-linier — cluster yang dihasilkan cenderung lebih tumpang tindih.

**t-SNE** unggul dalam mengungkap struktur *lokal* dan pola pengelompokan yang lebih halus, terutama karena hubungan antara faktor-faktor psikologis (kecemasan, harga diri, dukungan sosial, dsb.) dengan tingkat stres kemungkinan besar bersifat non-linier dan kompleks.

### Metode Mana yang Lebih Sesuai?
Untuk kasus **visualisasi dan eksplorasi cluster tingkat stres mahasiswa**, **t-SNE dinilai lebih sesuai** dibanding PCA, dengan alasan:
1. Fokus pada struktur lokal membuatnya lebih efektif mengungkap pengelompokan alami dalam data.
2. Mampu menangkap hubungan non-linier antar faktor psikologis-akademik yang memengaruhi stres.
3. Menghasilkan visualisasi cluster yang lebih terpisah dan intuitif untuk diinterpretasikan secara visual.

Meski demikian, PCA tetap bernilai sebagai langkah eksplorasi awal karena lebih cepat dan memberikan gambaran arah variabilitas utama dalam data sebelum dilakukan analisis lebih mendalam dengan t-SNE.

## 6. Cara Menjalankan

1. Buka notebook di Google Colab melalui badge di atas, atau clone repository ini dan jalankan secara lokal (Jupyter Notebook).
2. Install dependensi yang dibutuhkan:
   ```bash
   pip install kagglehub pandas scikit-learn matplotlib seaborn
   ```
3. Jalankan seluruh sel notebook secara berurutan (dataset akan otomatis diunduh melalui `kagglehub`).

## 7. Struktur Repository

```
.
├── Dimensionality_Reduction_Student_Stress.ipynb   # Notebook utama (kode + visualisasi + analisis)
└── README.md                                        # Dokumentasi tugas
```

## 8. Referensi

- Dataset: [Student Stress Factors: A Comprehensive Analysis — Kaggle](https://www.kaggle.com/datasets/rxnach/student-stress-factors-a-comprehensive-analysis)
- Scikit-learn Documentation — `sklearn.decomposition.PCA`
- Scikit-learn Documentation — `sklearn.manifold.TSNE`
