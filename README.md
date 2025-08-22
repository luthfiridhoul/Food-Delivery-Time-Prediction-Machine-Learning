# Food Delivery Time Prediction (Machine Learning)

Prediksi lama waktu pengantaran makanan (dalam menit) menggunakan model **Random Forest** dan **XGBoost**. Proyek ini berfokus pada akurasi prediksi serta identifikasi faktor-faktor yang paling memengaruhi waktu pengantaran (jarak, cuaca, lalu lintas, waktu pengantaran, jenis kendaraan, waktu persiapan, pengalaman kurir).

## Problem Statement & Goals
**Pertanyaan utama**
1) Bagaimana memprediksi lama waktu pengantaran dengan akurasi tinggi?  
2) Faktor apa saja yang paling berpengaruh terhadap lama pengantaran?

**Tujuan**
- Membangun model prediksi yang akurat & andal.
- Menyediakan insight operasional untuk meningkatkan efisiensi kurir & restoran.
- Memberikan estimasi waktu yang lebih realistis kepada pelanggan.

## Dataset
- Sumber: [Kaggle – Food Delivery Time Prediction](https://www.kaggle.com/datasets/denkuznetz/food-delivery-time-prediction)
- Ukuran: ±455 observasi, 9 variabel  
- Target: `Delivery_Time_min`

> Catatan lisensi/data: Dataset berasal dari Kaggle. Ikuti ketentuan lisensinya; repo ini hanya menyertakan **tautan**, bukan menyalin data mentah.

## Tahapan Proyek
1. **Data Preprocessing**
   - Missing values: kategorikal → modus; numerik → median
   - One-Hot Encoding (Weather, Traffic_Level, Time_of_Day, Vehicle_Type)
   - Standarisasi fitur numerik (StandardScaler)
   - Train–test split (80:20)
2. **EDA**
   - Distribusi target & fitur numerik (hist/boxplot)
   - Korelasi numerik, scatter `Distance_km` vs `Delivery_Time_min`
   - Boxplot kategorikal vs target
3. **Modeling**
   - Baseline: Random Forest, XGBoost (pipeline: scaler + OHE)
   - Evaluasi: **MAE, RMSE, R²**
4. **Hyperparameter Tuning**
   - `RandomizedSearchCV` untuk RF & XGB (5-fold CV, scorer RMSE)
5. **Interpretasi**
   - Permutation Feature Importance (Top features)
6. **Hasil & Rekomendasi**
   - Model terbaik + implikasi bisnis

## Hasil Utama (Setelah Tuning)
- **XGBoost (Tuned)**  
  - MAE: **6.596** | RMSE: **9.207** | R²: **0.811**  
  - CV RMSE (mean ± std): **11.949 ± 1.055**
- **Random Forest (Tuned)**  
  - MAE: **6.608** | RMSE: **9.519** | R²: **0.798**  
  - CV RMSE (mean ± std): **11.802 ± 0.895**

**Kesimpulan:** Kedua model akurat (error ±6–7 menit). **XGBoost (Tuned)** unggul tipis (RMSE lebih rendah, R² lebih tinggi) → direkomendasikan sebagai model utama.

## Rekomendasi Bisnis (Ringkas)
- Tampilkan **estimasi waktu** lebih realistis di aplikasi (rata-rata meleset ±6 menit).
- **Atur armada** di jam sibuk/area macet; perkuat penjadwalan berdasarkan Time_of_Day & Traffic_Level.
- Kolaborasi dengan restoran untuk **mempercepat preparation time**.
- Siapkan **mitigasi cuaca buruk** (armada/penjadwalan alternatif).
