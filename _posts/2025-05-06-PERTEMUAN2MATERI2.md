---
title: "PERTEMUAN 2 MATERI 2"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, Fractional Knapsack]
tags: [daa, Activity Selection Problem, desain, analisis algoritma]
---

# Fractional Knapsack

**Knapsack Problem** adalah sebuah masalah optimasi di mana kita dihadapkan pada tantangan untuk memilih barang-barang dari sekumpulan item yang tersedia. Tujuannya adalah untuk memaksimalkan total nilai dari barang-barang yang dipilih tanpa melebihi kapasitas berat maksimum dari sebuah ransel (*knapsack*).

Terdapat dua variasi utama dari masalah ini, yaitu:

1.  **0/1 Knapsack**: Pada variasi ini, kita hanya memiliki dua pilihan untuk setiap barang: mengambil seluruh barang tersebut atau tidak sama sekali. Barang tidak boleh dipotong atau diambil sebagian.
2.  **Fractional Knapsack**: Pada variasi ini, kita diperbolehkan untuk mengambil sebagian (fraksi) dari sebuah barang. Ini berarti barang bisa dipotong sesuai kebutuhan untuk mencapai nilai maksimal.

Perbedaan mendasar ini membuat **0/1 Knapsack** lebih kompleks dan umumnya diselesaikan dengan metode *pemrograman dinamis*. Sebaliknya, **Fractional Knapsack** dapat diselesaikan secara efisien menggunakan **algoritma *greedy*** yang lebih sederhana.

---

## Apa itu Fractional Knapsack?

### Definisi
**Fractional Knapsack** adalah sebuah permasalahan optimisasi di mana tujuannya adalah untuk memaksimalkan nilai total barang yang dimasukkan ke dalam sebuah ransel dengan kapasitas terbatas, dengan memperbolehkan pengambilan sebagian (fraksi) dari barang tersebut.

### Karakteristik
* Setiap barang memiliki dua atribut utama: **berat** (*weight*) dan **nilai** (*value*).
* Kapasitas ransel bersifat **terbatas**.
* Barang **boleh dipotong** atau diambil sebagian (misalnya, 0.5 kg dari barang A).
* Masalah ini dapat diselesaikan secara optimal menggunakan pendekatan ***greedy***, karena kita tidak perlu mencari semua kemungkinan kombinasi barang seperti pada 0/1 Knapsack.

---

## Algoritma Greedy

**Algoritma Greedy** adalah sebuah pendekatan atau strategi dalam merancang algoritma yang bekerja dengan cara membuat pilihan yang tampak terbaik pada saat itu (pilihan **optimal lokal**) dengan harapan bahwa serangkaian pilihan tersebut akan mengarah pada solusi **optimal global**.

### Karakteristik Utama Algoritma Greedy
* **Pilihan Lokal Optimal**: Di setiap langkahnya, algoritma ini selalu memilih opsi yang paling menguntungkan atau "serakah" (*greedy*) saat itu juga.
* **Tidak Melihat ke Depan**: Keputusan dibuat hanya berdasarkan informasi yang tersedia pada saat ini, tanpa mempertimbangkan sub-masalah yang akan muncul di masa depan setelah keputusan tersebut dibuat.
* **Sederhana dan Cepat**: Algoritma *greedy* seringkali sangat sederhana untuk diimplementasikan dan memiliki kompleksitas waktu yang rendah dibandingkan pendekatan lain seperti pemrograman dinamis.

Meskipun efektif untuk masalah tertentu, kelemahan utama algoritma *greedy* adalah **tidak selalu menghasilkan solusi optimal global** untuk semua jenis masalah. Ada beberapa masalah di mana pilihan terbaik saat ini justru dapat menghalangi tercapainya solusi terbaik secara keseluruhan.

---

## Strategi Penyelesaian Fractional Knapsack

Untuk menyelesaikan Fractional Knapsack, kita menggunakan pendekatan **Greedy Algorithm** dengan langkah-langkah sebagai berikut:

1.  **Hitung Rasio Nilai per Berat**: Untuk setiap barang, hitung rasio nilai terhadap beratnya (*value/weight*). Rasio ini merepresentasikan "kepadatan nilai" dari setiap barang.

2.  **Urutkan Barang**: Urutkan semua barang dalam urutan menurun berdasarkan rasio *value/weight* yang telah dihitung. Barang dengan rasio tertinggi akan berada di urutan pertama.

3.  **Isi Ransel secara "Serakah"**: Mulai dari barang dengan rasio tertinggi, masukkan barang sebanyak mungkin ke dalam ransel hingga barang tersebut habis atau hingga kapasitas ransel penuh.

4.  **Ambil Sebagian Jika Perlu**: Jika setelah memasukkan sebuah barang secara utuh kapasitas ransel tidak cukup untuk barang berikutnya dalam urutan, ambil sebagian (fraksi) dari barang tersebut secukupnya hingga kapasitas ransel tepat terpenuhi.

### Kompleksitas Waktu
Kompleksitas waktu untuk menyelesaikan Fractional Knapsack dengan strategi ini adalah **O(n log n)**.
* **O(n log n)** berasal dari langkah pengurutan barang berdasarkan rasionya.
* **O(n)** berasal dari langkah memasukkan barang ke dalam ransel (satu kali iterasi).

Karena langkah pengurutan mendominasi, maka kompleksitas waktu keseluruhannya adalah O(n log n).

---

## Aplikasi di Dunia Nyata

Konsep Fractional Knapsack dapat diterapkan dalam berbagai skenario optimisasi, di antaranya:
* Penjadwalan tugas dengan sumber daya terbatas.
* Investasi dana dengan mengalokasikannya ke beberapa proyek.
* Pengalokasian *bandwidth* di jaringan komputer.
* Optimisasi logistik dan pemuatan kargo.

---

## Kesimpulan

**Fractional Knapsack** adalah variasi dari Knapsack Problem yang dapat diselesaikan secara efisien menggunakan **algoritma *greedy***. Perbedaan utamanya dengan 0/1 Knapsack adalah barang boleh diambil sebagian (fraksional).

Dengan menghitung rasio nilai terhadap berat (*value/weight*) untuk setiap barang, lalu mengambil barang dengan rasio tertinggi secara berurutan hingga kapasitas tas penuh, kita bisa mendapatkan solusi optimal dengan cepat dan sederhana. Pendekatan *greedy* ini terbukti efektif karena pilihan optimal lokal (berdasarkan rasio tertinggi) akan selalu mengarah pada solusi optimal global dalam kasus Fractional Knapsack.