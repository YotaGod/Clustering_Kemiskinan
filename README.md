# Clustering Kemiskinan di Indonesia Menggunakan K-Means

Proyek ini bertujuan untuk mengelompokkan provinsi-provinsi di Indonesia berdasarkan rata-rata jumlah penduduk miskin selama periode 2020-2024 menggunakan algoritma _K-Means Clustering_. Proses ini mengikuti beberapa langkah, mulai dari persiapan data hingga evaluasi hasil _clustering_.

## Langkah-langkah Analisis

### Langkah 1: Import Library
Langkah pertama adalah mengimpor semua _library_ Python yang diperlukan untuk analisis, termasuk:
- `pandas` untuk manipulasi data.
- `numpy` untuk operasi numerik.
- `sklearn.preprocessing` untuk normalisasi data.
- `scipy.spatial.distance.euclidean` untuk menghitung jarak Euclidean.
- `sklearn.cluster.KMeans` untuk menerapkan algoritma K-Means.
- `matplotlib.pyplot` dan `seaborn` untuk visualisasi data.
- `sklearn.metrics.silhouette_score` untuk mengevaluasi kualitas _clustering_.
- `google.colab` untuk mengintegrasikan dengan Google Drive.

### Langkah 2: Load Dataset
Dataset yang digunakan adalah data jumlah penduduk miskin per provinsi di Indonesia dari tahun 2020 hingga 2024.

### Langkah 3: Data Understanding
- **Melihat keseluruhan dataset**: Menampilkan 39 baris data yang berisi nama provinsi dan jumlah penduduk miskin dari tahun 2020 hingga 2024. Terdapat beberapa baris dengan data yang tidak valid (bernilai '-').
- **Melihat tipe data**: Memeriksa tipe data setiap kolom. Semua kolom, termasuk kolom tahunan, memiliki tipe data `object` karena adanya nilai non-numerik seperti '-'.

### Langkah 4: Preprocessing
Langkah ini sangat penting untuk membersihkan dan mempersiapkan data sebelum model diterapkan.
- **Cek data duplikat**: Memastikan tidak ada baris data yang duplikat. Hasilnya menunjukkan tidak ada data duplikat.
- **Cek data kosong/null**: Mengidentifikasi nilai-nilai yang hilang atau tidak valid, yang ditandai dengan simbol '-'. Ditemukan 4 baris data yang tidak valid.
- **Pemisahan data**: Data dipisahkan menjadi tiga bagian:
    1. `valid_data`: Data provinsi yang memiliki nilai numerik lengkap.
    2. `invalid_data`: Data provinsi yang memiliki nilai tidak valid ('-').
    3. `jumlah_data`: Data untuk total Indonesia.
- **Perubahan tipe data**: Kolom tahunan dalam `valid_data` diubah dari tipe `object` menjadi `float` agar dapat dihitung secara numerik.
- **Mencari rata-rata**: Menghitung rata-rata jumlah penduduk miskin untuk setiap provinsi dari tahun 2020-2024. Kolom tahunan kemudian dihapus, menyisakan kolom 'Provinsi' dan 'Rata-rata'.
- **Normalisasi data**: Data rata-rata dinormalisasi menggunakan `StandardScaler` dari `scikit-learn` untuk memastikan semua fitur memiliki skala yang seragam, yang penting untuk algoritma K-Means.

### Langkah 5: Elbow Method
- Metode _Elbow_ digunakan untuk menentukan jumlah _cluster_ (k) yang optimal. Grafik _Within-Cluster Sum of Squares_ (WCSS) diplot terhadap jumlah _cluster_ dari 1 hingga 10.
- Dari plot tersebut, titik _elbow_ (siku) yang menunjukkan penurunan WCSS yang signifikan namun mulai melandai, berada di sekitar nilai k=2. Oleh karena itu, k=2 dipilih sebagai jumlah _cluster_ yang optimal.

### Langkah 6: Modeling
- Algoritma K-Means diterapkan pada data yang telah dinormalisasi dengan `k=2`.
- Proses iterasi K-Means ditampilkan untuk menunjukkan bagaimana titik _centroid_ bergeser hingga model konvergen.
- Jarak setiap provinsi ke masing-masing _centroid_ dihitung dan ditampilkan dalam _DataFrame_.
- Hasil _clustering_ (Cluster 0 dan Cluster 1) ditambahkan ke _DataFrame_ `valid_data`.
- Jumlah anggota di setiap _cluster_ dihitung, menunjukkan 31 anggota di Cluster 0 dan 3 anggota di Cluster 1.

### Langkah 7: Visualisasi
- **Scatter Plot Klaster**: Sebuah _scatter plot_ dibuat untuk memvisualisasikan hasil _clustering_. Sumbu X menunjukkan rata-rata jumlah penduduk miskin, sementara sumbu Y mewakili setiap provinsi. Provinsi-provinsi dikelompokkan berdasarkan warna _cluster_ dan titik _centroid_ ditandai dengan tanda 'X'.
- **Pie Chart Proporsi Wilayah**: Sebuah _pie chart_ dibuat untuk menunjukkan proporsi jumlah provinsi dalam setiap _cluster_.

### Langkah 8: Evaluasi Klaster
- **Silhouette Score**: Evaluasi kualitas _clustering_ dilakukan dengan menghitung _Silhouette Score_. Skor ini mengukur seberapa baik setiap objek dikelompokkan dalam _cluster_ yang benar. Skor yang diperoleh adalah 0.892, yang menunjukkan kualitas _clustering_ yang sangat baik.

---
