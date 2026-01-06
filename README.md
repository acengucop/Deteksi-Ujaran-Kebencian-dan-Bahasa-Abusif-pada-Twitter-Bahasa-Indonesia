# Deteksi Ujaran Kebencian dan Bahasa Abusif pada Twitter Bahasa Indonesia  
## Menggunakan Multi-Label Classification dan Model Transformer (IndoBERTweet)

## Deskripsi Proyek

Proyek ini bertujuan untuk membangun sistem **deteksi ujaran kebencian (hate speech) dan bahasa abusif (abusive language)** pada teks Twitter berbahasa Indonesia menggunakan pendekatan **multi-label classification** berbasis **model Transformer IndoBERTweet**.

Berbeda dengan klasifikasi biasa yang hanya memberikan satu label pada satu teks, pendekatan multi-label memungkinkan **satu tweet memiliki lebih dari satu label secara bersamaan**, misalnya:
- mengandung ujaran kebencian,
- bersifat bahasa kasar,
- ditujukan kepada individu atau kelompok,
- berbasis agama, ras, gender,
- serta memiliki tingkat intensitas tertentu.

Sistem ini dirancang agar dapat digunakan dan dipahami oleh pengguna awam, dengan menampilkan hasil prediksi menggunakan **nama label lengkap tanpa singkatan**.

---

## Latar Belakang

Media sosial seperti Twitter memungkinkan pengguna menyampaikan opini secara bebas dan cepat. Namun, kebebasan ini juga memicu meningkatnya penyebaran ujaran kebencian dan bahasa kasar yang dapat berdampak negatif terhadap individu maupun kelompok masyarakat.

Dalam konteks Indonesia yang memiliki keberagaman sosial, ujaran kebencian sering kali bersifat kompleks dan berlapis. Satu tweet dapat mengandung beberapa jenis ujaran kebencian sekaligus. Oleh karena itu, pendekatan **multi-label classification** menjadi penting untuk menggambarkan kondisi tersebut secara lebih realistis.

Model Transformer, khususnya **IndoBERTweet**, dipilih karena telah dilatih menggunakan data Twitter Bahasa Indonesia dan terbukti mampu memahami konteks bahasa informal dengan baik.

---

## Tujuan Proyek

Tujuan utama dari proyek ini adalah:

1. Mengembangkan sistem deteksi ujaran kebencian dan bahasa abusif pada Twitter Bahasa Indonesia.
2. Menerapkan pendekatan multi-label classification untuk mendeteksi lebih dari satu label dalam satu tweet.
3. Menggunakan model Transformer IndoBERTweet untuk memahami konteks semantik teks secara lebih akurat.
4. Menyajikan hasil prediksi dengan istilah yang mudah dipahami oleh pengguna awam.
5. Mengevaluasi performa model menggunakan metrik standar seperti Precision, Recall, dan F1-score.

---

## Dataset

Dataset yang digunakan adalah:

**Multi-Label Hate Speech and Abusive Language Detection in Indonesian Twitter**  
oleh Muhammad Okky Ibrohim dan Indra Budi (2019).

### Karakteristik Dataset
- Berisi tweet berbahasa Indonesia
- Menggunakan anotasi multi-label (0 dan 1)
- Memiliki beberapa kategori label sekaligus
- Disertai kamus slang dan daftar kata kasar

### Jumlah Data
- Total data: 13.169 tweet
- Pembagian data:
  - Data latih: 70%
  - Data validasi: 15%
  - Data uji: 15%

---

## Daftar Label dan Penjelasannya

Sistem mendeteksi 12 label berikut:

| Singkatan | Nama Lengkap |
|----------|--------------|
| HS | Ujaran Kebencian |
| Abusive | Bahasa Kasar / Abusif |
| HS_Individual | Ujaran Kebencian terhadap Individu |
| HS_Group | Ujaran Kebencian terhadap Kelompok |
| HS_Religion | Ujaran Kebencian berbasis Agama |
| HS_Race | Ujaran Kebencian berbasis Ras atau Etnis |
| HS_Physical | Ujaran Kebencian berbasis Kondisi Fisik atau Disabilitas |
| HS_Gender | Ujaran Kebencian berbasis Gender atau Orientasi Seksual |
| HS_Other | Ujaran Kebencian Lainnya (penghinaan umum) |
| HS_Weak | Ujaran Kebencian Tingkat Rendah |
| HS_Moderate | Ujaran Kebencian Tingkat Sedang |
| HS_Strong | Ujaran Kebencian Tingkat Tinggi |

Satu tweet dapat memiliki lebih dari satu label secara bersamaan.

---

## Metodologi

Tahapan utama dalam proyek ini meliputi:

1. Pemuatan dan eksplorasi dataset
2. Pra-pemrosesan teks:
   - Case folding
   - Pembersihan URL, mention, dan karakter khusus
   - Normalisasi kata slang
3. Representasi label dalam bentuk vektor multi-label
4. Tokenisasi menggunakan tokenizer IndoBERTweet
5. Pelatihan model Transformer dengan fine-tuning
6. Evaluasi performa model
7. Pengujian dan inferensi pada data baru

---

## Arsitektur Model

Model yang digunakan adalah **IndoBERTweet** dengan konfigurasi sebagai berikut:

- Input: teks tweet
- Encoder: Transformer IndoBERTweet
- Pooling: token [CLS]
- Output layer: fully connected layer
- Fungsi aktivasi output: Sigmoid
- Loss function: Binary Cross Entropy

Pendekatan ini memungkinkan model menghasilkan probabilitas untuk setiap label secara independen.

---

## Hasil Evaluasi

Hasil evaluasi pada data uji menunjukkan performa sebagai berikut:

- F1-score (Micro): 0.81
- F1-score (Macro): 0.66
- Precision (Micro): 0.83
- Recall (Micro): 0.78

Model menunjukkan performa sangat baik pada label dengan jumlah data besar seperti bahasa kasar dan ujaran kebencian umum, serta performa lebih rendah pada label dengan jumlah data sangat sedikit.

---

## Contoh Penggunaan Sistem

Contoh input:
Dasar bodoh, otak udang, gak pantas hidup!

lua
Salin kode

Contoh output:
Bahasa Kasar / Abusif
Ujaran Kebencian
Ujaran Kebencian terhadap Individu
Ujaran Kebencian Tingkat Tinggi

yaml
Salin kode

Hasil ditampilkan menggunakan nama label lengkap agar mudah dipahami oleh pengguna awam.

---

## Teknologi yang Digunakan

- Bahasa Pemrograman: Python
- Framework Deep Learning: PyTorch
- Library NLP: HuggingFace Transformers
- Model: IndoBERTweet
- Lingkungan Pengembangan: Google Colab

---

## Cara Menjalankan Proyek (Ringkas)

1. Clone repository
2. Install dependensi Python
3. Jalankan notebook atau script utama
4. Pastikan runtime menggunakan GPU untuk mempercepat pelatihan
5. Jalankan proses training dan evaluasi
6. Gunakan fungsi prediksi untuk menguji tweet baru

---

## Keterbatasan

- Beberapa label memiliki jumlah data yang sangat sedikit
- Model menggunakan threshold tetap (0.5) untuk semua label
- Tidak mencakup analisis multimedia seperti gambar atau video

---

## Pengembangan Selanjutnya

Beberapa pengembangan yang dapat dilakukan di masa depan:
- Penyesuaian threshold per label
- Penanganan data tidak seimbang dengan class weighting
- Penambahan data atau augmentasi teks
- Integrasi ke dalam aplikasi web atau sistem monitoring media sosial

---

## Lisensi dan Sitasi

Dataset yang digunakan bersifat open source dan dilisensikan untuk penggunaan non-komersial.  
Jika menggunakan dataset ini untuk publikasi, harap mencantumkan sitasi berikut:

Ibrohim, M. O., & Budi, I. (2019). Multi-label Hate Speech and Abusive Language Detection in Indonesian Twitter.

---

## Penutup

Proyek ini menunjukkan bahwa pendekatan multi-label classification dengan model Transformer IndoBERTweet mampu
