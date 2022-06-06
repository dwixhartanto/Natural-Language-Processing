## **INDONESIA MOVIE RECOMMENDER SYSTEM**

### **Project Overview**

**Latar Belakang**

Era digital ditandai ledakan informasi digital yang menimbulkan masalah dalam temu kembali informasi. Mesin pencari mempunyai keterbatasan pada kata kunci/query yang diingat pengguna. 

Industry perfilman dunia merupakan salah satu industry yang  tidak terpengaruh dengan maraknya hiburan digital seperti munculnya media social, program televisi yang beragam dan game. Industry film yang terus melakukan produksi ini semakin menambah informasi film yang melimpah di internet. Kondisi ini justru membuat para penikmat film menjadi kebingungan ketika harus memilih film kesukaannya

Menurut situs [Facts.net](https://facts.net/netflix-facts/) "Di tahun 2019 Netflix menghabiskan anggaran sekitar $1.5 Billion untuk riset dan development". Salah satunya untuk pembuatan sistem rekomendasi movie supaya user menemukan film sejenis yang telah ditonton dan disukai sehingga betah menghabiskan waktu bersama Netflix.

Sistem rekomendasi sendiri merupakan sebuah solusi yang bisa memberikan referensi yang bersifat personal dengan mempelajari penilaian pengguna terhadap item yang pernah dipilihnya.

Dari latar belakang diatas, penulis memilih domain proyek  ***Sistem Rekomendasi Film Indonesia***
### **Business Understanding**

Sistem rekomendasi memprediksi rating atau preferensi pengguna terhadap item tertentu. Rekomendasi ini dibuat berdasarkan perilaku pengguna di masa lalu atau perilaku pengguna lainnya. Jadi, sistem ini akan merekomendasikan sesuatu terhadap pengguna berdasarkan data perilaku atau preferensi dari waktu ke waktu. 

**Problem Statement**

Bagaimana cara membangun model machine learning untuk merekomendasikan sebuah film yang mungkin disukai pengguna?

**Goal**

Membuat sebuah Sistem Rekomendasi agar memudahkan pengguna mencari judul film yang mirip dengan film yang sudah ditonton sebelumnya atau mencari judul film yang mungkin disukai pengguna dan sebelumnya belum pernah di tonton pengguna.

**Solution**

Untuk menyelesaikan masalah ini, penulis menggunakan teknik content-based filtering. Berikut adalah penjelasan teknik tersebut yang akan digunakan untuk masalah ini :

Content-Based Filtering : Merupakan cara untuk memberi rekomendasi bedasarkan genre atau fitur pada item yang disukai oleh pengguna. Content-based filtering mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna.
    

### ***Data Understanding***

##### **Informasi Dataset**
Dataset yang digunakan diambil dari [Kaggle](https://www.kaggle.com/dimitriirfan/indonesian-film-industry-most-made-genre/), dimana data tersebut merupakan hasil scraping data IMDB Film Indonesia dari tahun 1926 sampai tahun 2020. Terdiri dari 1 csv yaitu indonesian_movies.csv.
berikut kolom yang ada di data csv tersebut.

![img01.png](https://github.com/dwixhartanto/Natural-Language-Processing/blob/main/Indonesia%20Movie%20Recommender/img/img01.png?raw=true)

Adapun dataset tersebut mempunya 11 kolom, dengan penjelasan dibawah ini :

*   title : Judul Film
*   year : Tahun terbit film
*   description : Ringkasan 
*   genre : Genre Film
*   rating : Rating film
*   users_rating : Rating dari user
*   votes  : Nilai hasil polling
*   languages : Bahasa di film
*   directors : Sutradara film
*   actors : Pemain di film
*   runtime : Durasi film



###### **Sebaran atau Distribusi Data pada Fitur yang Digunakan**
Berikut merupakan visualisasi data yang menunjukkan sebaran/distribusi data pada beberapa variabel yang akan penulis gunakan nanti:

**Year dan User Rating**

![img02.png](https://github.com/dwixhartanto/Natural-Language-Processing/blob/main/Indonesia%20Movie%20Recommender/img/img02.png?raw=true)

![img03.png](https://github.com/dwixhartanto/Natural-Language-Processing/blob/main/Indonesia%20Movie%20Recommender/img/img03.png?raw=true)

Dari grafik dan sebaran statistik diatas dapat kita ketahui bahwa :  
1. Year (Tahun rilis) film terbanyak ada di tahun 2020, dan terendah di tahun 1926
2. User rating tertinggi nilainya 9.4 dan terendah 1.2

**Genre**

![img04.png](https://github.com/dwixhartanto/Natural-Language-Processing/blob/main/Indonesia%20Movie%20Recommender/img/img04.png?raw=true)

Genre terbanyak di film indonesia adalah drama, dan genre terendahnya adalah history

**10 Film dengan User Rating Tertinggi**

![img05.png](https://github.com/dwixhartanto/Natural-Language-Processing/blob/main/Indonesia%20Movie%20Recommender/img/img05.png?raw=true)

Film dengan rating user tertinggi adalah : 
Horas Amang : Tiga Bulan Untuk Selamanya

## **Data Preparation**

Data preparation diperlukan untuk mempersiapkan data agar ketika nanti dilakukan proses pengembangan model diharapkan akurasi model akan semakin baik dan meminimalisir terjadinya bias pada data. Berikut ini merupakan tahapan-tahapan dalam melakukan data preparation :

**Memilih Feature yang digunakan**

Membuat dataframe baru yang berisi judul dan genre

**Mengatasi Missing Value**

Terdapat missing value sejumlah 36 di kolom genre, oleh karena itu kita drop baris yang ada nilai kosong tersebut dengan menggunakan fungsi .dropna()

**Mendrop Data Duplicate**

Mendrop data duplicate pada judul

**Mereset Index**

Mereset urutan index agar terurut kembali


### **Modeling dan Hasil**

Model yang dibuat menggunakan algoritma Content-Based Filtering dan menggunakan teknik TF-IDF Vectorizer dan Cosine Similarity. TF-IDF Vectorizer digunakan untuk merepresentasikan fitur penting dari setiap genre film yang tersedia. 

Fungsi tfidfvectorizer() digunakan untuk melakukan perhitungan idf dari setiap genre, kemudian melakukan fit dan transformasi vektor TF-IDF ke dalam bentuk matriks menggunakan fungsi todense(). Cosine similarity digunakan untuk menghitung derajat kesamaan antar film dari library sklearn. Setelah itu kita buat model rekomendasi film dengan parameter :

    judul : Judul Film
    similarity_data : Dataframe mengenai similarity (cosine_sim)
    Items : Nama dan fitur yang digunakan untuk mendefinisikan kemiripan, dalam hal ini adalah 'judul' dan 'genre'.
    k : Banyak rekomendasi yang ingin diberikan.

Pada model machine learning ini akan melakukan pencarian film yang memiliki genre sama atau mirip dengan film "Headshot".

Berikut hasil dari 10 rekomendasi film yang memiliki genre sama dengan film "Headshot" :

![rekomn.png](https://i.ibb.co/x1LxCWk/rekomn.png)

Dari gambar diatas, model dapat merekomendasikan 10 film dengan genre yang sama dengan film 'Headshot' yaitu genre 'Action' 


## **Evaluation**

Pada evaluasi model ini penulis menggunakan metrik precision content based filtering untuk menghitung precision model sistem telah dibuat sebelumnya.

Berikut ini adalah rumusnya:

![140904619-1de3fb26-be15-4c97-a10d-84f7a7a69b00.png](https://i.ibb.co/wpsWr1d/140904619-1de3fb26-be15-4c97-a10d-84f7a7a69b00.png)


Penulis menghitung total prediksi rekomendasi berdasarkan genre yang benar dibagi dengan total rekomendasi yang telah diberikan. penulis menggunakan metrik ini karena ingin mengetahui apakah model yang dipakai untuk content-based filtering dapat memprediksi semua konten bedasarkan genre dengan benar.

Adapun hasil ujicobanya : 

![Screenshot_64.png](https://i.ibb.co/qrv2G01/rec.png)

Hasil analisisnya :
Dari gambar di atas dapat dilihat bahwa semua film yang direkomendasikan oleh sistem memiliki genre yang sama dengan film 'Soekarno: Indonesia Merdeka' yaitu genre 'Biography'
Precission = 10/10.
Precission = 1 
berdasarkan rumus Precision maka dapat disimpulkan bahwa model ini memiliki precision 100%
