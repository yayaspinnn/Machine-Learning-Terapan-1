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

* *Content Based Filtering*: adalah algoritma yang merekomendasikan item serupa dengan apa yang disukai pengguna, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit.
* *Collaborative Filtering*: adalah algoritma yang bergantung pada pendapat komunitas pengguna. Dia tidak memerlukan atribut untuk setiap itemnya.

Algoritma Content Based Filtering digunakan untuk merekemondesikan game berdasarkan aktivitas pengguna pada masa lalu, sedangkan algoritma Collabarative Filltering digunakan untuk merekomendasikan game berdasarkan ratings yang paling tinggi.

## Data Understanding

Dataset ini berisi data penjualan video game dari seluruh dunia, di berbagai platform, genre, dan wilayah. Dataset ini memberikan informasi tentang apa yang dianggap sebagai game hit di industri game saat ini [[Discovering Hidden Trends in Global Video Games](https://www.kaggle.com/datasets/thedevastator/discovering-hidden-trends-in-global-video-games)]. Adapun total data ini berjumlah 1907.

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

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

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
