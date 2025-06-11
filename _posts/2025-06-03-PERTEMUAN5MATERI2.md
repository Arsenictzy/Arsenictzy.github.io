---
title: "PERTEMUAN 5 MATERI 2"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, Dijkstra's Algorithm]
tags: [daa, Dijkstra's Algorithm, desain, analisis algoritma]
---

# Dijkstra's Algorithm

## Apa itu Dijkstra's Algorithm?

Dijkstra's Algorithm adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik (simpul/vertex) dalam sebuah graf. Graf ini bisa berupa jaringan yang terdiri dari simpul (titik) dan sisi (hubungan antar titik) dengan bobot tertentu pada sisi-sisinya. Algoritma ini membantu kita menentukan jalur terpendek dari titik awal ke titik tujuan.

Algoritma Dijkstra dikembangkan oleh Edsger W. Dijkstra pada tahun 1956 dan merupakan salah satu algoritma *greedy* yang paling terkenal. Ini berarti pada setiap langkah, algoritma membuat pilihan yang tampak optimal pada saat itu, dengan harapan pilihan-pilihan lokal ini akan mengarah pada solusi global yang optimal.

**Catatan Penting:** Dijkstra's Algorithm hanya dapat bekerja pada graf yang semua bobot sisinya adalah non-negatif. Jika ada sisi dengan bobot negatif, algoritma ini tidak akan menjamin hasil yang benar. Untuk kasus tersebut, algoritma seperti Bellman-Ford atau Floyd-Warshall lebih cocok.

## Cara Kerja Dijkstra's Algorithm

Algoritma Dijkstra bekerja dengan cara membangun pohon jalur terpendek dari simpul sumber ke semua simpul lainnya secara bertahap. Berikut adalah langkah-langkah dasarnya:

1.  **Inisialisasi Jarak:**
    * Tetapkan jarak dari simpul sumber ke dirinya sendiri sebagai 0.
    * Tetapkan jarak dari simpul sumber ke semua simpul lainnya sebagai tak hingga (infinity).
    * Buat sebuah set atau array untuk melacak simpul-simpul yang sudah "dikunjungi" atau "finalized" (jarak terpendeknya sudah ditemukan). Awalnya, set ini kosong.

2.  **Pilih Simpul Saat Ini:**
    * Pilih simpul yang belum dikunjungi dengan jarak terpendek dari simpul sumber. Simpul ini menjadi "simpul saat ini".

3.  **Perbarui Jarak Tetangga:**
    * Untuk setiap tetangga dari simpul saat ini:
        * Hitung jarak alternatif dari simpul sumber ke tetangga tersebut melalui simpul saat ini.
        * Jika jarak alternatif ini lebih kecil dari jarak yang sudah tercatat untuk tetangga tersebut, perbarui jarak tetangga.

4.  **Tandai Dikunjungi:**
    * Setelah semua tetangga dari simpul saat ini diperbarui, tandai simpul saat ini sebagai sudah dikunjungi (finalized).

5.  **Ulangi:**
    * Ulangi langkah 2-4 sampai semua simpul telah dikunjungi atau semua simpul yang dapat dijangkau telah diproses.

## Tabel Jarak dan Jalur

Untuk memvisualisasikan cara kerja algoritma, kita sering menggunakan tabel. Tabel ini biasanya memiliki kolom untuk setiap simpul dan baris untuk setiap iterasi, mencatat jarak terpendek yang ditemukan sejauh ini dari simpul sumber ke simpul lain.

**Struktur Tabel:**
* **Simpul (Vertex):** Daftar semua simpul dalam graf.
* **Jarak (Distance):** Jarak terpendek yang diketahui dari simpul sumber ke simpul ini. Awalnya `0` untuk sumber, `infinity` untuk yang lain.
* **Sebelumnya (Previous):** Simpul yang mendahului simpul ini dalam jalur terpendek. Digunakan untuk merekonstruksi jalur.
* **Dikunjungi (Visited/Finalized):** Menandai apakah jarak terpendek ke simpul ini sudah final.

## Simulasi Dijkstra's Algorithm

Mari kita simulasikan Dijkstra's Algorithm pada graf contoh:

```
      (A) ---10--- (B)
      |          / |
      2         /  3
      |        /   |
      (S) ---5--- (C) ---4--- (D)
      |        \   /
      7         \ /
      |          /
      (E)
```

**Tabel Inisialisasi (Sumber = S):**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | False      |
| A      | $\infty$  | -              | False      |
| B      | $\infty$  | -              | False      |
| C      | $\infty$  | -              | False      |
| D      | $\infty$  | -              | False      |
| E      | $\infty$  | -              | False      |

**Iterasi 1: Pilih S (jarak 0)**
* Tandai S dikunjungi.
* Tetangga S: A, C, E.
    * Jarak ke A melalui S: $0 + 2 = 2$. (`D[A]` = 2, `P[A]` = S)
    * Jarak ke C melalui S: $0 + 5 = 5$. (`D[C]` = 5, `P[C]` = S)
    * Jarak ke E melalui S: $0 + 7 = 7$. (`D[E]` = 7, `P[E]` = S)

**Tabel Setelah Iterasi 1:**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | False      |
| B      | $\infty$  | -              | False      |
| C      | 5         | S              | False      |
| D      | $\infty$  | -              | False      |
| E      | 7         | S              | False      |

**Iterasi 2: Pilih A (jarak 2)**
* Tandai A dikunjungi.
* Tetangga A: S, B.
    * S sudah dikunjungi.
    * Jarak ke B melalui A: $2 + 10 = 12$. (`D[B]` = 12, `P[B]` = A)

**Tabel Setelah Iterasi 2:**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | True       |
| B      | 12        | A              | False      |
| C      | 5         | S              | False      |
| D      | $\infty$  | -              | False      |
| E      | 7         | S              | False      |

**Iterasi 3: Pilih C (jarak 5)**
* Tandai C dikunjungi.
* Tetangga C: S, B, D.
    * S sudah dikunjungi.
    * Jarak ke B melalui C: $5 + 3 = 8$. (Lebih kecil dari 12!) (`D[B]` = 8, `P[B]` = C)
    * Jarak ke D melalui C: $5 + 4 = 9$. (`D[D]` = 9, `P[D]` = C)

**Tabel Setelah Iterasi 3:**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | True       |
| B      | 8         | C              | False      |
| C      | 5         | S              | True       |
| D      | 9         | C              | False      |
| E      | 7         | S              | False      |

**Iterasi 4: Pilih E (jarak 7)**
* Tandai E dikunjungi.
* Tetangga E: S.
    * S sudah dikunjungi.

**Tabel Setelah Iterasi 4:**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | True       |
| B      | 8         | C              | False      |
| C      | 5         | S              | True       |
| D      | 9         | C              | False      |
| E      | 7         | S              | True       |

**Iterasi 5: Pilih B (jarak 8)**
* Tandai B dikunjungi.
* Tetangga B: A, C.
    * A sudah dikunjungi.
    * C sudah dikunjungi.

**Tabel Setelah Iterasi 5:**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | True       |
| B      | 8         | C              | True       |
| C      | 5         | S              | True       |
| D      | 9         | C              | False      |
| E      | 7         | S              | True       |

**Iterasi 6: Pilih D (jarak 9)**
* Tandai D dikunjungi.
* Tetangga D: C.
    * C sudah dikunjungi.

**Tabel Akhir (Semua simpul dapat dijangkau dan dikunjungi):**

| Simpul | Jarak (D) | Sebelumnya (P) | Dikunjungi |
| :----- | :-------- | :------------- | :--------- |
| S      | 0         | -              | True       |
| A      | 2         | S              | True       |
| B      | 8         | C              | True       |
| C      | 5         | S              | True       |
| D      | 9         | C              | True       |
| E      | 7         | S              | True       |

Dari tabel ini, kita dapat merekonstruksi jalur terpendek dari S ke simpul mana pun. Misalnya, jalur terpendek ke D adalah `S -> C -> D` dengan total jarak 9.

## Kompleksitas Waktu Dijkstra's Algorithm

Kompleksitas waktu Dijkstra's Algorithm tergantung pada implementasi struktur data yang digunakan untuk memilih simpul dengan jarak minimum.

* **Implementasi Sederhana (dengan array/list linier):** $O(V^2)$, di mana `V` adalah jumlah simpul. Ini karena pada setiap langkah, kita perlu mencari simpul terdekat dari `V` simpul yang belum dikunjungi.
* **Implementasi dengan Priority Queue (Min-Heap):** $O((V + E) \log V)$, di mana `V` adalah jumlah simpul dan `E` adalah jumlah sisi. Ini adalah implementasi yang jauh lebih efisien, terutama untuk graf besar dan jarang (*sparse graph*), karena operasi mencari minimum dan memperbarui jarak (decrease-key) menjadi lebih cepat.

## Kelebihan dan Kekurangan Dijkstra's Algorithm

### Kelebihan

* **Akurasi Tinggi:** Menjamin penemuan jalur terpendek pada graf berbobot non-negatif.
* **Fleksibel:** Dapat digunakan untuk menemukan jalur terpendek dari satu sumber ke semua simpul lainnya, atau hanya ke satu simpul tujuan spesifik.
* **Efisiensi (dengan Priority Queue):** Dengan penggunaan *priority queue* (min-heap), algoritma ini menjadi sangat efisien dan merupakan pilihan utama untuk masalah jalur terpendek di banyak aplikasi.
* **Fondasi Algoritma Lain:** Menjadi dasar bagi algoritma lain seperti A* (A Star) yang menambahkan heuristik untuk pencarian lebih cepat.

### Kekurangan

* **Tidak Bekerja dengan Bobot Negatif:** Ini adalah batasan utama. Jika graf memiliki sisi dengan bobot negatif, Dijkstra's Algorithm tidak akan menghasilkan jalur terpendek yang benar.
* **Potensi Kurang Efisien untuk Graf Sangat Jarang:** Meskipun $O((V+E)\log V)$ efisien, pada graf yang sangat besar namun sangat jarang (E << V^2), terkadang ada algoritma lain yang mungkin lebih cepat (meskipun jarang).
* **Perhitungan Bisa Terlalu Luas:** Jika tujuan kita hanya menemukan jalur dari titik A ke titik B, Dijkstra tetap menghitung jarak terpendek ke semua simpul lain yang dapat dijangkau dari A. Dalam kasus ini, algoritma seperti $A^{*}$ yang memperhitungkan heuristik arah tujuan bisa lebih optimal karena mereka "memandu" pencarian menuju tujuan.

---

## Kesimpulan

Algoritma Dijkstra merupakan salah satu algoritma pencarian jalur terpendek yang paling efisien dan banyak digunakan dalam teori graf. Algoritma ini bekerja dengan cara mencari jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot non-negatif. Melalui pendekatan *greedy*, Dijkstra memastikan bahwa setiap langkahnya mendekatkan solusi menuju hasil optimal. Keunggulan utama algoritma ini terletak pada keakuratannya dan efisiensinya, terutama jika dikombinasikan dengan struktur data seperti *priority queue* atau *min-heap*. Dalam implementasi praktis, algoritma Dijkstra sangat berguna dalam berbagai bidang seperti jaringan komputer, sistem navigasi, dan pemodelan transportasi.

---