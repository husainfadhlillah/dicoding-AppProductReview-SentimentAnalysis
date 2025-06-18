# Analisis Sentimen Ulasan Aplikasi Tokopedia 🛒

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/2560px-Pandas_logo.svg.png" width="90" alt="Pandas Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/NumPy_logo_2020.svg/2560px-NumPy_logo_2020.svg.png" width="90" alt="NumPy Logo">
  <img src="https://miro.medium.com/v2/resize:fit:592/1*YM2HXc7f4v02pZBEO8h-qw.png" width="55" alt="NLTK Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/XGBoost_logo.svg/2560px-XGBoost_logo.svg.png" width="100" alt="XGBoost Logo">
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/1200px-Scikit_learn_logo_small.svg.png" width="110" alt="Scikit-learn Logo">
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

- Melatih dan membandingkan empat arsitektur model yang berbeda secara fundamental untuk menemukan pendekatan yang paling optimal.

**4. 📊 Evaluasi & Analisis Komparatif**

- Mengevaluasi keempat model menggunakan metrik klasifikasi standar (_Accuracy, Precision, Recall, F1-Score_).
- Menganalisis kelebihan dan kekurangan masing-masing pendekatan.

**5. 💡 Inferensi Model Juara**

- Menguji model dengan performa terbaik pada kalimat-kalimat baru untuk memvalidasi kemampuannya dalam skenario dunia nyata.

---

## 🛠️ Tahapan Proyek Secara Detail

### Tahap 1: Pengumpulan Data

Data ulasan dikumpulkan menggunakan _script_ pada `scraping.ipynb` dengan _library_ `google-play-scraper`. Proses ini menghasilkan file `tokopedia_reviews_15000.csv` yang menjadi dataset utama untuk proyek ini.

### Tahap 2: Pra-pemrosesan Teks & Pelabelan

Teks ulasan mentah dibersihkan melalui beberapa langkah penting untuk mempersiapkannya sebelum masuk ke model:

- **Case Folding**: Mengubah teks menjadi huruf kecil.
- **Noise & Punctuation Removal**: Menghapus semua karakter yang tidak relevan.
- **Normalization**: Menggunakan kamus _slang_ untuk mengubah kata tidak baku menjadi baku.
- **Stopword Removal**: Menghapus kata-kata umum dalam Bahasa Indonesia (menggunakan `NLTK` & `Sastrawi`).
- **Pelabelan Sentimen**: Ulasan diberi label berdasarkan skor bintang (`score`):
  - ⭐ 1-2: **Negatif**
  - ⭐ 3: **Netral**
  - ⭐ 4-5: **Positif**

### Tahap 3: Pemodelan & Eksperimen dengan 4 Skema

Ini adalah inti dari proyek, di mana kami bereksperimen dengan empat pendekatan berbeda:

1.  **Model A: Random Forest + Word2Vec**

    - **Arsitektur**: Model _ensemble_ klasik yang kuat dikombinasikan dengan _embedding_ **Word2Vec** untuk merepresentasikan makna kata secara kontekstual.
    - **Tujuan**: Menguji kekuatan _machine learning_ tradisional dengan _feature engineering_ yang cerdas.

2.  **Model B: XGBoost + Word2Vec**

    - **Arsitektur**: Model _gradient boosting_ yang terkenal dengan kecepatan dan performanya, juga menggunakan **Word2Vec** sebagai input fitur.
    - **Tujuan**: Membandingkan performa antara dua algoritma _ensemble_ terkemuka (Random Forest vs XGBoost) pada tugas yang sama.

3.  **Model C: Bi-LSTM (Deep Learning)**

    - **Arsitektur**: Jaringan Saraf Tiruan Berulang (RNN) dengan arsitektur _Bidirectional Long Short-Term Memory_ menggunakan **Keras Embedding Layer**.
    - **Tujuan**: Menguji kemampuan model _deep learning_ sekuensial dalam menangkap ketergantungan jangka panjang dalam teks.

4.  **Model D: IndoBERT (Transformer)**
    - **Arsitektur**: Model Transformer _state-of-the-art_ yang sudah di-_pre-train_ pada korpus besar Bahasa Indonesia.
    - **Tujuan**: Mengukur performa dari model bahasa skala besar yang canggih sebagai _benchmark_ teratas.

---

## 🏆 Hasil Evaluasi & Model Juara

Keempat model dievaluasi secara ketat pada data uji yang sama. Hasilnya memberikan _insight_ yang sangat menarik:

| Model                        | Akurasi  | Presisi  |  Recall  |  F1-Score   |
| :--------------------------- | :------: | :------: | :------: | :---------: |
| **Random Forest + Word2Vec** | **0.90** | **0.90** | **0.90** | **0.90** 🏆 |
| XGBoost + Word2Vec           |   0.89   |   0.89   |   0.89   |    0.89     |
| Bi-LSTM (Keras)              |   0.87   |   0.87   |   0.87   |    0.87     |
| IndoBERT (Transformer)       |   0.88   |   0.88   |   0.88   |    0.88     |

> **Analisis Hasil Komparatif:**
> Secara mengejutkan, model **Random Forest dengan embedding Word2Vec** muncul sebagai pemenang dengan performa tertinggi di semua metrik. Ini adalah temuan penting yang menunjukkan bahwa:
>
> - **_Feature Engineering_ Masih Relevan**: Representasi fitur yang baik (Word2Vec) dapat membuat model klasik menjadi sangat kompetitif.
> - **Kompleksitas Bukan Segalanya**: Model _Deep Learning_ yang lebih kompleks (Bi-LSTM dan IndoBERT) tidak selalu menjamin performa yang lebih baik, terutama pada dataset dengan ukuran sedang dan tugas klasifikasi yang relatif jelas.
> - **Efisiensi**: Model Random Forest cenderung lebih cepat untuk dilatih dibandingkan dengan model _deep learning_, menjadikannya pilihan yang sangat praktis dan efisien.

---

## 💡 Uji Coba Model Terbaik

Model juara, **Random Forest**, kemudian diuji kemampuannya untuk melakukan inferensi pada kalimat-kalimat baru:

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
