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
Di industri telekomunikasi, menjaga keberlangsungan pelanggan (*customer retention*) sangat krusial karena biaya akuisisi pelanggan baru jauh lebih tinggi dibanding mempertahankan pelanggan yang ada[cite: 3]. Pada dataset IBM Telco Customer Churn, tingkat *churn* mencapai **26,5%** (1.869 dari 7.043 pelanggan)[cite: 3]. Penelitian ini bertujuan membangun sistem peringatan dini berbasis *machine learning* dan menganalisis faktor pemicunya agar tim operasional dapat mengambil langkah penanganan yang presisi[cite: 3].

### 2. Rumusan Masalah
1. Bagaimana kinerja *CatBoost Classifier* dalam memprediksi *customer churn* berdasarkan metrik *Recall*, *F1-score*, dan *ROC-AUC*?[cite: 3]
2. Faktor apa saja yang berkontribusi terhadap *churn* berdasarkan interpretasi SHAP (global dan lokal), serta bagaimana pemetaannya secara eksplisit menjadi rekomendasi tindakan retensi?[cite: 3]

---

## 🔬 State of the Art & Research Gap

Tabel berikut merangkum posisi penelitian ini dibandingkan dengan lima studi terdahulu[cite: 3]:

| No | Peneliti & Tahun | Metode & Dataset | Hasil Utama | Research Gap / Keterbatasan |
| :- | :--- | :--- | :--- | :--- |
| 1 | Azzahra & Agastya (2026) | Random Forest + SMOTE (IBM Telco) | ROC-AUC 0.833, F1 0.611 | Tidak melaporkan *hyperparameter tuning* & CV; SHAP sebatas *bar plot* tanpa memperlihatkan arah pengaruh (+/-)[cite: 3]. |
| 2 | Ali dkk. (2026) | CatBoost (IBM Telco) | ROC-AUC 0.840, F1 0.636 | SHAP hanya *bar plot* rata-rata; strategi retensi disusun per segmen risiko umum, bukan diturunkan langsung dari nilai SHAP[cite: 3]. |
| 3 | Damuri dkk. (2026) | XGBoost (Iranian Churn) | ROC-AUC 0.991 | Menggunakan dataset pola penggunaan; belum ada pemetaan eksplisit faktor SHAP ke aksi retensi operasional[cite: 3]. |
| 4 | Wang & Zhang (2024) | CatBoost (China Mobile) | Akurasi 0.852, ROC-AUC 0.926 | Menggunakan dataset operasional privat (tidak *reproducible*); interpretasi SHAP sebatas naratif[cite: 3]. |
| 5 | Nur dkk. (2025) | CatBoost + Optuna (IBM Telco) | ROC-AUC 0.937 | Validitas simulasi *counterfactual* sangat rendah (0.200); belum ada pemetaan eksplisit ke tindakan bisnis[cite: 3]. |

### 🎯 Solusi & Kebaharuan (Novelty)
Penelitian ini mengisi *research gap* di atas dengan menghubungkan secara langsung nilai kontribusi SHAP global (*beeswarm plot*) dan lokal (*waterfall plot*) beserta arah pengaruhnya (+/-) menjadi **Tabel Pemetaan Eksplisit Aksi Retensi Operasional** pada dataset publik IBM Telco yang teruji dan *reproducible*[cite: 3].

---

## 🗺️ Research Mind Map (Kerangka Pemikiran)

| Tahap | Deskripsi & Alur Logika |
| :--- | :--- |
| **1. Masalah Bisnis & Data** | Tingginya tingkat *churn* (26,5%) dan tingginya biaya akuisisi[cite: 3]. Membutuhkan tindakan retensi yang presisi[cite: 3]. |
| **2. Pendekatan Pemodelan** | *CatBoost Classifier* dengan *class weight* bawaan pada data riil, dievaluasi via *Stratified 5-Fold Cross-Validation*[cite: 3]. |
| **3. Explainable AI (XAI)** | Interpretasi SHAP dua tingkat: *Summary Beeswarm Plot* (global) dan *Waterfall Plot* (lokal)[cite: 3]. |
| **4. Kebaharuan (Novelty)** | Pemetaan eksplisit nilai & arah pengaruh SHAP (+/-) ke tindakan retensi pelanggan[cite: 3]. |
| **5. Luaran Akhir (Output)** | Tabel rekomendasi tindakan retensi operasional yang siap dieksekusi tim CRM[cite: 3]. |

---

## 📊 Dataset Riset

* **Nama Dataset**: IBM Telco Customer Churn (Kaggle)[cite: 3]
* **Ukuran Data**: 7.043 baris & 21 atribut[cite: 3]
* **Variabel Terikat**: `Churn` (Yes: 1.869 / 26,5%, No: 5.174 / 73,5%)[cite: 3]
* **Variabel Bebas (19 Atribut)**:[cite: 3]
  * **Demografi**: `gender`, `SeniorCitizen`, `Partner`, `Dependents`[cite: 3]
  * **Layanan**: `tenure`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`[cite: 3]
  * **Kontrak & Finansial**: `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`[cite: 3]

---

## ⚙️ Metodologi & Evaluation Metrics

1. **Pra-pemrosesan Data**: Hapus `customerID`, penyesuaian tipe data `TotalCharges`, dan konversi fitur kategorikal untuk CatBoost[cite: 3].
2. **Pemodelan**: *CatBoost Classifier* dengan penimbangan bobot kelas (*class weight*) pada data latih[cite: 3].
3. **Validasi Pemodelan**: *Stratified 5-Fold Cross-Validation*[cite: 3].
4. **Metrik Evaluasi**:
   * **Recall**: Diprioritaskan utama untuk meminimalkan *false negative* (pelanggan *churn* yang luput terdeteksi)[cite: 3].
   * **F1-Score**: Mengukur keseimbangan *Precision* dan *Recall* pada data tidak seimbang (*imbalanced data*)[cite: 3].
   * **ROC-AUC**: Mengukur kemampuan diskriminasi model pada berbagai tingkatan *threshold*[cite: 3].
   * **Confusion Matrix**: Matriks acuan penentu TP, FP, TN, dan FN[cite: 3].

---

## 📂 Struktur Repositori

```text
├── PROPOSAL PENELITIAN.pdf   # Dokumen proposal penelitian lengkap (Bab I - Bab III)
└── README.md                 # Rincian ringkasan repositori & proposal penelitian
