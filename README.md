# Laporan Proyek Machine Learning - Syafirna Miftahul Jannah

## Project Overview
Dalam industri *platform streaming*, tantangan utama adalah menyediakan rekomendasi yang personal kepada pengguna dari katalog film yang besar. Platform streaming harus memastikan bahwa konten yang direkomendasikan sesuai dengan preferensi pengguna untuk menjaga kepuasan pelanggan dan meningkatkan efisiensi operasional. Masalah utama yang dihadapi anpa rekomendasi yang akurat, pengguna dapat merasa kewalahan dengan pilihan yang tersedia, yang dapat mengurangi tingkat kepuasan dan meningkatkan risiko churn pelanggan.
implementasi teknik *collaborative filtering* menjadi kunci untuk meningkatkan kualitas rekomendasi dan memastikan relevansi konten yang ditawarkan kepada pengguna, menjaga kepuasan pelanggan, serta meningkatkan efisiensi operasional *platform streaming*[1]. untuk itu permasalahan ini memiliki urgensi yang sangat mendesak, Urgensi Permasalahan ini adalah :
- Peningkatan Persaingan: Industri platform streaming sangat kompetitif. Kemampuan untuk memberikan rekomendasi yang personal dan relevan dapat menjadi pembeda utama di pasar.
- Skala Data yang Besar: Dengan jutaan pengguna dan ribuan film, tantangan dalam mengelola dan menganalisis data untuk menghasilkan rekomendasi yang akurat semakin besar.
- Kepuasan dan Retensi Pengguna: Pengguna yang merasa puas dengan rekomendasi yang diberikan lebih cenderung untuk tetap menggunakan platform, mengurangi risiko churn dan meningkatkan retensi pelanggan.
- Efisiensi Operasional: Mengelola katalog film yang terus berkembang memerlukan sistem yang efisien dan scalable untuk memproses dan menganalisis data dalam jumlah besar.

Implementasi machine learning berupa recomendation system dengan collaborative filterring perlu dilakukan karna sistem ini akan mempertibangkan preferensi pengguna secara historisnya. untuk itu rekomendasi yang lebih sesuai akan meningkatkan kepuasan pengguna. sehingga pengguna akan cendrung lebih menggunakan platform. selain itu pada sisi operational pembuatan sistem ini akan membantu keefisienan proses. Penelitian telah menunjukkan bahwa *collaborative filtering* efektif dalam meningkatkan akurasi rekomendasi dengan mempertimbangkan preferensi pengguna dan interaksi historis [2].

## Business Understanding
Dalam konteks *platform streaming*, sistem rekomendasi yang efektif dapat menghadirkan manfaat signifikan bagi perusahaan:
- Peningkatan Retensi Pelanggan: Dengan menyediakan rekomendasi yang sesuai, perusahaan dapat meningkatkan tingkat retensi pelanggan.
- Penghematan Biaya: Mengurangi biaya akuisisi pelanggan baru dengan mempertahankan pelanggan yang ada.
- Optimalisasi Pengalaman Pengguna: Memberikan pengalaman pengguna yang lebih personal dan menyenangkan dengan rekomendasi yang relevan.

Stakeholder dan Sasaran
- Manajemen Perusahaan: Menggunakan analisis dan hasil rekomendasi untuk mendukung keputusan strategis.
- Tim Teknologi dan Data: Mengembangkan dan mengimplementasikan solusi teknis untuk meningkatkan sistem rekomendasi.
- Tim Pemasaran dan Layanan Pelanggan: Menggunakan wawasan dari sistem rekomendasi untuk meningkatkan strategi pemasaran dan layanan pelanggan.

### Problem Statements
- Bagaimana cara memastikan pengguna dapat menemukan rekomendasi film yang sesuai dengan minat mereka dari banyaknya film di* platform streaming* ?
- Bagaimana *platform streaming* dapat mempersonalisasikan rekomendasi film dengan mempertimbangkan preferensi pengguna yang beragam ?

### Goals
- Mengembangkan sistem rekomendasi yang dapat memprediksi preferensi film pengguna dengan akurasi tertinggi dari 3 algoritma rekomendasi yang akan dibandingkan, setelah dilatih dengan data yang digunakan. 
- Meningkatkan skalabilitas dan efisiensi sistem rekomendasi untuk menangani volume besar data pengguna dan pembaruan katalog film sehingga sistem rekomendasi dapat menghasilkan rekomendasi dalam waktu singkat dalam hitungan detik

### Solution statements
- Membandingkan beberapa algoritma yang dinilai cocok untuk rekomendasi sistem dengan *colaborative filterring* untuk mendapatkan rekomendasi yang relevan untuk pengguna perdasarkan preferensi perngguna.
- Menerapkan teknik *collaborative filtering* seperti SVD, KNNBasic, dan NMF untuk menganalisis interaksi pengguna-film dan menghasilkan rekomendasi film yang dipersonalisasi.

## Data Understanding
1. *Data Ghatering*. Dataset diunduh dari public dataset Grouplens dengan perinta "!wget" untuk mengunduh file dari internet kelingkungan kerja lokal, setelahnya dilakukan proses unzip pada file sehingga file dalam bentuk CSV dapat diolah pada dataframe. Dataset yang digunakan adalah [MovieLens Latest Datasets 100.000](https://grouplens.org/datasets/movielens/latest/)
2. *Data Asessing*. atau penilaian pada data dilakukan dengan :
  - Proyek ini menggunakan dua dataframe utama yaitu ratings.csv dan movies.csv. Dataframe ratings.csv digunakan untuk menyimpan informasi tentang rating yang diberikan oleh pengguna, sedangkan dataframe movies.csv digunakan untuk menyimpan informasi detail tentang film yang diberi rating. Kedua dataframe ini digabungkan berdasarkan variabel movieId untuk membuat satu dataframe gabungan yang memuat semua kolom dari kedua dataframe tersebut.
  - Info dari *dataframe* untuk melihat gambaran tetang jumlah *non-null values* dari setiap kolom dalam *dataframe*. Hal ini membantu dalam memahami struktur data dan identifikasi awal terhadap kolom-kolom yang memiliki *missing values*. data yang dibutuhkan dalam 2 dataframe, maka dilakukan proses merge dengan pandas pada kedua data frame. variabel ini akan memuat semua colum dari movie.csv dan rating.csv berdasarkan movieId.
  - Melihat jumlah *missing value* pada *dataframe* untuk mengetahui jumlah nilai yang hilang pada setiap kolom, sehingga dapat diputuskan langkah selanjutnya untuk menghapus kolom/row sebelum dianalisis lebih lanjut. Tidak ditemukan *missing value* pada data.
  - Melihat jumlah data *duplicated* pada *dataframe* untuk mengetahui data yang sama lebih dari 1, hal ini dilakukan untuk memastikan integritas data. Duplikasi yang ditemukan akan dihapus agar tidak mempengaruhi analisis dan model prediksi yang akan dibuat. tidak didapatkan data duplicate.
3. *Exploratory data analysis*(EDA).Visualisasi ini membantu kita memahami bagaimana pengguna menilai film berdasarkan genre. Ini memberikan wawasan yang berguna untuk membuat sistem rekomendasi yang lebih efektif dengan mempertimbangkan kecenderungan rating pada setiap genre.
    
  Gambar 1.Box PLot Distribusi rating
  ![Distribusi rating boxplot](https://github.com/Smjfirna/Movie_recommendation-system/assets/142133715/3908d570-d4f9-4748-97d6-43b18029ee92)
  
  - Rating Median Tertinggi:Film-Noir dan Documentary menunjukkan median rating yang relatif tinggi, mendekati atau sekitar 4. Drama dan War juga memiliki median rating yang cukup tinggi.
  - Rating Median Terendah: Horror memiliki median rating yang lebih rendah dibandingkan genre lainnya, mendekati atau di bawah 3.Genre seperti Children dan Comedy memiliki median rating yang sedikit lebih rendah dibandingkan genre lain, namun masih berada di sekitar 3.
  - Distribusi Rating: Horror menunjukkan rentang distribusi yang luas, dari rating 1 hingga 5, menunjukkan variasi besar dalam penilaian pengguna.Genre seperti Comedy dan Children juga menunjukkan rentang distribusi yang cukup lebar, meskipun tidak se-luas Horror.
  - Outliers: Hampir setiap genre memiliki outliers di bagian bawah (rating 1), menunjukkan bahwa ada beberapa film dalam setiap genre yang mendapatkan rating sangat rendah. Outliers juga terlihat di bagian atas (rating 5), menunjukkan ada beberapa film dalam setiap genre yang sangat disukai.
  - Genre dengan Rating Konsisten: Drama, War, dan Film-Noir cenderung memiliki distribusi yang lebih konsisten dan tidak terlalu banyak outliers dibandingkan genre lain.
  - Popularitas Genre: Genre seperti Adventure, Animation, Action, Sci-Fi, dan Fantasy memiliki rentang rating yang cukup konsisten, biasanya berkisar antara 3 hingga 4.
  - Genre Terbaik untuk Direkomendasikan: Film dalam genre Film-Noir, Documentary, Drama, dan War umumnya mendapat rating yang lebih tinggi, sehingga bisa menjadi fokus dalam rekomendasi untuk pengguna yang menyukai kualitas film yang tinggi.
  - Genre dengan Rating Beragam: Film Horror menunjukkan rating yang sangat beragam, jadi jika merekomendasikan film horror, perlu dipastikan bahwa film tersebut memang memiliki rating yang tinggi untuk menghindari rekomendasi film dengan kualitas rendah.
  - Genre Populer: Genre seperti Adventure, Animation, dan Sci-Fi cenderung disukai oleh pengguna, tetapi distribusi rating mereka menunjukkan adanya variasi. Memilih film dengan rating di atas median dalam genre ini akan meningkatkan kepuasan pengguna.

### Variabel-variabel pada MovieLens Latest Datasets 100.000 adalah sebagai berikut:
1. ratings.csv
File ini berisi data rating yang diberikan oleh pengguna terhadap berbagai film di platform streaming. Variabel-variabel dalam file ini adalah sebagai berikut:
  - userId : *String* unik untuk mengidentifikasi setiap user. Variabel ini digunakan untuk melacak siapa yang memberikan rating.
  - movieId : *String* unik untuk mengidentifikasi setiap film. Variabel ini digunakan untuk menentukan film mana yang telah dinilai oleh pengguna.
  - rating :  peringkat yang diberikan pengguna untuk film yang telah toton pada platform streaming film(Interval : 0.5 - 5.0) menunjukkan preferensi pengguna terhadap film tertentu.
  - timestamp : waktu pengguna memberikan rating pada film. Meskipun variabel ini berguna untuk analisis temporal, dalam proyek ini, fokus kita adalah pada pola interaksi pengguna-film melalui rating, sehingga variabel ini tidak digunakan dalam model collaborative filtering.
2. movies.csv
File ini berisi informasi detail tentang film yang ada di dataset. Variabel-variabel dalam file ini adalah sebagai berikut:
  - movieId : *String* unik untuk mengidentifikasi setiap film. Variabel ini digunakan untuk menghubungkan data film dengan data rating.
  - tittle : Judul film yang memberikan infomrmasi deskripsi pada film. Variabel ini memberikan informasi deskriptif tentang film, tetapi tidak digunakan langsung dalam proses collaborative filtering.
  - genres : Genre atau kategori film. Variabel ini juga memberikan informasi deskriptif yang dapat berguna untuk analisis lebih lanjut atau metode rekomendasi yang berbeda, tetapi tidak digunakan dalam model collaborative filtering ini.

## Data Preparation
1. Memastikan format data yang sesuai
  Sebelum melakukan pemodelan, penting untuk memastikan bahwa format data sesuai dengan yang diharapkan. Kami menggunakan fungsi info() untuk memeriksa tipe data. Variabel userId dan movieId harus berbentuk integer agar sesuai dengan model collaborative filtering. Karena kedua variabel tersebut sudah berbentuk integer, tidak perlu dilakukan encoding tambahan. Ini memastikan bahwa data siap untuk digunakan dalam model collaborative filtering tanpa memerlukan transformasi tambahan.
2. Cek Karakteristik Data
Kami melakukan pengecekan jumlah userId, movieId, dan analisis statistik rating menggunakan fungsi len(), min(), dan max() untuk memahami karakteristik data yang digunakan:
  - Jumlah Pengguna: Menghitung jumlah unik userId untuk mengetahui berapa banyak pengguna yang ada dalam dataset.
  - Jumlah Film: Menghitung jumlah unik movieId untuk mengetahui berapa banyak film yang ada dalam dataset.
  - Nilai Minimum dan Maksimum Rating: Mengetahui rentang nilai rating yang diberikan oleh pengguna, dengan minimum rating 0.5 dan maksimum rating 5.0.
3. Split Data
Membagi data menjadi data pelatihan dan data uji sangat penting untuk mengevaluasi performa model pada data yang belum pernah dilihat sebelumnya. Langkah-langkah yang dilakukan adalah:
  - Menentukan Skala Rating: Menggunakan Reader dari pustaka Surprise untuk menentukan skala rating dari 0.5 hingga 5.0. Langkah ini penting untuk memastikan bahwa sistem memahami rentang rating yang digunakan dalam dataset.
  - Membuat Dataset Akhir: Menggunakan Dataset.load_from_df dari pustaka Surprise untuk memuat data yang telah diformat ke dalam dataframe dengan kolom userId, movieId, dan rating. Langkah ini penting untuk mempersiapkan data dalam format yang dapat digunakan oleh algoritma rekomendasi di pustaka Surprise.
  - Membagi Data: Menggunakan train_test_split dari pustaka Surprise untuk membagi data menjadi set pelatihan (80%) dan set pengujian (20%), dengan pengaturan random_state untuk memastikan reproducibility. Pembagian data ini penting untuk melatih model pada set pelatihan dan menguji performa model pada set pengujian yang belum pernah dilihat sebelumnya. Pemisahan data ini membantu dalam mengevaluasi kemampuan generalisasi model.

## Modeling
1. Algoritma Yang Dibandingkan
  - Singular Value Decomposition(SVD)
    - Deskripsi: SVD adalah teknik dekomposisi matriks yang digunakan untuk memprediksi rating yang hilang dalam matriks pengguna-film.
    - Kelebihan: Efisien untuk menangani dataset besar, menghasilkan rekomendasi yang akurat, dan mampu menangani data yang jarang (sparse data).
    - Kekurangan: Memerlukan penyesuaian hyperparameter yang cermat untuk hasil optimal, bisa menjadi kurang akurat jika ada perubahan preferensi pengguna yang dinamis.
    - Cara Kerja pada Dataset: SVD memecah matriks rating pengguna-film menjadi tiga matriks yang lebih kecil untuk menemukan hubungan laten antara pengguna dan film. Model ini menggunakan informasi ini untuk memprediksi rating yang belum diberikan oleh pengguna.
    - Alasan Penggunaan: SVD cocok untuk masalah ini karena mampu menangani data yang besar dan jarang dengan baik. Dengan memanfaatkan pola laten dalam data, SVD dapat memberikan rekomendasi yang akurat.
  - KNN (K-Nearest Neighbors)
    - Deskripsi: KNNBasic adalah metode berbasis memori yang menggunakan kemiripan antara pengguna atau item untuk membuat prediksi.
    - Kelebihan: Mudah diimplementasikan, tidak memerlukan pelatihan model, dan bekerja dengan baik untuk dataset kecil.
    - Kekurangan: Tidak efisien untuk dataset besar, karena memerlukan perhitungan kemiripan untuk setiap prediksi, dan performanya bisa menurun jika data sangat jarang.
    - Cara Kerja pada Dataset: KNNBasic menghitung kemiripan antara pengguna atau film berdasarkan rating yang diberikan. Kemudian, ia menggunakan rating dari tetangga terdekat untuk memprediksi rating yang hilang.
    - Alasan Penggunaan: KNN digunakan sebagai pembanding karena kesederhanaannya dan kemampuannya untuk menangani dataset kecil dengan baik. Namun, metode ini mungkin kurang efisien untuk dataset besar.
  - NMF (Non-Negative Matrix Factorization)
    - Deskripsi: NMF adalah teknik dekomposisi matriks yang membatasi faktor-faktor laten dan representasi data agar tidak negatif.
    - Kelebihan: Dapat menghasilkan representasi yang lebih interpretatif, bekerja dengan baik pada data jarang, dan menghindari nilai negatif dalam dekomposisi.
    - Kekurangan: Memerlukan lebih banyak iterasi untuk konvergensi dibandingkan SVD, dan hasilnya bisa sensitif terhadap nilai awal.
    - Cara Kerja pada Dataset: NMF memecah matriks rating pengguna-film menjadi dua matriks non-negatif yang lebih kecil untuk menemukan pola laten dalam data. Model ini menggunakan informasi ini untuk memprediksi rating yang hilang.
    - Alasan Penggunaan: NMF dipilih untuk menghindari nilai negatif dalam dekomposisi dan memberikan representasi yang lebih interpretatif dari data. NMF juga bekerja dengan baik pada data yang jarang.
2. Tahapan Pemodelan
  - Inisialisasi Model. setelah dilakukan pembagian dataset. model yang akan digunakan di inisialisasi setelah sebelumnya mengimport library surprice dan semua algoritma yang digunakan yaitu SVD, KNNBasic dan NMF
  - Training model. model dilatih menggunakan dataset trainset untuk kemudian dievaluasi untuk melihat seberapa efektif model memprediski menggunakan data testset.
3. Berdasarkan hasil pelatihan dan evaluasi, model terbaik untuk menangani masalah rekomendasi film pada dataset ini adalah Singular Value Decomposition (SVD). SVD telah menunjukkan hasil akurasi yang lebih baik dari dua algoritma lainnya dan evaluasi lainnya yang juga unggul. Model ini memberikan rekomendasi yang lebih akurat dengan mempertimbangkan pola laten dalam data rating pengguna.
4. Top-N Reccomendation. disajikan  dengan memilih userId secara acak kemudian model akan mengidentifikasi film yang sudah di tonton dan ratingnya yang kemudian menggunakan model SVD yang sudah dilatih sebelumnya untuk memprediksi rating film yang belum ditonton dan memberikan 10 rekomendasi film dengan prediksi rating tertinggi untuk direkomendasikan kepada pengguna. film ditampilkan dengan judul dan genre.

Tabel 1. Contoh Tabel Top-N dari User 12
Showing recommendations for user: 12
===========================
Movies with high ratings from user
--------------------------------
| Title                        | Genre                       |
|------------------------------|-----------------------------|
| Emma (1996)                  | Comedy|Drama|Romance        |
| She's All That (1999)        | Comedy|Romance              |
| 10 Things I Hate About You (1999) | Comedy|Romance          |
| Never Been Kissed (1999)     | Comedy|Romance              |
| Love Actually (2003)         | Comedy|Drama|Romance        |

--------------------------------
Top 10 movie recommendations
--------------------------------
| Title                                     | Genre                              |
|-------------------------------------------|------------------------------------|
| Braveheart (1995)                         | Action|Drama|War                   |
| Star Wars: Episode IV - A New Hope (1977) | Action|Adventure|Sci-Fi            |
| Pulp Fiction (1994)                       | Comedy|Crime|Drama|Thriller        |
| Forrest Gump (1994)                       | Comedy|Drama|Romance|War           |
| Schindler's List (1993)                   | Drama|War                          |
| Silence of the Lambs, The (1991)          | Crime|Horror|Thriller              |
| Fargo (1996)                              | Comedy|Crime|Drama|Thriller        |
| Reservoir Dogs (1992)                     | Crime|Mystery|Thriller             |
| Star Wars: Episode V - The Empire Strikes Back (1980) | Action|Adventure|Sci-Fi |
| Apocalypse Now (1979)                     | Action|Drama|War                   |

## Evaluation
1. Tabel Evaluasi Model
Tabel 2. Hasil Evaluasi

| Model	   | RMSE  |
|----------|-------|
|SVD	     | 0.856 |
|KNNBasic	 | 0.924 |
|NMF	     | 0.891 |

2. Interpretasi Hasil Metrik
  - RMSE (Root Mean Squared Error): Merupakan ukuran seberapa baik model kolaboratif (collaborative filtering) bekerja dalam memprediksi rating atau preferensi pengguna untuk item tertentu. Semakin rendah RMSE, semakin baik performa model.
  - Model SVD memiliki RMSE terendah yaitu 0.856, menunjukkan performa prediksi yang lebih baik dibandingkan dengan KNNBasic (RMSE = 0.924) dan NMF (RMSE = 0.891).
  - KNNBasic memiliki RMSE tertinggi, menunjukkan performa prediksi yang lebih rendah dibandingkan dengan SVD dan NMF.
3. Analisis Hasil
Berdasarkan evaluasi di atas, model SVD menunjukkan kinerja yang lebih baik dalam memprediksi preferensi atau rating pengguna terhadap item-item dalam dataset. Meskipun NMF memiliki RMSE yang sedikit lebih baik dibandingkan KNNBasic, namun SVD tetap unggul dalam hal performa prediksi.
4. Test rekomendasi film berdasarkan satu user menggunakan Algoritma SVD
Dalam implementasi tersebut diambil 10 film dengan prediksi rating tertinggi yang belum ditonton oleh user. selanjutnya juga diambil 5 film dengan rating tertinggi yang diberikan yang pernah ditonton oleh user untuk memberikan gambaran lebih lanjut tentang preferensinya. Rekomendasi ini dapat membantu meningkatkan pengalaman pengguna dalam menemukan film-film yang sesuai dengan preferensi mereka berdasarkan analisis dari model kolaboratif SVD yang telah dievaluasi sebelumnya.
5. Kesimpulan
  - Keberhasilan Proyek: Meskipun model KNNBasic dan NMF memberikan hasil yang dapat diterima dengan RMSE di bawah 1.0, model SVD menonjol dengan RMSE 0.856, mencerminkan prediksi yang lebih akurat.
  - Pencapaian Goals: Goals proyek untuk membangun model kolaboratif yang mampu memprediksi preferensi pengguna tercapai dengan baik, terutama dengan pilihan model SVD.
  - Penyelesaian Problem: Model SVD memberikan solusi yang cukup efektif dalam menyelesaikan masalah prediksi preferensi atau rating pengguna pada item tertentu. Evaluasi dengan menggunakan RMSE memberikan gambaran yang jelas tentang performa model dalam konteks dataset yang digunakan.

# Reference
[1] Putri, H. D., & Faisal, M. (2023). Analyzing the effectiveness of collaborative filtering and content-based filtering methods in anime recommendation systems. Jurnal Komtika (Komputasi dan Informatika), 7(2), 124-133.

[2] Al-Ghamdi, M., Elazhary, H., & Mojahed, A. (2021). Evaluation of collaborative filtering for recommender systems. International Journal of Advanced Computer Science and Applications, 12(3).

[3] Salloum, S., & Rajamanthri, D. (2021). Implementation and evaluation of movie recommender systems using collaborative filtering. Journal of Advances in Information Technology, 12(3).
