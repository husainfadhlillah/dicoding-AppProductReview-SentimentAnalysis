# Analisis Sentimen Ulasan Aplikasi Tokopedia 🛒

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/2560px-Pandas_logo.svg.png" width="90" alt="Pandas Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/NumPy_logo_2020.svg/2560px-NumPy_logo_2020.svg.png" width="90" alt="NumPy Logo">
  <img src="https://miro.medium.com/v2/resize:fit:592/1*YM2HXc7f4v02pZBEO8h-qw.png" width="55" alt="NLTK Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/XGBoost_logo.svg/2560px-XGBoost_logo.svg.png" width="100" alt="XGBoost Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/1200px-Scikit_learn_logo_small.svg.png" width="110" alt="Scikit-learn Logo">
 <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2d/Tensorflow_logo.svg/1200px-Tensorflow_logo.svg.png" width="50" alt="TensorFlow Logo">
  <img src="https://huggingface.co/front/assets/huggingface_logo-noborder.svg" width="60" alt="Hugging Face Transformers Logo">
</p>

Selamat datang di repositori proyek **Analisis Sentimen End-to-End** untuk ulasan aplikasi Tokopedia! Proyek ini mengupas tuntas proses pengolahan bahasa alami (NLP) untuk mengubah ribuan ulasan subjektif dari pengguna menjadi _insight_ bisnis yang terukur.

Untuk menemukan solusi terbaik, proyek ini tidak hanya membangun satu, tetapi **empat skema model** yang berbeda, membandingkan kekuatan _machine learning_ klasik dengan arsitektur _deep learning_ modern.

---

## 🚀 Alur Kerja Proyek

Proyek ini dirancang mengikuti siklus hidup ilmu data secara menyeluruh, dari hulu ke hilir:

**1. 📥 Pengumpulan Data**

- Melakukan _scraping_ **15.000 ulasan** aplikasi Tokopedia langsung dari Google Play Store.

**2. 🧹 Pra-pemrosesan & Pelabelan**

- Membersihkan teks ulasan dari _noise_ (simbol, angka, dll.), melakukan normalisasi kata, dan menghapus _stopwords_.
- Memberi label sentimen (**Positif, Netral, Negatif**) secara otomatis berdasarkan skor rating pengguna.

**3. 🔬 Eksperimen & Pemodelan (4 Skema)**

- Merancang, melatih, dan membandingkan empat arsitektur model yang berbeda untuk menemukan pendekatan yang paling optimal.

**4. 📊 Evaluasi & Analisis Komparatif**

- Mengevaluasi keempat model menggunakan metrik akurasi pada data latih dan data uji.
- Menganalisis hasil untuk memilih model juara.

**5. 💡 Inferensi Model Juara**

- Menggunakan model dengan performa terbaik untuk memprediksi sentimen pada kalimat-kalimat baru untuk memvalidasi kemampuannya dalam skenario dunia nyata.

---

## 🛠️ Tahapan Proyek Secara Detail

### Tahap 1: Pengumpulan Data

Data ulasan dikumpulkan menggunakan _script_ pada `scraping.ipynb` dengan _library_ `google-play-scraper`. Proses ini menghasilkan file `tokopedia_reviews_15000.csv` yang menjadi dataset utama untuk proyek ini.

### Tahap 2: Pra-pemrosesan Teks & Pelabelan

Teks mentah dari ulasan sangat _noisy_. Oleh karena itu, dilakukan serangkaian proses pembersihan yang ketat:

- **Case Folding**: Mengubah teks menjadi huruf kecil.
- **Noise & Punctuation Removal**: Menghapus semua karakter yang tidak relevan.
- **Normalization**: Menggunakan kamus _slang_ untuk mengubah kata tidak baku menjadi baku.
- **Stopword Removal**: Menghapus kata-kata umum dalam Bahasa Indonesia (menggunakan `NLTK` & `Sastrawi`).
- **Pelabelan Sentimen**: Ulasan diberi label berdasarkan skor bintang (`score`):
  - ⭐ 1-2: **Negatif**
  - ⭐ 3: **Netral**
  - ⭐ 4-5: **Positif**

### Tahap 3: Eksperimen dan Pelatihan Model

Untuk menemukan model dengan performa terbaik, kami merancang dan menguji empat skema eksperimen yang berbeda, masing-masing dengan kombinasi algoritma, representasi fitur, dan rasio pembagian data yang unik.

1.  **Skema 1: Random Forest + Word2Vec (Target Akurasi > 92%)**

    - **Arsitektur**: Model _ensemble_ klasik (Random Forest) yang dikombinasikan dengan _embedding_ **Word2Vec** untuk merepresentasikan makna kata secara kontekstual.
    - **Fitur Unik**: Menggunakan pembagian data **90% data latih** dan **10% data uji** untuk memberikan lebih banyak data pada model saat proses pelatihan.

2.  **Skema 2: XGBoost + Word2Vec (Target Akurasi > 85%)**

    - **Arsitektur**: Model _gradient boosting_ (XGBoost) yang terkenal dengan kecepatan dan performanya, juga menggunakan **Word2Vec** sebagai input fitur.
    - **Fitur Unik**: Menggunakan pembagian data standar **80% data latih** dan **20% data uji**.

3.  **Skema 3: Logistic Regression + TF-IDF (Target Akurasi > 85%)**

    - **Arsitektur**: Model linear sederhana (Logistic Regression) yang dipasangkan dengan metode representasi fitur klasik **TF-IDF** (Term Frequency-Inverse Document Frequency).
    - **Fitur Unik**: Berfungsi sebagai _baseline_ yang kuat untuk melihat seberapa baik performa model sederhana dibandingkan dengan model yang lebih kompleks.

4.  **Skema 4: Bi-LSTM (Deep Learning) (Target Akurasi > 85%)**
    - **Arsitektur**: Jaringan Saraf Tiruan Berulang (_Bidirectional Long Short-Term Memory_) yang dibangun menggunakan Keras, dengan **Embedding Layer** yang dilatih dari awal.
    - **Fitur Unik**: Dirancang untuk menangkap dependensi sekuensial dan konteks kalimat dari dua arah (depan ke belakang dan belakang ke depan).

---

## 🏆 Hasil Evaluasi & Model Juara

Keempat skema model dievaluasi secara ketat berdasarkan performa akurasinya pada data latih dan data uji. Hasilnya dirangkum dalam tabel berikut:

| Skema | Algoritma           | Representasi Fitur | Split Data | Akurasi Latih (%) | Akurasi Uji (%) |
| :---: | :------------------ | :----------------- | :--------: | :---------------: | :-------------: |
|   1   | **Random Forest**   | **Word2Vec**       | **90/10**  |       99.98       |  **92.25** 🏆   |
|   2   | XGBoost             | Word2Vec           |   80/20    |       99.74       |      90.32      |
|   3   | Logistic Regression | TF-IDF             |   80/20    |       91.98       |      87.26      |
|   4   | Bi-LSTM             | Embedding Layer    |   80/20    |       97.71       |      91.81      |

> **Analisis Hasil Komparatif:**
>
> - **Model Juara**: **Skema 1 (Random Forest + Word2Vec)** secara jelas menjadi pemenang dengan **akurasi uji tertinggi mencapai 92.25%**. Penggunaan 90% data untuk pelatihan terbukti efektif memberikan performa generalisasi terbaik pada data baru.
> - **Performa Model Lain**:
>   - **Bi-LSTM** (Skema 4) menunjukkan performa yang sangat kompetitif dan menjadi yang terbaik kedua dengan akurasi 91.81%, membuktikan kekuatan _deep learning_ pada data sekuensial.
>   - **XGBoost** (Skema 2) juga memberikan hasil yang solid di atas 90%, namun sedikit di bawah RF dan Bi-LSTM.
>   - **Logistic Regression** (Skema 3) berfungsi sebagai _baseline_ yang baik, namun performanya paling rendah, menandakan bahwa representasi fitur yang lebih canggih (Word2Vec, Embedding) memberikan nilai tambah yang signifikan.
> - **Overfitting**: Terlihat kecenderungan _overfitting_ pada model berbasis _tree_ (RF dan XGBoost) di mana akurasi latih sangat tinggi (mendekati 100%). Namun, Random Forest tetap mampu melakukan generalisasi dengan lebih baik pada data uji.

---

## 💡 Uji Coba Model Terbaik

Model juara, **Random Forest (Skema 1)**, kemudian diuji kemampuannya untuk melakukan inferensi pada kalimat-kalimat baru:

| Kalimat Uji                                   | Prediksi Sentimen |
| :-------------------------------------------- | :---------------: |
| "aplikasinya bagus dan sangat membantu"       |    **POSITIF**    |
| "update terbaru sering error dan lemot parah" |    **NEGATIF**    |
| "ini adalah aplikasi untuk belanja online"    |    **NETRAL**     |
| "kecewa, pesanan saya dibatalkan tiba-tiba"   |    **NEGATIF**    |

Model berhasil memprediksi sentimen dengan benar, membuktikan kemampuannya untuk menggeneralisasi pada data yang belum pernah dilihat sebelumnya dan memvalidasi keberhasilan _pipeline_ proyek secara keseluruhan.

---

## 📁 Struktur Repositori

```
├── scraping.ipynb
├── pelatihan_model.ipynb
├── tokopedia_reviews_15000.csv
├── requirements.txt
└── README.md
```

- **`scraping.ipynb`**: Notebook untuk _scraping_ data ulasan.
- **`pelatihan_model.ipynb`**: Notebook utama berisi pra-pemrosesan, analisis, pelatihan keempat model, dan evaluasi.
- **`tokopedia_reviews_15000.csv`**: Dataset mentah hasil _scraping_.
- **`requirements.txt`**: Daftar lengkap _library_ Python yang dibutuhkan untuk mereplikasi proyek.
- **`README.md`**: Dokumentasi lengkap yang sedang Anda baca ini.

---

## 🚀 Instalasi & Penggunaan

Untuk menjalankan proyek ini di lingkungan lokal Anda, ikuti langkah-langkah berikut:

1.  **Clone repositori ini:**

    ```bash
    git clone [https://github.com/NAMA_USER/NAMA_REPO.git](https://github.com/NAMA_USER/NAMA_REPO.git)
    cd NAMA_REPO
    ```

2.  **Buat dan aktifkan lingkungan virtual (sangat direkomendasikan):**

    ```bash
    python -m venv venv
    source venv/bin/activate  # Untuk Windows: venv\Scripts\activate
    ```

3.  **Instal semua dependensi dari file `requirements.txt`:**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Jalankan Jupyter Notebook:**
    Buka dan jalankan `pelatihan_model.ipynb` untuk melihat keseluruhan proses, dari data mentah hingga prediksi akhir.
    ```bash
    jupyter notebook
    ```
