# 🍅 Knowledge Distillation – Model Development Repository

Repository ini berisi kode pengembangan dan eksperimen model untuk klasifikasi 
penyakit daun tomat menggunakan Knowledge Distillation. Fokus utama repository 
ini adalah pengecilan ukuran pelatihan model Teacher, proses distilasi pengetahuan ke model Student, 
serta eksperimen parameter untuk menghasilkan model yang efisien dan akurat.

Repository ini terpisah dari repository deployment (Flask/Hugging Face). 
Repository ini hanya mencakup proses training, evaluasi, dan eksperimen model.

---

## Ruang Lingkup Model

Pengembangan model dalam repository ini mencakup beberapa tahap berikut:

### 1. Model Teacher — EfficientNetB5

Model guru yang dilatih sebagai acuan dalam proses Knowledge Distillation:

- EfficientNetB5 pretrained ImageNet
- Input size: 456×456 px

Model Teacher digunakan sebagai pembanding performa dari sisi:

- Akurasi klasifikasi
- Ukuran model
- Waktu inferensi

### 2. Model Student Baseline — EfficientNetB0

Model murid yang dilatih **tanpa** Knowledge Distillation sebagai baseline:

- EfficientNetB0 pretrained ImageNet
- Input size: 224×224 px

### 3. Knowledge Distillation

Proses transfer pengetahuan dari Teacher ke Student menggunakan Distillation Loss:

- **Soft Loss**: KL Divergence antara distribusi probabilitas Teacher dan Student
- **Hard Loss**: Cross Entropy antara prediksi Student dengan label asli

Parameter distilasi yang digunakan:

- **Temperature (T)**: mengontrol kehalusan distribusi probabilitas
- **Alpha (α)**: mengontrol bobot antara Soft Loss dan Hard Loss

### 4. Eksperimen Parameter

Eksperimen dilakukan untuk mencari kombinasi T dan α terbaik:

**Eksperimen Alpha** — Temperature dikunci T=3, Alpha divariasikan:

- α = 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9

**Eksperimen Temperature** — Alpha dikunci α=0.3, Temperature divariasikan:

- T = 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

### 5. Model Terbaik (Final Model)

Model akhir yang dihasilkan merupakan Student terbaik berdasarkan eksperimen:

- **Arsitektur**: EfficientNetB0
- **Temperature**: T = 3
- **Alpha**: α = 0.1
