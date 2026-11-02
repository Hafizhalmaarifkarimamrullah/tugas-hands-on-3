# Tugas Hands-On 3: Pandas Lanjutan

**Nama:** Hafizh Al Ma'arif Karim Amrullah  
**NIM:** 24552011137  
**Kasus yang Dipilih:** 03 — Product Recommendation (E-Commerce)  
**Dataset:** `case3_ecommerce_transactions.csv` (10.000 baris)

---

## 📌 Ringkasan Proyek
Proyek ini merupakan bagian dari Tugas Hands-On 3 yang berfokus pada alur kerja *Data Wrangling* dan persiapan *Machine Learning* menggunakan dataset transaksi E-Commerce (`case3_ecommerce_transactions.csv`). 

Secara garis besar, proyek ini mencakup beberapa tahapan utama:
1. **Audit & Pembersihan Data:** Melakukan audit kualitas pada 10.000 baris data untuk mendeteksi *missing value*, duplikat, dan *outlier*. Data dibersihkan dengan normalisasi teks (memperbaiki *typo* pada sentimen ulasan), imputasi statistik, dan penanganan nilai ekstrem menggunakan metode IQR, tanpa mengorbankan integritas target klasifikasi.
2. **Feature Engineering:** Membuat fitur turunan yang lebih kaya informasi, seperti `total_revenue` (pendapatan bersih), indikator `is_returned`, ekstraksi fitur waktu (bulan, hari libur/akhir pekan), serta pembuatan target klasifikasi biner (`is_high_rating`).
3. **Exploratory Data Analysis (EDA):** Menganalisis pola data melalui visualisasi untuk menemukan tren musiman pendapatan, tingkat pengembalian barang (*return rate*) per kategori, dan korelasi antar fitur numerik.
4. **Analisis RFM (Recency, Frequency, Monetary):** Melakukan segmentasi pelanggan untuk mengidentifikasi pelanggan bernilai tinggi (VIP) guna mendukung strategi retensi bisnis.
5. **Pemodelan Machine Learning (Anti-Leakage):** Mempersiapkan data untuk model menggunakan `train_test_split` dengan stratifikasi, dan membangun `ColumnTransformer` (scaling & encoding) yang *fit*-nya hanya dilakukan pada data latih (*train*) untuk mencegah kebocoran data (*data leakage*). Model yang dilatih mencakup **Klasifikasi** (memprediksi kepuasan pelanggan) dan **Clustering K-Means** (segmentasi karakteristik produk).

Seluruh proses *end-to-end* ini diimplementasikan menggunakan Python dengan pustaka utama **Pandas** (manipulasi data), **Scikit-Learn** (pemodelan dan *preprocessing*), serta **Matplotlib & Seaborn** (visualisasi) di lingkungan Google Colab.

---

## 💡 3 Temuan Utama & Rekomendasi Actionable
Berdasarkan hasil analisis data eksploratif (EDA), analisis RFM, dan pemodelan, terdapat tiga temuan krusial yang dapat ditindaklanjuti oleh manajemen:

### 1. Tingginya Tingkat Retur (Return Rate) pada Kategori Tertentu
*   **Fakta Data:** Tingkat pengembalian barang (retur) secara keseluruhan mencapai 22,46%. Berdasarkan grafik, kategori Kecantikan memiliki *return rate* tertinggi (mendekati 24%). Hal ini juga diperkuat oleh distribusi rating, di mana mayoritas pelanggan memberikan rating di bawah 4 (hanya ~24% yang merekomendasikan produk).
*   **Dampak Bisnis:** Tingginya retur mengurangi profitabilitas dan membebani biaya logistik balik, serta mengindikasikan ketidakpuasan pelanggan.
*   **Rekomendasi Aksi:** Lakukan audit kualitas produk secara menyeluruh pada kategori Kecantikan. Perbaiki deskripsi produk, foto, dan ekspektasi pengiriman agar tidak terjadi kesalahpahaman yang memicu retur.

### 2. Terdapat Segelintir Pelanggan VIP (Analisis RFM)
*   **Fakta Data:** Dari analisis RFM (Recency, Frequency, Monetary), ditemukan bahwa sebagian besar pelanggan hanya bertransaksi 1-2 kali, namun terdapat segelintir pelanggan (Top 5) yang menyumbang pendapatan (Monetary) sangat besar hingga ratusan juta rupiah.
*   **Dampak Bisnis:** Pelanggan VIP ini adalah aset berharga. Jika mereka berpindah ke kompetitor, pendapatan perusahaan akan turun drastis.
*   **Rekomendasi Aksi:** Terapkan strategi retensi khusus (seperti program *Membership* atau *Loyalty Program*). Berikan voucher eksklusif atau layanan prioritas bagi pelanggan dengan skor Monetary dan Frequency tertinggi.

### 3. Pola Musiman pada Pendapatan (Revenue)
*   **Fakta Data:** Grafik *time series* (Revenue Bulanan) menunjukkan pola fluktuatif dengan lonjakan penjualan yang jelas pada pertengahan tahun (sekitar kuartal 3) dan akhir tahun (kuartal 4).
*   **Dampak Bisnis:** Lonjakan ini bisa menjadi peluang emas jika diantisipasi, namun bisa menjadi masalah jika stok barang tidak siap.
*   **Rekomendasi Aksi:** Alihkan alokasi anggaran pemasaran (*marketing budget*) secara agresif pada bulan-bulan menjelang periode puncak tersebut. Pastikan juga manajemen rantai pasok (*supply chain*) menyiapkan stok produk *Best Seller* lebih awal.

---

## 🚀 Cara Menjalankan Notebook
1. Buka file `notebook.ipynb` menggunakan **Google Colab**.
2. Upload file dataset `case3_ecommerce_transactions.csv` ke dalam folder `data/` di panel Files Colab.
3. Klik menu **Runtime** > **Restart and Run all**.
4. Notebook akan berjalan dari atas ke bawah (Load Data -> Cleaning -> EDA -> RFM -> Modeling).
5. Hasil output (data bersih, kamus data, laporan kualitas) akan otomatis tersimpan di folder `output/` dan root Colab.

## 📁 Struktur Folder
Berikut adalah struktur direktori untuk pengumpulan tugas ini:

```text
tugas-hands-on-3/
├── README.md                  # Ringkasan: kasus, temuan, cara menjalankan
├── notebook.ipynb             # Notebook utama (dapat dijalankan dari atas ke bawah)
├── laporan_kualitas.csv       # Tabel perbandingan kualitas data sebelum vs sesudah
│
├── data/
│   └── case3_ecommerce_transactions.csv  # Dataset asli (format CSV)
│
└── output/
    ├── data_bersih.csv        # Hasil pembersihan data
    └── kamus_data.csv         # Kamus data: kolom, tipe, n_missing, n_unik