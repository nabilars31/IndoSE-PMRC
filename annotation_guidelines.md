## Panduan Anotasi Corpus IndoSE

Dokumen ini merupakan panduan operasional (*Annotation Guidelines*) yang digunakan oleh annotator untuk melakukan pelabelan skema **PMRC** (*Problem, Method, Result, Conclusion*) serta kategori tambahan *No_pmrc* pada tingkat kalimat (*sentence-level*) di dalam abstrak artikel ilmiah berbahasa Indonesia pada domain Rekayasa Perangkat Lunak (*Software Engineering*).

### 1. Metodologi Pembentukan Dataset
Dataset **Corpus IndoSE** (total 1.881 kalimat) dibangun melalui proses bertahap untuk menjamin kualitas data yang objektif dan valid sebagai *Gold Standard*:

*   **Tahap 1 (Anotasi Pakar)**
    - Pembuatan standar baku dan acuan dasar (*ground truth*) pelabelan oleh pakar di bidang terkait.
*   **Tahap 2 (Validasi Cohen's Kappa)**
    - Pengukuran *inter-annotator agreement* dilakukan pada 676 kalimat untuk menguji konsistensi pemahaman antar-annotator terhadap panduan ini sebelum pelabelan skala besar dilakukan.
*   **Tahap 3 (Semi-Otomatis & Koreksi Manual)**
    - Sebanyak 1.016 kalimat diproses secara semi-otomatis oleh model awal, kemudian diperiksa ulang dan dikoreksi secara manual oleh annotator manusia.
*   **Tahap 4 (Konsolidasi Akhir)**
    - Sebanyak 189 kalimat sisa diproses secara semi-otomatis dari gabungan data tahap-tahap sebelumnya, lalu dikoreksi kembali secara manual oleh annotator hingga menghasilkan total akumulasi 1.881 kalimat yang bersih dan valid.


### 2. Hasil Uji Reliabilitas (Cohen's Kappa)
Untuk membuktikan bahwa aturan pelabelan dalam panduan ini bersifat objektif dan dapat dipahami secara konsisten, pengujian statistik dilakukan pada dataset Tahap 2 (676 kalimat).

*   Nilai Cohen's Kappa: 0.8525
*   Tingkat Kesepakatan: *Almost Perfect Aggreement*
*   Eksperimen: Proses perhitungan statistik dan matriks kesepakatan antar-annotator dapat diakses melalui link berikut [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1zNsl0HPvW3LJMSkF7Edosdpu6B7Cjond?usp=sharing)

### 3. Definisi dan Aturan Pelabelan
Pelabelan dilakukan pada **level kalimat (sentence-level)**. Jika dalam satu kalimat mengandung lebih dari satu indikasi komponen PMRC, annotator harus menentukan label berdasarkan fokus atau komponen yang paling dominan di dalam kalimat tersebut.

#### A. Problem
*   **Definisi**: Kalimat yang menyatakan latar belakang masalah spesifik, kesenjangan penelitian (*research gap*), tantangan, atau urgensi mengapa penelitian tersebut dilakukan.
*   **Kata Kunci Utama**: *permasalahannya adalah, tantangan dalam, menjadi kendala, sulit untuk, untuk mengatasi, cara atau sistem manual, dll*.
*   **Contoh**: "Sistem Informasi Manajemen Filing di Rumah Sakit masih jarang ditemui, banyak rumah sakit yang masih menggunakan sistem manual dalam pencatatan peminjaman dan pengembalian DRM, sehingga masih banyak terjadi missfile, karena belum terlaksana dengan baik pencatatannya"

#### B. Method
*   **Definisi**: Kalimat yang memuat penjelasan mengenai pendekatan, algoritma, arsitektur sistem, model, instrumen, tahapan proses, atau teknik yang diusulkan atau digunakan untuk menyelesaikan masalah.
*   **Kata Kunci Utama**: *menggunakan metode, diimplementasikan dengan, menggunakan algoritma, mengusulkan arsitektur, menerapkan teknik, dirancang menggunakan, dll*.
*   **Contoh**: "Kami menerapkan model arsitektur IndoBERT-Base dengan optimasi AdamW untuk klasifikasi teks."

#### C. Result 
*   **Definisi**: Kalimat yang menyajikan temuan, produk/sistem yang berhasil dibangun, hasil pengujian, angka performa akurasi, atau observasi utama yang didapatkan setelah eksperimen dijalankan.
*   **Kata Kunci Utama**: *hasil pengujian menunjukkan, memperoleh akurasi sebesar, aplikasi ini berhasil, menaikkan performa hingga, hasil menunjukkan, dll*.
*   **Contoh**: "Model yang diusulkan berhasil mencapai nilai akurasi sebesar 89,5% pada dataset pengujian."

#### D. Conclusion 
*   **Definisi**: Kalimat yang berisi kesimpulan akhir, implikasi teoritis atau praktis, kontribusi nyata dari penelitian, atau saran untuk pengembangan di masa depan.
*   **Kata Kunci Utama**: *kesimpulan dari, penelitian ini berkontribusi pada, diharapkan dapat membantu, disimpulkan bahwa, untuk penelitian selanjutnya, dll*.
*   **Contoh**: "Dapat disimpulkan bahwa pendekatan semi-otomatis mampu memangkas waktu anotasi tanpa menurunkan kualitas data."

#### E. No_pmrc
*   **Definisi**: Kalimat pendukung atau komplementer yang tidak mengandung esensi dari keempat komponen PMRC di atas. Umumnya berupa kalimat latar belakang bidang ilmu yang terlalu umum, informasi administratif, lokasi/waktu penulisan, atau kalimat sapaan/terima kasih.
*   **Kata Kunci Utama**: *perkembangan teknologi saat ini, saat ini rekayasa perangkat lunak, penulis mengucapkan terima kasih, studi ini dilakukan di, dll*.
*   **Contoh**: "Di era digital saat ini, perkembangan aplikasi perangkat lunak berbasis mobile berkembang sangat pesat."

### 4. Protokol Resolusi Ketidaksepakatan (Disagreement Resolution)

Anotator manusia bertindak sebagai **hakim tertinggi** (*highest judge*) dalam menentukan keabsahan label. Jika terjadi perbedaan pendapat antar-annotator atau perbedaan antara anotator dengan prediksi model semi-otomatis, aturan berikut wajib diterapkan:

1.  **Prioritas Konteks**: Baca kalimat sebelum dan sesudahnya untuk memahami konteks paragraf abstrak secara utuh sebelum memutuskan label.
2.  **Anulir Model**: Meskipun model semi-otomatis memberikan prediksi dengan tingkat keyakinan (*confidence score*) yang tinggi, jika annotator secara kontekstual menilai prediksi tersebut keliru, maka **keputusan manual annotator yang mutlak benar** dan hasil model harus dianulir.
3.  **Konsolidasi Panel**: Jika terjadi jalan buntu (*deadlock*) perbedaan pendapat antar-annotator manusia, resolusi akan diselesaikan melalui diskusi bersama pakar ketiga untuk menentukan label final.
