# Laporan Proyek Machine Learning - Roni Merdiansah

## Project Overview

Beralihnya tren game dari *game console* menjadi *digital game* merubah cara pendistribusian game tersebut. Game digital diakui memiliki banyak keunggulan
dibandingkan game console, diantaranya; mudah diakses, bersifat *online*, dll. Pendistribusian game digital dilakukan melalui platform-platform tertentu. 
Banyaknya genre game yang ada juga membuat para pemain bingung dalam memilih game apa yang akan mereka mainkan. Salah satu cara untuk mengatasi masalah tersebut 
adalah menggunakan Sistem Rekomendasi pada setiap platform game.

Sistem rekomendasi adalah aplikasi perangkat lunak yang bertujuan untuk mendukung pengguna dalam pengambilan keputusan saat berinteraksi dengan ruang informasi
yang besar. Sistem rekomendasi membantu mengatasi masalah informasi yang berlebihan dengan mengekspos pengguna ke item yang paling menarik, terbaru, dan relevan 
[[Fasiha Ikram, 2022](https://www.hindawi.com/journals/sp/2022/6084363/)]. Sistem ini akan merekomendasikan game berdasarkan genre yang pemain sukai, ataupun
berdasarkan game apa yang sedang tren saat itu.

## Business Understanding

### Problem Statements

Bagaimana cara merekomendasikan game yang dimainkan pemain lain dapat direkomendasikan kepada pemain lainnya juga?

### Goals

Dapat membuat sistem rekomendasi yang akurat berdasarkan ratings dan aktivitas pemain pada masa lalu.

### Solution statements

Proyek ini menggunakan 2 algoritma Machine Learning sistem rekomendasi sebagai solusi, diantaranya :

* *Content Based Filtering*: adalah algoritma yang merekomendasikan game serupa dengan genre yang disukai pemain, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit.
* *Collaborative Filtering*: adalah algoritma yang bergantung pada pendapat komunitas pengguna, tidak memerlukan atribut untuk setiap itemnya.

Algoritma Content Based Filtering digunakan untuk merekemondesikan game berdasarkan aktivitas pemain pada masa lalu, sedangkan algoritma Collabarative Filltering digunakan untuk merekomendasikan game berdasarkan rating yang paling tinggi.

## Data Understanding

Dataset ini berisi data penjualan video game dari seluruh dunia, di berbagai platform, genre, dan wilayah. Dataset ini memberikan informasi tentang apa yang dianggap sebagai game hit di industri game saat ini [[Discovering Hidden Trends in Global Video Games](https://www.kaggle.com/datasets/thedevastator/discovering-hidden-trends-in-global-video-games)]. Meskipun dataset ini merupakan data penjualan game, pada proyek ini akan mencoba menggunakan data yang ada untuk membuat sistem rekomendasi. Adapun total data ini berjumlah 1907.

### Variable

Variabel-variabel pada Discovering Hidden Trends in Global Video Games dataset adalah sebagai berikut:
- `Rank`	Peringkat game dalam hal penjualan global. (Int)
- `Game Title` : Judul game. (String)
- `Platform` : Platform tempat game dirilis. (String)
- `Year` : Tahun game dirilis. (Integer)
- `Genre` : Genre game. (String)
- `Publisher` : Penerbit game. (String)
- `North America` : Penjualan game di Amerika Utara. (Integer)
- `Europe` : Penjualan game di Eropa. (Integer)
- `Japan` : Penjualan game di Jepang. (Integer)
- `Rest of World` : Penjualan game di seluruh dunia. (Integer)
- `Global` : Total penjualan game secara global. (Integer)
- `Review` : Skor ulasan game. (Float)

### Exploratory Data Analysis

![](https://github.com/Dapperson/Machine-Learning-Terapan/blob/main/Proyek%20Akhir/Variabel%20Kategorik.png)

Dari visualisasi diatas didapatkan beberapa *insight* diantaranya
- Platform yang paling sering merilis game adalah PS2
- Perusahaan penerbit paling banyak adalah Nintendo
- Game dengan genre **Sport** paling banyak dibuat
- Jumlah game dirilis tertinggi pada tahun 2008
- Untuk rating paling rendah adalah 30.0 dan paling tinggi adalah 97.0

## Data Preparation
Terdapat beberapa tahapan yang dilakukan sebelum membuat model sistem rekomendasi. Adapun tahapan nya sebagai berikut:

1. **Membuat Fitur `User_ID`** : Data ini tidak memiliki fitur user_id, maka diasumsikan bahwa setiap baris yang ada pada kolom adalah user_id, sehingga setiap index pada baris di labeli sebagai user_id.
2. **Memilih Fitur** : Data ini merupakan data penjualan dan ini adalah proyek membuat sistem rekomendasi, maka dilakukan pemilihan fitur terlebih dahulu guna mempermudah dalam membuat model. Fitur yand dipilih sebagai berikut:
 - `User_ID` 
 - `Game Title`	
 - `Platform`	
 - `Year`	
 - `Genre`	
 - `Publisher` 
 - `Review`
3. **Format Ulang Fitur** : Melakukan pembulatan bilangan pada kolom `Review`
4. **Membuat Fitur `Game_ID`** : Sama seperti sebelumnya, dataset ini tidak memiliki fitur game_id sehingga diasumsikan bahwa setiap nilai *Unique* pada `Game Title` adalah game_id kemudian melabelinya
5. **Menghapus Duplikasi Data** : Menghilangkan data duplikasi berdasarkan fitur `Game_ID`
6. **Membuat Dictionary** : Dilakukan untuk membuat DataFrame baru dengan beberapa fitur saja
7. **Membuat DataFrame** : DataFrame yang dibuat hanya berisikan beberapa fitur saja untuk keperluan pembuatan model
8. **Mengaplikasikan TF-IDF Vectorizer** : Menghitung bobot setiap kata terhadap data yang ada
9. **Menghitung Cosine Similarity** : Bertujuan untuk mengetahui nilai kemiripan antar data

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
