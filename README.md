# Prediksi Customer Churn Menggunakan CatBoost dan Interpretasi SHAP untuk Mendukung Strategi Retensi Pelanggan

Repository ini berisi proposal penelitian dan dokumentasi tugas **Evaluasi Tengah Semester (ETS) Riset Informatika**.

---

## 📌 Informasi Peneliti
* **Nama**: Reno Naufal Maulidyan
* **NPM**: 23081010026
* **Program Studi**: Informatika
* **Mata Kuliah**: Riset Informatika

---

## 📝 Ringkasan Proposal Penelitian

### 1. Latar Belakang & Urgensi
Di industri telekomunikasi, menjaga keberlangsungan pelanggan (*customer retention*) sangat krusial karena biaya akuisisi pelanggan baru jauh lebih tinggi dibanding mempertahankan pelanggan yang ada. Pada dataset IBM Telco Customer Churn, tingkat *churn* mencapai **26,5%** (1.869 dari 7.043 pelanggan). Penelitian ini bertujuan membangun sistem peringatan dini berbasis *machine learning* dan menganalisis faktor pemicunya agar tim operasional dapat mengambil langkah penanganan yang presisi.

### 2. Rumusan Masalah
1. Bagaimana kinerja *CatBoost Classifier* dalam memprediksi *customer churn* berdasarkan metrik *Recall*, *F1-score*, dan *ROC-AUC*?
2. Faktor apa saja yang berkontribusi terhadap *churn* berdasarkan interpretasi SHAP (global dan lokal), serta bagaimana pemetaannya secara eksplisit menjadi rekomendasi tindakan retensi?

### 3. Kebaharuan (Novelty & Research Gap)
Penelitian ini menghubungkan secara langsung kontribusi nilai beserta arah pengaruh (+/-) dari SHAP global (*beeswarm plot*) dan lokal (*waterfall plot*) menjadi **Tabel Pemetaan Eksplisit Aksi Retensi Operasional** pada dataset publik IBM Telco yang teruji dan *reproducible*.

---

## 🗺️ Research Mind Map (Kerangka Pemikiran)

| Tahap | Deskripsi & Alur Logika |
| :--- | :--- |
| **1. Masalah Bisnis & Data** | Tingginya tingkat *churn* (26,5%) dan tingginya biaya akuisisi. Membutuhkan tindakan retensi yang presisi. |
| **2. Pendekatan Pemodelan** | *CatBoost Classifier* dengan *class weight* bawaan pada data riil, dievaluasi via *Stratified 5-Fold Cross-Validation*. |
| **3. Explainable AI (XAI)** | Interpretasi SHAP dua tingkat: *Summary Beeswarm Plot* (global) dan *Waterfall Plot* (lokal). |
| **4. Kebaharuan (Novelty)** | Pemetaan eksplisit nilai & arah pengaruh SHAP (+/-) ke tindakan retensi pelanggan. |
| **5. Luaran Akhir (Output)** | Tabel rekomendasi tindakan retensi operasional yang siap dieksekusi tim CRM. |

---

## 📊 Dataset Riset

* **Nama Dataset**: IBM Telco Customer Churn (Kaggle)
* **Ukuran Data**: 7.043 baris & 21 atribut
* **Variabel Terikat**: `Churn` (Yes: 1.869 / 26,5%, No: 5.174 / 73,5%)
* **Variabel Bebas (19 Atribut)**:
  * **Demografi**: `gender`, `SeniorCitizen`, `Partner`, `Dependents`
  * **Layanan**: `tenure`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`
  * **Kontrak & Finansial**: `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`

---

## ⚙️ Metodologi & Evaluation Metrics

1. **Pra-pemrosesan Data**: Hapus `customerID`, penyesuaian tipe data `TotalCharges`, dan konversi fitur kategorikal untuk CatBoost.
2. **Pemodelan**: *CatBoost Classifier* dengan penimbangan bobot kelas (*class weight*) pada data latih.
3. **Validasi Pemodelan**: *Stratified 5-Fold Cross-Validation*.
4. **Metrik Evaluasi**:
   * **Recall**: Diprioritaskan utama untuk meminimalkan *false negative* (pelanggan *churn* yang luput terdeteksi).
   * **F1-Score**: Mengukur keseimbangan *Precision* dan *Recall* pada data tidak seimbang (*imbalanced data*).
   * **ROC-AUC**: Mengukur kemampuan diskriminasi model pada berbagai tingkatan *threshold*.
   * **Confusion Matrix**: Matriks acuan penentu TP, FP, TN, dan FN.

---

## 📂 Struktur Repositori

```text
├── PROPOSAL PENELITIAN.pdf   # Dokumen proposal penelitian lengkap (Bab I - Bab III)
└── README.md                 # Rincian ringkasan repositori & proposal penelitian
