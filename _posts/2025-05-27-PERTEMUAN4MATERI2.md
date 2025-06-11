---
title: "Breadth-First Search (BFS)"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, Breadth-First Search (BFS)]
tags: [daa, Breadth-First Search (BFS), desain, analisis algoritma]
---

# Breadth-First Search (BFS)

## Pengertian Breadth-First Search (BFS)

Breadth-First Search (BFS) adalah metode sistematis untuk menjelajahi atau mencari pada struktur data graf atau pohon dengan menelusuri simpul-simpul berdasarkan jaraknya dari titik awal. Secara sederhana, BFS akan mengeksplorasi semua simpul yang paling dekat terlebih dahulu (yaitu, pada "level" yang sama), baru kemudian beralih ke simpul yang lebih jauh. Jadi pendekatannya menyebar ke seluruh arah secara merata dari pusat, seperti gelombang yang memancar dari titik awal.

Sebagai ilustrasi, bayangkan kita sedang mencari ruang kelas di sebuah gedung kampus berlantai 3. Kita pasti akan memeriksa seluruh ruangan dari lantai pertama sebelum lanjut ke lantai atas. Itulah cara kerja BFS: menjelajah secara mendatar, level demi level.

BFS banyak digunakan dalam berbagai aplikasi, mulai dari pencarian rute tercepat dalam game, penelusuran jaringan sosial, hingga pencarian jalur optimal dalam sistem navigasi dan peta digital.

## Konsep Dasar BFS

Beberapa konsep kunci yang mendasari BFS adalah:

1.  **Penggunaan Struktur Data Queue (Antrean):** BFS secara fundamental menggunakan struktur data antrean (Queue) untuk mengelola simpul-simpul yang akan dikunjungi. Simpul yang baru ditemukan akan ditambahkan ke belakang antrean, dan simpul yang akan diproses diambil dari depan antrean (First-In, First-Out / FIFO).
2.  **Penjelajahan Level-by-Level:** Algoritma ini memulai dari simpul awal, mengunjungi semua tetangganya terlebih dahulu, kemudian mengunjungi semua tetangga dari tetangga tersebut, dan seterusnya. Ini memastikan penjelajahan per lapisan atau per level.
3.  **Level-Order Traversal:** Istilah ini sering digunakan untuk menggambarkan cara BFS menelusuri simpul, yaitu berdasarkan lapisan demi lapisan dari simpul awal.
4.  **Matriks Kunjungan (Visited Array/Set):** Untuk mencegah pengulangan kunjungan pada simpul yang sama dan menghindari *infinite loop* (terutama pada graf yang memiliki siklus), BFS menggunakan sebuah cara untuk menandai simpul yang sudah dikunjungi. Ini bisa berupa array boolean `visited[]` atau sebuah `Set` untuk menyimpan simpul yang telah dikunjungi.

## Mekanisme Kerja BFS

Algoritma BFS bekerja dengan langkah-langkah sebagai berikut:

1.  **Inisialisasi:**
    * Buat sebuah antrean kosong (`Q`).
    * Buat sebuah array/set `visited` untuk melacak simpul yang sudah dikunjungi.
    * Tambahkan simpul awal (`s`) ke `Q`.
    * Tandai simpul awal `s` sebagai sudah dikunjungi (`visited[s] = true`).

2.  **Iterasi:**
    * Selama `Q` tidak kosong:
        * Ambil (dequeue) simpul `u` dari depan `Q`.
        * Proses simpul `u` (misalnya, cetak `u`).
        * Untuk setiap tetangga `v` dari `u`:
            * Jika `v` belum dikunjungi (`visited[v] == false`):
                * Tandai `v` sebagai sudah dikunjungi (`visited[v] = true`).
                * Tambahkan (enqueue) `v` ke `Q`.

## Contoh Visualisasi Graf

Misalkan kita memiliki graf dengan simpul-simpul berikut: A, B, C, D, E, F, G.

```
      A
     / \
    B   C
   / \   \
  D   E   F
   \ /
    G
```

Asumsi, kita memulai BFS dari simpul A.

**Langkah-langkah Simulasi BFS dari A:**

1.  **Antrean (Q):** `[ ]`
    **Dikunjungi (Visited):** `{}`
    * Tambahkan A ke Q, tandai A sebagai dikunjungi.
    **Q:** `[A]`
    **Visited:** `{A}`

2.  **Proses A:**
    * Ambil A dari Q. Cetak A.
    * Tetangga A: B, C.
    * Tambahkan B ke Q, tandai B dikunjungi.
    * Tambahkan C ke Q, tandai C dikunjungi.
    **Q:** `[B, C]`
    **Visited:** `{A, B, C}`
    **Output:** `A`

3.  **Proses B:**
    * Ambil B dari Q. Cetak B.
    * Tetangga B: A, D, E.
    * A sudah dikunjungi.
    * Tambahkan D ke Q, tandai D dikunjungi.
    * Tambahkan E ke Q, tandai E dikunjungi.
    **Q:** `[C, D, E]`
    **Visited:** `{A, B, C, D, E}`
    **Output:** `A, B`

4.  **Proses C:**
    * Ambil C dari Q. Cetak C.
    * Tetangga C: A, F.
    * A sudah dikunjungi.
    * Tambahkan F ke Q, tandai F dikunjungi.
    **Q:** `[D, E, F]`
    **Visited:** `{A, B, C, D, E, F}`
    **Output:** `A, B, C`

5.  **Proses D:**
    * Ambil D dari Q. Cetak D.
    * Tetangga D: B, G.
    * B sudah dikunjungi.
    * Tambahkan G ke Q, tandai G dikunjungi.
    **Q:** `[E, F, G]`
    **Visited:** `{A, B, C, D, E, F, G}`
    **Output:** `A, B, C, D`

6.  **Proses E:**
    * Ambil E dari Q. Cetak E.
    * Tetangga E: B, G.
    * B sudah dikunjungi.
    * G sudah dikunjungi.
    **Q:** `[F, G]`
    **Visited:** `{A, B, C, D, E, F, G}`
    **Output:** `A, B, C, D, E`

7.  **Proses F:**
    * Ambil F dari Q. Cetak F.
    * Tetangga F: C.
    * C sudah dikunjungi.
    **Q:** `[G]`
    **Visited:** `{A, B, C, D, E, F, G}`
    **Output:** `A, B, C, D, E, F`

8.  **Proses G:**
    * Ambil G dari Q. Cetak G.
    * Tetangga G: D, E.
    * D sudah dikunjungi.
    * E sudah dikunjungi.
    **Q:** `[ ]`
    **Visited:** `{A, B, C, D, E, F, G}`
    **Output:** `A, B, C, D, E, F, G`

**Urutan Penjelajahan (Output BFS):** A, B, C, D, E, F, G.
Ini menunjukkan penelusuran level demi level:
* Level 0: A
* Level 1: B, C
* Level 2: D, E, F
* Level 3: G

## Kompleksitas Waktu BFS

Kompleksitas waktu BFS bergantung pada representasi graf:

* **Representasi Adjacency Matrix:** $O(V^2)$, di mana `V` adalah jumlah simpul. Ini karena untuk setiap simpul, kita mungkin perlu memeriksa semua `V` simpul lainnya untuk menemukan tetangga.
* **Representasi Adjacency List:** $O(V + E)$, di mana `V` adalah jumlah simpul dan `E` adalah jumlah sisi (edges). Ini lebih efisien karena kita hanya mengunjungi sisi-sisi yang benar-benar ada.

## Aplikasi BFS

BFS memiliki berbagai aplikasi penting dalam ilmu komputer dan bidang lainnya:

1.  **Pencarian Jalur Terpendek (Shortest Path):** BFS dapat digunakan untuk menemukan jalur terpendek dalam graf yang tidak berbobot (unweighted graph). Ini karena BFS menjelajahi simpul secara level demi level, sehingga simpul pertama yang ditemukan adalah simpul dengan jarak terpendek.
2.  **Web Crawlers:** Mesin pencari menggunakan prinsip BFS untuk menjelajahi halaman-halaman web. Mereka mulai dari satu halaman, kemudian mengunjungi semua tautan di halaman itu, lalu semua tautan di halaman-halaman yang baru ditemukan, dan seterusnya.
3.  **Jaringan Sosial:** BFS digunakan untuk menemukan "teman dari teman" atau mengidentifikasi orang-orang dalam jarak sosial tertentu.
4.  **Sistem Navigasi/GPS:** Untuk menemukan rute terpendek antara dua lokasi pada peta yang dapat direpresentasikan sebagai graf.
5.  **Broadcast/Multicast di Jaringan:** Untuk mengirimkan pesan ke semua simpul dalam jaringan secara efisien.
6.  **Pencarian dalam Game:** Digunakan dalam algoritma AI untuk menemukan jalur terpendek ke tujuan atau musuh.
7.  **Graph Bipartite Testing:** Untuk menentukan apakah suatu graf adalah graf bipartit.
8.  **Deteksi Siklus:** Dapat digunakan untuk mendeteksi siklus dalam graf tak berarah.

---