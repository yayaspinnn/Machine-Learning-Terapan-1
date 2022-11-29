# Laporan Proyek Pertama: Predictive Analytics - Roni Merdiansah

## Domain Proyek

Saat ini tinggal di sebuah apartemen sudah menjadi gaya hidup masyarakat urban, hal ini disebabkan karena banyaknya fasilitas yang ditawarkan di sebuah apartemen. Apalagi saat ini banyaknya apartemen yang dibangun di pusat kota ataupun pusat bisnis, sehingga dapat memudahkan bagi mereka para profesional muda untuk beraktivitas [(Tim Editorial Rumah.com, 2022)](https://www.rumah.com/panduan-properti/bisnis-apartemen-69876). Kelengkapan fasilitas yang dimiliki tiap apartemen sangat mempengaruhi dalam mengklasifikasikan apartemen itu sendiri. Proyek yang dilakukan saat ini akan mempelajari klasifikasi yang sudah ada sebelumnya pada dataset dengan pendekatan *Machine Learning*.

## Business Understanding

### Problem Statements

Sebuah hal penting untuk mengetahui fasilitas seperti apa yang dapat mempengaruhi kualitas sebuah apartemen. Hal ini akan sangat membantu seseorang yang ingin memulai bisnis apartemen. Berikut beberapa rumusan masalah yang akan kita cari tahu:
- Seberapa akurat klasifikasi yang ada sebelumnya pada dataset?
- Fasilitas apa saja yang sangat berpengaruh terhadap peng-klasifikasian itu?

### Goals

Adapun tujuan dari proyek ini sebagai berikut:
- Melatih model klasifikasi dengan jumlah 4 model dan mencaritahu model mana yang memiliki akurasi paling bagus terhadap kolom target, dan menjadikan kolom lain sebagai fitur.
- Mencaritahu ada berapa fasilitas penting yang memiliki presentase tinggi terhadap kolom target, dengan cara mengambil model yang memiliki kemampuan membaca presentase setiap fitur dengan baik.

## Data Understanding

Data ini merupakan data imajiner [Paris Housing](https://www.kaggle.com/datasets/aleshagavrilov/parishousing) (Apartemen Paris) dari tahun 1990-2021. Meskipun imajiner data ini cukup bagus untuk digunakan dalam proyek ini. Data ini berisi karakteristik dari setiap apartemen di Paris seperti lokasi, fasilitas, dan harga. Data ini memiliki total 1000 data.

### Variabel

Paris Housing memiliki 17 variabel sebagai berikut:

1. `squareMeters` : Luas Tanah (numerik-m2)
2. `numberOfRooms` : Jumlah Ruangan per-Apartemen (Teks Angka dalam bahasa inggris)
3. `floors` : Jumlah Lantai Apartemen (numerik)
4. `cityCode` : Kode Pos (numerik-Kategorikal)
5. `cityPartRange` : Jarak ke Kota (numerik-m2)
6. `numPrevOwners` : Berapa Kali sudah ditempati sebelumnya (numerik)
7. `made` : Tahun dibangun (numerik-Tahun)
8. `isNewBuilt` : Baru/Direnovasi (Biner-Ya/Tidak)
9. `hasStormProtector` : Penangkal Petir (Biner-Ya/Tidak)
10. `basement` : Ruang Bawah tanah (numerik)
11. `attic` : Loteng (numerik)
12. `garage` : Garasi (numerik)
13. `hasStorageRoom` : Gudang (numerik)
14. `hasGuestRoom` : Ruang Tamu (numerik)
15. `price` : Harga (numerik)
16. `category` : Kategori (numerik)
17. `PoolAndYard` : Kolam Renang & Taman (Kategorikal)

### Exploratory Data Analysis

1. analisis kolom `category`

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Presentase%20Category.png)

2. analisis kolom numerik

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Variabel%20Numerik.png)

3. analisis kolom kategorikal & biner

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Variabel%20Kategorikal.png)


Dari beberapa visualisasi yang dilakukan didapatkan beberapa insight sebagai berikut:

- Mayoritas `category` adalah *Basic* dengan presentase sebesar 87%, dan *Luxury* adalah 13%
- Hampir semua fitur pada kolom numerikal memiliki rata-rata yang sama antara `category` *Basic* dan *Luxury* seperti perbandingan pada presentase sebelumnya, tidak terdapat perbedaan yang signifikan pada nilai tertentu
- Begitu juga pada kolom kategorikal & biner, tidak terdapat perbedaan yang signifikan antar sub kolom, hampir semuanya memiliki perbandingan yang sama.


## Data Preparation

### Data Cleaning

Pada tahap ini dilakukan pembersihan pada data-data yang tidak memiliki informasi yang berarti, seperti bernilai null atau kosong. Setelah dilakukan pemeriksaan pada dataset, didapatkan bahwa datanya bersih dan tidak ada yang null, atau cacat.

### Feature Engineering

#### Delete Unnecessary Features

Karena model yang akan dibuat disini adalah klasifikasi, maka diperlukan mengeliminasi beberapa fitur yang tidak diperlukan. adapaun fitur yang akan dieliminasi adalah `cityCode` dan `made`.

#### Reformatting String
Sebelumnya pada fitur `numberOfRooms` merupakan Teks Angka dalam bahasa inggris, maka harus diubah dahulu menjadi numerik agar fitur dapat digunakan pada saat pemodelan *Machine Learning*

#### Encoding

*Encoding* perlu dilakukan agar fitur selain numerik dapat ikut digunakan pada saat pemodelan *Machine Learning* dengan cara melabeli setiap nilainya, karena *Machine Learning* hanya bisa menggunakan nilai numerik. Untuk fitur `category` yang merupakan kolom target akan diaplikasikan dengan *LabelEncoder*, dimana nilai *Basic* menjadi `0` dan nilai *Luxury* menjadi `1`

Sedangkan untuk kolom kategorikal dan biner lainnya akan diaplikasikan dengan *OneHotEncoder*, karena kolom-kolom ini merupakan input feature. Didapatkan beberapa fitur baru hasil *OneHotEncoder* sebagai berikut:

- `isNewBuilt_False`
- `isNewBuilt_True`
- `hasStormProtector_False`
- `hasStormProtector_True`
- `hasStorageRoom_False`
- `hasStorageRoom_True`
- `PoolAndYard_has pool and has yard`	
- `PoolAndYard_has pool and no yard`	
- `PoolAndYard_no pool and has yard`	
- `PoolAndYard_no pool and no yard`

Dimana setiap fitur memiliki nilai `0` dan `1`

### Feature Selection

Adapun fitur target yang digunakan seperti yang sudah dibahas sebelumnya yaitu kolom `category`. Karena pada tahap sebelumnya sudah dilakukan eliminasi fitur, dan juga telah melakukan tahap *Encoding* sehingga terdapat penambahan fitur, sehingga jumlah akhir dari fitur input adalah 20.


## Modeling

### Split Data

Pembagian untuk data latih adalah 80% atau 8000 data, dan data test adalah 20% atau 2000 data.

### Basis Model

Disini akan menggunakan 10 basis model untuk mencari tahu perbandingan model mana yang memiliki akurasi paling bagus, adapun 10 model itu sebagai berikut:

- DecisionTreeClassifier

Decision tree membangun model klasifikasi dan regresi dalam bentuk struktur pohon. Algoritma ini menguraikan kumpulan data menjadi himpunan bagian yang lebih kecil dan menghubungkannya menjadi pohon keputusan yang terkait. Tujuan utama dari algoritma decision tree adalah untuk membangun model pelatihan yang digunakan untuk memprediksi nilai variabel target dengan mempelajari aturan keputusan. Aturan ini disimpulkan dari data training yang sebelumnya telah diinput. Keuntungan algoritma ini adalah mudah dimengerti, mudah menghasilkan aturan, tidak mengandung hiper-parameter, dan model decision tree yang kompleks dapat disederhanakan secara signifikan dengan visualisasinya.

- RandomForestClassifier

Algoritma Random Forest Classifier merupakan salah satu algoritma klasifikasi machine learning yang paling populer. Seperti namanya, algoritma ini bekerja dengan cara membuat hutan pohon secara acak. Semakin banyak pohon yang dibuat, maka hasilnya akan semakin akurat. Dasar dari algoritma random forest adalah algoritma decision tree. Keuntungan dari algoritma ini adalah dapat digunakan untuk rekayasa fitur seperti mengidentifikasi fitur yang paling penting diantara semua fitur yang tersedia dalam dataset training, bekerja sangat baik pada database berukuran besar, sangat fleksibel, dan memiliki akurasi yang tinggi.

- GaussianNB

Naive bayes classifier merupakan algoritma klasifikasi yang sangat sederhana berdasarkan apa yang disebut pada teorema bayesian. Algoritma ini memiliki satu sifat umum, yaitu setiap data diklasifikasikan tidak bergantung pada fitur lain yang terikat pada kelas atau biasa disebut dengan independen. Artinya, satu data tidak berdampak pada data yang lain. Meskipun algoritma ini merupakan algoritma yang tergolong sederhana, namun naive bayes dapat mengalahkan beberapa metode klasifikasi yang lebih canggih. Algoritma ini biasa digunakan untuk deteksi spam dan klasifikasi dokumen teks. Kelebihan algoritma ini adalah sederhana dan mudah diterapkan, tidak sensitif terhadap fitur yang tidak relevan, cepat, hanya membutuhkan sedikit data training, dan dapat digunakan untuk masalah klasifikasi multi-class dan biner.

- SVC

Support Vector Machine atau biasa dikenal dengan algoritma SVM adalah algoritma machine learning yang digunakan untuk masalah klasifikasi atau regresi. Namun, aplikasi yang paling sering digunakan adalah masalah klasifikasi. Algoritma SVM banyak digunakan untuk mengklasifikasikan dokumen teknis misalnya spam filtering, mengkategorikan artikel berita berdasarkan topik, dan lain sebagainya. Keuntungan algoritma ini adalah cepat, efektif untuk ruang dimensi tinggi, akurasi yang bagus, powerful dan fleksibel, dan dapat digunakan di banyak aplikasi.

Didapatkan data pada kolom target sebelumnya tidak seimbang (imbalance) jumlah antara *Basic* dan *Luxury*, maka pada proyek ini menggunakan _Cross Validation - Stratified K Fold_. Konsep dari Cross Validation - Stratified K Fold sendiri adalah validasi silang antara data latih dan data test, dimana sejumlah data yang pernah menjadi data latih akan di posisikan menjadi data test, begitu pun sebaliknya. Validasi silang ini dilakukan tergantung jumlah _n_ yang dimasukkan. Pada proyek ini menggunakan jumlah _n_ sebanyak 2. Setelah membuat basis model didaptkan 2 model terbaik yang memiliki akurasi sempurna sebagai berikut:

- DecisionTreeClassifier
- RandomForestClassifier

Confusion Matrix

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Confusion%20Matrix.png)

Kedua model tersebut dapat membaca model dengan baik dengan nilai
- True Positive = `4367`
- True Negative = `633`
- False Positive = `0`
- False Negative = `0`

Salah satu tujuan proyek ini adalah mencari tahu fitur penting yang sangat berpengaruh terhadap klasifikasi, maka diantara kedua model tersebut yang paling banyak mendeteksi fitur penting adalah *RandomForestClassifier*

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Feature%20Importance%20RFC.png)

## Evaluasi

Untuk memastikan kembali model yang dipilih tidak ada kesalahan, maka pada tahap evaluasi ini melakukan _Hyperparameter Tuning_ dengan menggunakan _GridSearchCV_. GridSearchCV berfungsi untuk melakukan permutasi terhadap semua parameter yang kita inputkan pada model untuk mencari parameter terbaik. Setelah melakukan Hyperparameter Tuning didapatkan parameter terbaik 

Best Score: 1.0
Best Hyperparameters: 
- criterion : gini
- max_depth : 5
- max_features : auto
- n_estimators : 200}

dengan matriks kebingungan dari data test sebagai berikut

![](https://raw.githubusercontent.com/Dapperson/Machine-Learning-Terapan/main/Submission%201/Confusion%20Matrix%20HT.png)

- True Positive = `1744`
- True Negative = `256`
- False Positive = `0`
- False Negative = `0`

Dengan demikian dapat disimpulkan bahwa kolom `category` meng-klasifikasikan apartemen dengan sempurna antara apartemen *Basic* (Biasa) dengan apartemen *Luxury* (Mewah), dimana faktor yang sangat berpengaruh dalam peng-klasifikasian itu adalah dari *apakah apartemen itu baru di bangun/direnovasi* dan juga *apakah apartemen itu memiliki fasilitas taman ataupun kolam renang*.
