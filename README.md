# Analisis Sentimen Ulasan Aplikasi Maxime

## Deskripsi Proyek
Proyek ini mengimplementasikan analisis sentimen terhadap ulasan pengguna aplikasi Maxime dari Google Play Store. Tujuannya adalah mengklasifikasikan ulasan ke dalam kategori **positif**, **negatif**, atau **netral** menggunakan teknik machine learning. Data ulasan diambil melalui scraping, diproses, dan dianalisis dengan model seperti Support Vector Machine (SVM) dan Random Forest, yang dikombinasikan dengan fitur ekstraksi seperti TF-IDF dan Word2Vec.

Proyek ini mencakup:
- **Scraping Data**: Mengambil ulasan dari Google Play Store.
- **Preprocessing Teks**: Membersihkan teks, case folding, koreksi slang, tokenisasi, dan penghapusan stopword.
- **Pelatihan Model**: Menggunakan tiga skema model dengan pembagian data berbeda.
- **Testing**: Memprediksi sentimen pada ulasan baru.
- **Evaluasi**: Menghitung akurasi, precision, recall, dan F1-score.

Hasil analisis dapat digunakan untuk memahami persepsi pengguna terhadap aplikasi Maxime, seperti keluhan umum atau fitur yang disukai.

## Fitur Utama
- **Scraping Data**: Menggunakan `google-play-scraper` untuk mengumpulkan ulasan aplikasi.
- **Preprocessing Teks**: Meliputi pembersihan teks, konversi huruf kecil, koreksi kata slang, tokenisasi, penghapusan stopword, dan stemming dengan Sastrawi.
- **Model Machine Learning**:
  - Skema 1: SVM dengan TF-IDF (pembagian data 80/20).
  - Skema 2: Random Forest dengan Word2Vec (pembagian data 80/20).
  - Skema 3: Random Forest dengan TF-IDF (pembagian data 70/30).
- **Evaluasi**: Menyediakan laporan klasifikasi (precision, recall, F1-score) dan akurasi.
- **Inferensi**: Prediksi sentimen pada ulasan baru menggunakan model yang telah dilatih.
- **Penyimpanan Model**: Model dan vectorizer disimpan untuk penggunaan ulang.

## Persyaratan
Proyek ini menggunakan Python 3.12 dengan dependensi yang tercantum di `requirements.txt`. Beberapa library utama:
- pandas
- numpy
- scikit-learn
- gensim
- nltk
- Sastrawi
- google-play-scraper
- joblib

Contoh output prediksi:
```
Ulasan Asli: 'Aplikasi ini sangat membantu dan mudah digunakan. Saya suka sekali!'
Teks Diproses: 'aplikasi membantu mudah suka'
Prediksi SVM (TF-IDF 80/20)    : POSITIVE
Prediksi RF (Word2Vec 80/20)   : POSITIVE
Prediksi RF (TF-IDF 70/30)     : POSITIVE
```

Model yang telah dilatih disimpan di folder `models/` untuk penggunaan ulang.

## Dataset
- **Sumber**: Ulasan aplikasi Maxime (com.taxsee.taxsee) dari Google Play Store.
- **Jumlah Data**: Sekitar 121.500 ulasan, berisi kolom seperti `reviewId`, `content`, `score`, `thumbsUpCount`, dan lainnya.
- **File**: `ulasan_aplikasiMaxime.csv` (dihasilkan dari `scrape_data.ipynb`).

## Hasil dan Evaluasi
- **Akurasi**:
  - Skema 3 (RF + TF-IDF, 70/30): 85.75%
- **Laporan Klasifikasi (Skema 3)**:
  ```
              precision    recall  f1-score   support
  negative       0.71      0.70      0.71      8710
  neutral        0.08      0.01      0.01       156
  positive       0.90      0.91      0.91     27584
  accuracy                           0.86     36450
  macro avg      0.57      0.54      0.54     36450
  weighted avg   0.85      0.86      0.86     36450
  ```

Detail evaluasi untuk semua skema dapat dilihat di `analisisSentimentMaxime.ipynb`.
