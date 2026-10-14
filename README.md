# Tugas UTS: Linear Regression & Logistic Regression

## 👤 Identitas Mahasiswa
- **Nama:** Hadi Sulaiman
- **NIM:** 241011402572
- **Kelas:** 05TPLM003
- **Program Studi:** S-1 Teknik Informatika
- **Mata Kuliah:** Machine Learning
- **Random State:** 72 (2 Digit Terakhir NIM)

---

## 📊 Ringkasan Hasil Pengerjaan

### 1. Bagian A — Linear Regression (Dataset: `Ads_Data.csv`)
Memodelkan hubungan antara **Biaya Iklan** ($X$, dalam Juta Rp) terhadap **Penjualan** ($y$, dalam Juta Rp).

- **Persamaan Garis Regresi (Normal Equation):**
  $$\hat{y} = 27.6480 + 9.1215 \cdot X$$
  *Interpretasi:* Penjualan dasar tanpa iklan diperkirakan sebesar Rp27,65 juta. Setiap penambahan biaya iklan sebesar Rp1 juta akan meningkatkan penjualan rata-rata sebesar Rp9,12 juta.

- **Hasil Evaluasi Model:**
  | Dataset | MAE (Juta Rp) | MSE | RMSE (Juta Rp) | $R^2$ Score |
  |---|:---:|:---:|:---:|:---:|
  | **Training** | 4.8030 | 40.6667 | 6.3770 | **0.9298 (92.98%)** |
  | **Testing** | 3.6673 | 18.8028 | 4.3362 | **0.9688 (96.88%)** |

- **Eksperimen Learning Rate pada Gradient Descent:**
  - $\alpha = 0.001$: Terlalu lambat (belum konvergen setelah 5.000 iterasi).
  - $\alpha = 0.02$: **Optimal / Pas** (konvergen stabil dengan nilai identik dengan Normal Equation: $b = 27.6480, m = 9.1215$).
  - $\alpha = 0.1$: **Divergen / Gagal Konvergen** (loss meledak/overflow karena overshooting langkah pembaruan).

- **Prediksi Kasus Baru:**
  - Biaya Iklan **Rp4,5 Juta** $\rightarrow$ Estimasi Penjualan: **Rp68,69 Juta**
  - Biaya Iklan **Rp7,0 Juta** $\rightarrow$ Estimasi Penjualan: **Rp91,50 Juta**
  - Biaya Iklan **Rp12,0 Juta** $\rightarrow$ Estimasi Penjualan: **Rp137,11 Juta** *(Ekstrapolasi: perlu dicermati karena berada jauh di luar rentang data historis 0.8–6.5 juta)*.

---

### 2. Bagian B — Logistic Regression (Dataset: `Email_Data.csv`)
Membuat filter **Spam** berdasarkan variabel **Jumlah Link** ($X_1$) dan **Jumlah Kata Promo** ($X_2$).

- **Persamaan Probabilitas Logistik:**
  $$P(\text{Spam}) = \sigma(-10.3273 + 0.9351 \cdot \text{JumlahLink} + 0.8704 \cdot \text{KataPromo})$$

- **Persamaan Garis Batas Keputusan (*Decision Boundary* pada $P=0.5$):**
  $$\text{KataPromo} = 11.8650 - 1.0743 \cdot \text{JumlahLink}$$

- **Eksperimen Ambang Batas (*Threshold*):**
  | Threshold | Akurasi | Precision | Recall | F1-Score | Keterangan |
  |:---:|:---:|:---:|:---:|:---:|---|
  | **0.3** | 73.33% | 62.50% | 83.33% | 0.7143 | Terlalu agresif menandai spam (FP tinggi) |
  | **0.5** | 80.00% | 71.43% | 83.33% | 0.7692 | Ambang batas seimbang standar |
  | **0.7 (Pilihan)** | **86.67%** | **100.00%** | **66.67%** | **0.8000** | **Terbaik: Presisi 100% (FP = 0), aman dari email penting terbuang** |

- **Prediksi Email Baru (Ambang Batas 0.7):**
  - **E1** (Link: 1, Promo: 2) $\rightarrow P(\text{Spam}) = 0.0005 \rightarrow$ **Bukan Spam (0)**
  - **E2** (Link: 5, Promo: 6) $\rightarrow P(\text{Spam}) = 0.3942 \rightarrow$ **Bukan Spam (0)**
  - **E3** (Link: 9, Promo: 10) $\rightarrow P(\text{Spam}) = 0.9989 \rightarrow$ **Spam (1)**
  - **E4** (Link: 2, Promo: 11) $\rightarrow P(\text{Spam}) = 0.7534 \rightarrow$ **Spam (1)**

---

### 3. Bagian C — Jawaban Pemahaman Konsep
Seluruh 5 pertanyaan refleksi mengenai alasan penamaan Logistic Regression, peran sigmoid, perbandingan Normal Equation vs Gradient Descent, overfitting, perbandingan MSE vs Log Loss, serta variasi hasil berbasis random state NIM telah dijawab tuntas dengan argumentasi teoretis yang mendalam.

---

### 4. Bagian Bonus — Perbandingan dengan Scikit-Learn
- **Linear Regression:** Intercept, koefisien, MSE, dan $R^2$ antara implementasi manual dengan pustaka Scikit-Learn menghasilkan nilai yang **persis sama (100% identik)**.
- **Logistic Regression:** Model Scikit-Learn tanpa penalti (`penalty=None`) menghasilkan nilai akurasi klasifikasi pada data uji yang **identik** dengan implementasi Gradient Descent manual.

---

## 📁 Struktur Berkas Tugas
```
uts-machine-learning-241011402572/
├── README.md            # Dokumentasi identitas, metodologi, dan ringkasan hasil
├── tugas_UTS.ipynb      # Jupyter Notebook lengkap dengan visualisasi output
├── Ads_Data.csv         # Dataset regresi linear
└── Email_Data.csv       # Dataset klasifikasi regresi logistik
```
