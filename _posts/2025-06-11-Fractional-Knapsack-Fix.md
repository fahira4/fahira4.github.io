---
title: FRACTIONAL KNAPSACK
date: 2025-05-06
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]     # TAG names should always be lowercase
---

![Desktop View](https://res.cloudinary.com/codecrucks/images/f_webp,q_auto/v1634623105/fractional-knapsack/fractional-knapsack.jpg?_i=AA){: width="500"}
_---_

Dalam dunia nyata, kita sering dihadapkan pada situasi di mana kita harus memilih item dari berbagai pilihan yang memiliki nilai dan berat berbeda, tetapi kita dibatasi oleh kapasitas tertentu. Bayangkan kamu sedang berkemas untuk mendaki gunung—kamu hanya bisa membawa tas dengan kapasitas tertentu, namun kamu ingin mengisinya dengan barang-barang bernilai tinggi. Bagaimana cara memilih barang agar total nilai yang dibawa maksimal?

Masalah inilah yang dijawab oleh **Fractional Knapsack Problem**.

Berbeda dengan **0/1 Knapsack** di mana item hanya bisa diambil seluruhnya atau tidak sama sekali, pada **Fractional Knapsack** kita diizinkan mengambil sebagian dari suatu item. Ini membuat masalah bisa diselesaikan secara **greedy** (rakus) karena kita bisa memilih bagian terbaik dari item berdasarkan nilai per satuan berat (*value per weight*).

### Definisi

**Fractional Knapsack** adalah varian dari masalah Knapsack di mana kita dapat mengambil **pecahan (fraksi)** dari suatu item, tidak hanya item secara keseluruhan. Ini berarti jika kita tidak bisa memasukkan seluruh item ke dalam knapsack karena kapasitas yang terbatas, kita bisa mengambil sebagian dari item tersebut untuk memaksimalkan nilai total.

---

### Karakteristik

* **Pecahan Item Diizinkan**: Ini adalah karakteristik utama yang membedakannya dari 0/1 Knapsack (di mana item harus diambil seluruhnya atau tidak sama sekali).
* **Setiap Item Memiliki Berat dan Nilai**: Setiap item *i* memiliki berat *w_i* dan nilai *v_i*.
* **Kapasitas Terbatas**: Knapsack memiliki kapasitas berat maksimum *W*.
* **Tujuan Optimasi**: Maksimalkan total nilai item yang dimasukkan ke dalam knapsack.

---

### Strategi Penyelesaian

Karena kita dapat mengambil pecahan item, masalah Fractional Knapsack dapat diselesaikan secara optimal menggunakan pendekatan **Greedy Algorithm**. Strategi ini didasarkan pada gagasan untuk selalu memilih apa yang tampak terbaik pada saat itu.

---

### Kompleksitas Waktu

Kompleksitas waktu untuk menyelesaikan Fractional Knapsack menggunakan algoritma greedy sebagian besar didominasi oleh langkah pengurutan. Jika ada *n* item:

* Mengurutkan item berdasarkan rasio nilai per berat membutuhkan waktu *O(n \log n)*.
* Iterasi melalui item yang sudah diurutkan membutuhkan waktu *O(n)*.

Oleh karena itu, **kompleksitas waktu keseluruhan adalah *O(n \log n)***.

---

### Pengaplikasiannya

Fractional Knapsack memiliki berbagai aplikasi di dunia nyata, antara lain:

* **Alokasi Sumber Daya**: Mengalokasikan sumber daya yang terbatas (misalnya, anggaran, waktu) ke berbagai proyek atau investasi untuk memaksimalkan keuntungan.
* **Manajemen Investasi**: Memilih portofolio investasi dengan memaksimalkan keuntungan berdasarkan modal yang tersedia dan nilai pengembalian per unit modal.
* **Pemuatan Truk/Kapal**: Memuat barang ke dalam kendaraan pengangkut dengan kapasitas terbatas untuk memaksimalkan nilai barang yang diangkut.
* **Penjadwalan Tugas**: Menjadwalkan tugas dengan durasi dan prioritas berbeda dalam rentang waktu tertentu.

---

### Algoritma Greedy

Algoritma greedy untuk Fractional Knapsack bekerja sebagai berikut:

1.  **Hitung Rasio Nilai per Berat**: Untuk setiap item, hitung rasio nilai per berat (*v_i / w_i*). Rasio ini menunjukkan seberapa "berharga" setiap unit berat dari suatu item.
2.  **Urutkan Item**: Urutkan semua item dalam urutan **menurun** berdasarkan rasio nilai per berat mereka. Item dengan rasio yang lebih tinggi dianggap lebih menguntungkan.
3.  **Iterasi dan Pilih Item**: Mulai dari item dengan rasio nilai per berat tertinggi:
    * Jika seluruh item dapat dimasukkan ke dalam knapsack (berat item *\le* sisa kapasitas knapsack), masukkan seluruh item tersebut, kurangi kapasitas knapsack, dan tambahkan nilai item ke total nilai.
    * Jika seluruh item tidak dapat dimasukkan (berat item *>* sisa kapasitas knapsack), ambil **pecahan** dari item tersebut yang sesuai dengan sisa kapasitas knapsack. Tambahkan nilai pecahan tersebut ke total nilai, dan kapasitas knapsack menjadi nol. Hentikan proses.


## Permasalahan

Seorang penjelajah memiliki ransel dengan kapasitas maksimum 50 kg. Ia memiliki sejumlah barang, masing-masing dengan berat dan nilai tertentu. Ia dapat mengambil **sebagian** dari sebuah barang jika seluruh barang tidak muat dalam ransel.

| Barang | Berat (kg) | Nilai (unit) |
|--------|------------|--------------|
| 1      | 10         | 60           |
| 2      | 20         | 100          |
| 3      | 30         | 120          |

Bagaimana cara penjelajah memilih barang (atau sebagian barang) untuk dimasukkan ke dalam ranselnya agar **total nilai maksimal**?

---

## Solusi 

Kita akan menggunakan algoritma **greedy**, yaitu selalu memilih barang dengan rasio nilai/berat tertinggi terlebih dahulu.

- Langkah-Langkah Penyelesaian:
1. Hitung rasio nilai per unit berat (value/weight)
Untuk setiap item, kita hitung berapa nilai yang diberikan untuk setiap satuan beratnya. Ini karena kita ingin memaksimalkan nilai total yang bisa dimasukkan ke dalam knapsack.

2. Urutkan item berdasarkan rasio tersebut secara menurun (descending)
Item dengan rasio tertinggi akan diprioritaskan, karena memberikan "nilai terbaik" per kilogram.

3. Ambil item satu per satu dari yang paling bernilai
Selama masih ada ruang di dalam knapsack:
- ika berat item masih muat sepenuhnya, masukkan seluruh item.
- Jika tidak muat, ambil sebagian item yang sesuai dengan sisa kapasitas dan tambahkan nilai proporsional.

4. Proses berhenti ketika kapasitas knapsack habis.

- Contoh Singkat
Misal:

- Kapasitas knapsack: 50 kg

- Item:
1. Item A: nilai 60, berat 10 → rasio = 6
2. Item B: nilai 100, berat 20 → rasio = 5
3. Item C: nilai 120, berat 30 → rasio = 4

- Langkah:

1. Urutkan berdasarkan rasio → A (6), B (5), C (4)
2. Masukkan seluruh A (10 kg, sisa 40 kg)
3. Masukkan seluruh B (20 kg, sisa 20 kg)
4. Masukkan sebagian C (20/30 dari berat → ambil 2/3 nilainya → 80)

Total nilai:
60 (A) + 100 (B) + 80 (C) = 240

-----

### Kesimpulan

**Fractional Knapsack** adalah masalah optimasi yang dapat diselesaikan secara efisien menggunakan **algoritma greedy**. Kunci penyelesaiannya adalah mengurutkan item berdasarkan **rasio nilai per berat** dan memilih item-item dengan rasio tertinggi hingga knapsack penuh. Kemampuan untuk mengambil pecahan item membuatnya berbeda dan lebih sederhana untuk dipecahkan secara optimal dibandingkan dengan masalah 0/1 Knapsack yang memerlukan pemrograman dinamis. Efisiensinya, dengan kompleksitas waktu *O(n \log n)*, menjadikannya solusi praktis untuk berbagai skenario alokasi sumber daya.

![Desktop View](https://i.pinimg.com/564x/3f/55/43/3f554324815a6183498fb891d37b1a97.jpg){: width="200"}
_---_

