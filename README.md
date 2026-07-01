## IndoSE-PMRC Classification
Repositori ini berisi implementasi model klasifikasi struktur retoris (PMRC: Problem, Method, Result, Conclusion) pada abstrak penelitian bahasa Indonesia menggunakan model IndoBERT. Eksperimen ini bertujuan untuk mengekstrak dan mengklasifikasikan informasi kunci dari dokumen akademis secara otomatis untuk mendukung efisiensi analisis literatur.

### 1. Anotasi & Dataset (Corpus IndoSE)
Dataset **Corpus IndoSE** disusun melalui proses anotasi yang teliti untuk memastikan kualitas Gold Standard. Proses pembentukan dataset dilakukan dalam empat tahap sistematis:
- **Tahap 1 (Anotasi Pakar):** Anotasi manual dilakukan oleh pakar pada dataset awal untuk menetapkan standar pelabelan.
- **Tahap 2 (Validasi Cohen's Kappa):** Pengukuran inter-annotator agreement menggunakan Cohen’s Kappa dilakukan pada 676 data untuk memastikan konsistensi pelabelan.
- **Tahap 3 (Semi-Otomatis & Koreksi):** Sebanyak 1.016 data diproses secara semi-otomatis oleh model awal, kemudian dikoreksi secara manual oleh anotator.
- **Tahap 4 (Konsolidasi):** Sebanyak 189 data diproses secara semi-otomatis dari gabungan data tahap sebelumnya, yang kemudian dikoreksi kembali secara manual oleh anotator. Hasil koreksi dari 189 data ini digabungkan dengan data dari Tahap 2 dan Tahap 3, sehingga membentuk Consolidated Training Dataset final dengan total 1.881 kalimat.

**Definisi Label PMRC:**
- Problem: Pernyataan masalah atau urgensi topik.
- Method: Pendekatan, algoritma, instrumen, atau teknik yang digunakan.
- Result: Temuan, hasil eksperimen, atau observasi utama.
- Conclusion: Kesimpulan akhir, implikasi, atau kontribusi penelitian.
- No_pmrc: Kalimat pendukung yang tidak memiliki relevansi langsung dengan struktur PMRC.

### 2. Spesifikasi Teknis
- Model Base: IndoBERT-Base (`indobenchmark/indobert-base-p1`)
- Tokenizer: `BertTokenizerFast` (Hugging Face) untuk proses tokenisasi teks tingkat tinggi yang cepat dan efisien.
- Arsitektur Klafikasi: `BertForSequenceClassification` yang dikonfigurasi khusus untuk klasifikasi (PMRC + No_pmrc).
- Dataset: IndoSE Corpus (1.881 kalimat teranotasi)
- Framework: `transformers` (Hugging Face), `PyTorch`, `pandas`, `nltk`


### 3. Eksperimen (Fine-Tuning)
Eksperimen dilakukan untuk melatih model IndoBERT agar memahami pola struktur retoris dalam abstrak. Model yang telah dilatih (fine-tuned) disimpan sebagai checkpoint (`indobert-pmrc.zip`) yang siap untuk digunakan dalam tahap inferensi.

### 4. Alur Kerja Inferensi
Tahap ini dilakukan untuk memvalidasi model pada data abstrak baru. Sistem memproses abstrak menjadi struktur terklasifikasi melalui tahapan berikut:

- Segmentasi: Abstrak utuh dipecah menjadi unit kalimat individual menggunakan sentence tokenizer.
- Tokenisasi: Kalimat diubah menjadi format numerik (input IDs dan attention masks) agar dapat diproses oleh arsitektur IndoBERT.
- Klasifikasi: Model melakukan inferensi untuk menentukan label PMRC terbaik bagi setiap kalimat.
- Post-processing: Hasil klasifikasi beserta confidence score disusun ke dalam tabel terstruktur untuk memudahkan verifikasi manual.


### 5. Panduan Menjalankan Eksperimen
Eksperimen ini dirancang untuk dijalankan di Google Colab. Ikuti langkah berikut:

- Persiapan: Unduh seluruh file dari repositori ini ke komputer Anda.
- Unggah ke Colab:
    - Buka Google Colab.
    - Buka panel Files (ikon folder di sebelah kiri).
    - Drag and drop seluruh file (.ipynb, .zip, .xlsx) ke dalam panel tersebut. Tunggu hingga proses unggah selesai 100%.
- Eksekusi:
    - Buka `indobert_classification.ipynb`.
    - Jalankan sel kode secara berurutan (Run All).
    - Saat mencapai sel Inference, pilih metode input (manual atau Excel) sesuai kebutuhan Anda.
- Output: Setelah proses selesai, sistem akan menampilkan tabel hasil dan secara otomatis mengunduh prediction_results.xlsx ke perangkat Anda.



