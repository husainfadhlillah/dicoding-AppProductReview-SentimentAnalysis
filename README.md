# Analisis Sentimen Ulasan Aplikasi Tokopedia 🛒

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/2560px-Pandas_logo.svg.png" width="90" alt="Pandas Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/NumPy_logo_2020.svg/2560px-NumPy_logo_2020.svg.png" width="90" alt="NumPy Logo">
  <img src="https://miro.medium.com/v2/resize:fit:592/1*YM2HXc7f4v02pZBEO8h-qw.png" width="55" alt="NLTK Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/XGBoost_logo.svg/2560px-XGBoost_logo.svg.png" width="60" alt="XGBoost Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/1200px-Scikit_learn_logo_small.svg.png" width="110" alt="Scikit-learn Logo">
  <img src="https://huggingface.co/front/assets/huggingface_logo-noborder.svg" width="60" alt="Hugging Face Transformers Logo">
</p>

Selamat datang di proyek _end-to-end_ untuk analisis sentimen ulasan aplikasi Tokopedia! Di dunia _e-commerce_ yang kompetitif, memahami suara pelanggan adalah kunci. Proyek ini mengotomatiskan proses analisis ribuan ulasan pengguna dari Google Play Store, mengubah teks kualitatif menjadi _insight_ kuantitatif yang dapat ditindaklanjuti.

---

## 🚀 Alur Kerja Proyek

Proyek ini mencakup siklus hidup _machine learning_ secara lengkap, dari pengumpulan data hingga inferensi model.

**1. 📥 Pengumpulan Data**

- Melakukan _scraping_ **15.000 ulasan** aplikasi Tokopedia dari Google Play Store menggunakan `google-play-scraper`.

**2. 🧹 Pra-pemrosesan & Pelabelan**

- Membersihkan teks ulasan (case folding, cleaning, normalisasi, stopword removal).
- Memberi label sentimen (**Positif, Netral, Negatif**) secara otomatis berdasarkan skor rating.

**3. 🔬 Eksperimen & Pemodelan**

- Melakukan eksperimen dengan tiga arsitektur model yang berbeda untuk menemukan yang terbaik:
  - **Model A**: `Word2Vec` + `Random Forest`
  - **Model B**: `Word2Vec` + `XGBoost`
  - **Model C**: `Pre-trained Transformer` (IndoBERT)

**4. 📊 Evaluasi & Analisis**

- Mengevaluasi semua model menggunakan metrik klasifikasi standar.
- Menganalisis hasil untuk memilih model juara.

**5. 💡 Inferensi Model**

- Menggunakan model terbaik untuk memprediksi sentimen pada kalimat baru yang belum pernah dilihat sebelumnya.

---

## 🛠️ Tahapan Proyek Secara Detail

### Tahap 1: Pengumpulan Data

Data ulasan dikumpulkan menggunakan _script_ pada `scraping.ipynb`. Proses ini menghasilkan file `tokopedia_reviews_15000.csv` yang menjadi fondasi untuk seluruh analisis.

### Tahap 2: Pra-pemrosesan Teks & Pelabelan

Teks mentah dari ulasan sangat _noisy_. Oleh karena itu, dilakukan serangkaian proses pembersihan yang ketat:

- **Case Folding**: Mengubah semua teks menjadi huruf kecil.
- **Noise & Punctuation Removal**: Menghapus angka, karakter spesial, dan tanda baca.
- **Normalization**: Mengonversi kata-kata slang atau singkatan ke bentuk bakunya (menggunakan kamus).
- **Stopword Removal**: Menghapus kata-kata umum yang tidak memiliki makna sentimen (menggunakan library `NLTK` & `Sastrawi`).
- **Pelabelan**: Ulasan diberi label berdasarkan skor bintang (`score`):
  - ⭐ 1-2: **Negatif**
  - ⭐ 3: **Netral**
  - ⭐ 4-5: **Positif**

### Tahap 3: Pemodelan & Eksperimen

Kami membandingkan tiga pendekatan untuk mendapatkan pemahaman yang komprehensif:

1.  **Machine Learning Klasik dengan Word2Vec**: Kami menggunakan `Random Forest` dan `XGBoost`, dua algoritma _ensemble_ yang sangat kuat, dengan fitur teks yang direpresentasikan oleh vektor **Word2Vec**. Word2Vec mampu menangkap konteks semantik kata dalam ulasan.
2.  **Deep Learning dengan Transformer**: Sebagai pembanding, kami menggunakan **IndoBERT**, sebuah model Transformer _state-of-the-art_ yang sudah dilatih secara khusus untuk Bahasa Indonesia. Model ini diharapkan mampu memahami nuansa bahasa yang lebih kompleks.

---

## 🏆 Hasil Evaluasi & Model Juara

Setelah melatih dan mengevaluasi ketiga model pada data uji, kami mendapatkan hasil berikut:

| Model                        | Akurasi  | Presisi  |  Recall  |  F1-Score   |
| :--------------------------- | :------: | :------: | :------: | :---------: |
| **Random Forest + Word2Vec** | **0.90** | **0.90** | **0.90** | **0.90** 🏆 |
| XGBoost + Word2Vec           |   0.89   |   0.89   |   0.89   |    0.89     |
| IndoBERT (Transformer)       |   0.88   |   0.88   |   0.88   |    0.88     |

> **Analisis Hasil**:
> Mengejutkan! Model **Random Forest dengan embedding Word2Vec** berhasil mengungguli model Transformer yang lebih kompleks. Hal ini menunjukkan bahwa dengan _feature engineering_ yang cerdas (Word2Vec) dan dataset yang cukup, model _machine learning_ klasik masih bisa menjadi solusi yang sangat efektif, efisien, dan lebih mudah diinterpretasikan.

---

## 💡 Uji Coba Model Terbaik

Untuk membuktikan kemampuannya, model Random Forest diuji pada beberapa kalimat baru:

| Kalimat Uji                             | Prediksi Sentimen |
| :-------------------------------------- | :---------------: |
| "aplikasinya bagus dan sangat membantu" |    **POSITIF**    |
| "sering error dan lemot parah"          |    **NEGATIF**    |
| "ini adalah aplikasi e-commerce"        |    **NETRAL**     |

Hasil inferensi menunjukkan bahwa model dapat menggeneralisasi dengan sangat baik dan berhasil menangkap sentimen dari teks yang belum pernah dilihatnya. Ini adalah bukti keberhasilan dari keseluruhan _pipeline_ yang dibangun.

---

## 📁 Struktur Repositori

```

├── scraping.ipynb
├── pelatihan_model.ipynb
├── tokopedia_reviews_15000.csv
├── requirements.txt
└── README.md

```

- **`scraping.ipynb`**: Notebook untuk scraping data ulasan dari Google Play Store.
- **`pelatihan_model.ipynb`**: Notebook utama berisi pra-pemrosesan, analisis, pelatihan, dan evaluasi model.
- **`tokopedia_reviews_15000.csv`**: Dataset hasil scraping.
- **`requirements.txt`**: Daftar _library_ Python yang dibutuhkan.
- **`README.md`**: Dokumentasi proyek yang sedang Anda baca.

---

## 🚀 Instalasi & Penggunaan

Untuk menjalankan proyek ini di lingkungan Anda, ikuti langkah berikut:

1.  **Clone repositori ini:**

    ```bash
    git clone [https://github.com/NAMA_USER/NAMA_REPO.git](https://github.com/NAMA_USER/NAMA_REPO.git)
    cd NAMA_REPO
    ```

2.  **Buat dan aktifkan lingkungan virtual (direkomendasikan):**

    ```bash
    python -m venv venv
    source venv/bin/activate  # Untuk Windows: venv\Scripts\activate
    ```

3.  **Instal semua dependensi:**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Jalankan Notebook:**
    Anda dapat menjalankan `scraping.ipynb` terlebih dahulu untuk menghasilkan dataset baru, atau langsung menjalankan `pelatihan_model.ipynb` untuk menggunakan dataset yang sudah tersedia.
    ```bash
    jupyter notebook
    ```
