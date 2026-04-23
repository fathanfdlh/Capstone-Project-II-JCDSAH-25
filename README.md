# Capstone-Project-II-JCDSAH-25

# Customer Segmentation Analysis pada Supermarket

## Pendekatan RFM, Demografi, dan Efektivitas Kampanye untuk Mendukung Strategi Pemasaran

## Table of Contents

- [Latar Belakang](#introduction)
- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [Technologies Used](#technologies-used)
- [How to Run the Project](#how-to-run-the-project)

## Introduction

Dalam lanskap ritel supermarket yang sangat kompetitif, kesuksesan tidak hanya diukur dari peningkatan penjualan, tetapi juga kemampuan untuk mempertahankan pelanggan dan mengimplementasikan strategi pemasaran yang tepat sasaran. Setiap pelanggan memiliki keunikan dalam latar belakang demografi, perilaku belanja, dan respons terhadap promosi. Oleh karena itu, pendekatan universal tidak lagi efektif.

Proyek ini bertujuan untuk menganalisis perilaku pelanggan menggunakan pendekatan **Recency, Frequency, dan Monetary (RFM)** sebagai dasar segmentasi, dikombinasikan dengan data demografi dan analisis respons kampanye pemasaran. Melalui segmentasi ini, diharapkan perusahaan dapat mengidentifikasi pelanggan bernilai tinggi, pelanggan berisiko hilang, serta mengevaluasi efektivitas kampanye promosi untuk setiap segmen.

## Problem Statement

Bagaimana perusahaan supermarket dapat mengembangkan segmentasi pelanggan yang efektif dengan memanfaatkan analisis RFM, data demografi, dan respons terhadap kampanye pemasaran dalam meningkatkan ketepatan strategi pemasaran, retensi pelanggan, dan nilai bisnis?

## Dataset

Dataset 'Supermarket Customers' berisi 28 kolom yang mencakup informasi pribadi pelanggan (ID, Tahun Lahir, Pendidikan, Status Pernikahan, Pendapatan, Jumlah Anak, Tanggal Pendaftaran, Recency, Keluhan), pengeluaran produk (Anggur, Buah, Daging, Ikan, Manisan, Emas), promosi (Jumlah Pembelian dengan Diskon, Respons Kampanye 1-5, Respons Kampanye Terakhir), dan tempat pembelian (Pembelian Web, Katalog, Toko, Kunjungan Web Bulanan).

## Methodology

Proyek ini mengikuti langkah-langkah berikut:

1.  **Data Understanding:** Memahami struktur data, tipe data, dan mengidentifikasi anomali awal seperti missing values dan inkonsistensi penamaan kolom.
2.  **Data Cleaning & Formatting:**
    *   Menyeragamkan nama kolom ke format *snake_case*.
    *   Mengubah tipe data `dt_customer` menjadi datetime.
    *   Melakukan text formatting dan konsistensi pada kolom `education` dan `marital_status`.
    *   Menangani missing values pada kolom `income` dengan imputasi median.
    *   Menangani outliers pada kolom `year_birth` dengan membuat fitur `age` dan menghapus data yang tidak relevan (> 80 tahun).
3.  **Feature Engineering:**
    *   Menciptakan fitur `age_group` dari `age`.
    *   Mengelompokkan `marital_status` dan `education` ke dalam kategori yang lebih bermakna.
    *   Menghitung `total_spent` (Monetary), `total_purchase` (Frequency), `total_accepted_cmp`, dan `total_children`.
    *   Mengidentifikasi `preferred_channel` dan menghitung `deal_ratio` serta `deal_segment`.
    *   Membuat `recency_segment`.
4.  **RFM Feature dan Segmentasi:**
    *   Menghitung `r_score`, `f_score`, dan `m_score` menggunakan `pd.qcut`.
    *   Menggabungkan skor menjadi `rfm_score`.
    *   Menerapkan fungsi segmentasi RFM (`Champions`, `Loyal Customers`, `Potential Loyalist`, `Cannot Lose Them`, `Hibernating`).
5.  **Exploratory Data Analysis (EDA):**
    *   **Demographic Analysis by RFM Segment:** Menganalisis distribusi usia, jumlah anak, pendapatan, tingkat pendidikan, dan status pernikahan untuk setiap segmen RFM.
    *   **Campaign Effectiveness Analysis:** Menganalisis rata-rata pengeluaran, tingkat respons kampanye, dan rata-rata penerimaan kampanye berdasarkan `deal_segment` dan `rfm_segment`.
    *   Melakukan uji hipotesis (Uji-T dan Chi-Squared) untuk menguji hubungan antara segmen promo dengan pengeluaran dan respons kampanye, serta Uji ANOVA untuk membandingkan rata-rata penerimaan kampanye dan pengeluaran antar segmen RFM.

## Key Findings

*   **Champions** dan **Loyal Customers** adalah segmen paling bernilai, dengan pengeluaran dan frekuensi pembelian tinggi, respons kampanye yang baik, serta ketergantungan rendah terhadap diskon. Mereka didominasi oleh usia produktif (Middle-Aged, Young Adult, Adult), berpendidikan tinggi (Bachelor, PhD, Master), dan mayoritas berstatus 'In Relationship'. Produk wine adalah produk yang paling banyak dibeli.
*   **Potential Loyalist** memiliki potensi besar untuk menjadi pelanggan setia. Mereka cukup responsif terhadap kampanye dan lebih sensitif terhadap diskon.
*   **Cannot Lose Them** adalah pelanggan dengan rata-rata pengeluaran tertinggi namun sudah tidak aktif. Mereka kurang responsif terhadap kampanye dan diskon, menunjukkan strategi diskon kurang efektif untuk segmen ini.
*   **Hibernating** adalah segmen terbesar namun kontribusinya paling rendah, dengan pengeluaran dan respons kampanye yang rendah, serta ketergantungan tinggi pada diskon.
*   Penggunaan promo (`deal_segment`) memiliki asosiasi signifikan dengan nilai pelanggan dan respons kampanye. Pelanggan `Low Promo Usage` cenderung memiliki nilai belanja lebih tinggi, sementara `High Promo Usage` memiliki nilai belanja lebih rendah.

## Recommendations

1.  **Champions:** Pertahankan loyalitas melalui program eksklusif (VIP program, penawaran premium, layanan pelanggan prioritas). Fokus pada pengalaman non-diskon untuk menjaga margin.
2.  **Loyal Customers:** Berikan nilai konsisten dan dorong mereka menjadi 'Champions' melalui akses awal produk atau penawaran personalisasi.
3.  **Potential Loyalist:** Konversi menjadi pelanggan setia dengan penawaran menarik namun strategis. Gunakan diskon sebagai pendorong, dikombinasikan dengan nilai tambah seperti poin loyalitas ekstra atau bundle eksklusif.
4.  **Cannot Lose Them:** Identifikasi alasan ketidakaktifan melalui komunikasi langsung (personal email, customer service). Hindari diskon dan fokus pada aktivasi kembali berdasarkan riwayat pembelian masa lalu.
5.  **Hibernating:** Gunakan promosi dan diskon (flash sale, cuci gudang, kupon) untuk menarik perhatian kembali, dengan pertimbangan ROI yang ketat. Tawarkan diskon terbatas waktu atau promo untuk produk yang sering dibeli sebelumnya.
6.  **Strategi Berdasarkan Deal Segment:**
    *   **Low Promo Usage:** Tawarkan penawaran eksklusif berfokus pada kualitas, kenyamanan, dan pengalaman (produk premium, layanan VIP).
    *   **Medium Promo Usage:** Kombinasikan diskon moderat dengan manfaat tambahan (poin reward). Uji berbagai jenis promosi.
    *   **High Promo Usage:** Pertahankan promosi, arahkan ke pembelian volume lebih besar (misalnya, beli 2 gratis 1) atau perkenalkan produk dengan margin lebih baik melalui diskon terbatas.

## Technologies Used

*   Python
*   Pandas (for data manipulation and analysis)
*   NumPy (for numerical operations)
*   Matplotlib (for static visualizations)
*   Seaborn (for statistical data visualization)
*   Plotly Express (for interactive visualizations)
*   SciPy (for statistical tests like Chi-Squared, T-test, ANOVA)
*   Regular Expressions (re) for text processing

## How to Run the Project

1.  Clone this repository:
    ```bash
    git clone <repository_url>
    ```
2.  Navigate to the project directory:
    ```bash
    cd customer-segmentation-supermarket
    ```
3.  Install the required dependencies:
    ```bash
    pip install pandas numpy matplotlib seaborn plotly scikit-learn scipy
    ```
4.  Open the Jupyter Notebook or Google Colab file:
    `Supermarket Customer Segmentation Analysis.ipynb` (or similar name)
    ```
6.  Run all cells in the notebook to reproduce the analysis and results.
```
