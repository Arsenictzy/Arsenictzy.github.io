---
title: "PERTEMUAN 4 MATERI 3"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, Depth-First Search (DFS)]
tags: [daa, Depth-First Search (DFS), desain, analisis algoritma]
---

# Depth-First Search (DFS)

## Pengertian Depth-First Search (DFS)

Depth-First Search (DFS) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (*backtrack*) dan melanjutkan ke cabang berikutnya.

Bayangkan kita sedang menjelajahi labirin. Dengan DFS, kita akan memilih satu jalan, mengikuti jalan itu sejauh mungkin, dan jika menemui jalan buntu, kita akan kembali ke persimpangan terakhir dan mencoba jalan lain. Ini berbeda dengan BFS yang menyebar secara level demi level.

## Prinsip Utama DFS

Prinsip utama yang mendasari DFS adalah:

1.  **Penggunaan Struktur Data Stack (Tumpukan):** DFS secara fundamental menggunakan struktur data tumpukan (Stack) untuk mengelola simpul-simpul yang akan dikunjungi. Simpul yang baru ditemukan akan ditambahkan ke atas tumpukan, dan simpul yang akan diproses diambil dari atas tumpukan (Last-In, First-Out / LIFO). Meskipun sering diimplementasikan secara rekursif (yang secara implisit menggunakan stack panggilan), konsep stack tetap menjadi inti.
2.  **Penjelajahan Sedalam Mungkin:** Algoritma ini memulai dari simpul awal, menjelajahi salah satu tetangganya, kemudian menjelajahi tetangga dari tetangga tersebut, dan seterusnya, sampai mencapai simpul yang tidak memiliki tetangga belum dikunjungi, atau sampai jalan buntu.
3.  **Backtracking:** Ketika DFS mencapai simpul dari mana ia tidak bisa lagi bergerak lebih dalam (yaitu, semua tetangga sudah dikunjungi atau merupakan dinding), algoritma akan "mundur" (*backtrack*) ke simpul sebelumnya yang masih memiliki tetangga yang belum dijelajahi, dan melanjutkan pencarian dari sana.
4.  **Matriks Kunjungan (Visited Array/Set):** Mirip dengan BFS, DFS juga menggunakan sebuah cara untuk menandai simpul yang sudah dikunjungi (`visited[]` array boolean atau `Set`) untuk mencegah pengulangan kunjungan pada simpul yang sama dan menghindari *infinite loop* (terutama pada graf yang memiliki siklus).

## Mekanisme Kerja DFS

Algoritma DFS bekerja dengan langkah-langkah sebagai berikut:

1.  **Inisialisasi:**
    * Buat sebuah tumpukan kosong (`S`).
    * Buat sebuah array/set `visited` untuk melacak simpul yang sudah dikunjungi.
    * Masukkan simpul awal (`s`) ke `S`.
    * Tandai simpul awal `s` sebagai sudah dikunjungi (`visited[s] = true`).

2.  **Iterasi:**
    * Selama `S` tidak kosong:
        * Ambil (pop) simpul `u` dari atas `S`.
        * Proses simpul `u` (misalnya, cetak `u`).
        * Untuk setiap tetangga `v` dari `u` (dalam urutan tertentu, misalnya, dari yang terkecil ke terbesar atau sebaliknya):
            * Jika `v` belum dikunjungi (`visited[v] == false`):
                * Tandai `v` sebagai sudah dikunjungi (`visited[v] = true`).
                * Masukkan (push) `v` ke `S`.

    *Jika menggunakan pendekatan rekursif:*
    * **Fungsi Rekursif `DFS(u, graph, visited)`:**
        * Tandai `u` sebagai dikunjungi.
        * Proses `u` (misalnya, cetak `u`).
        * Untuk setiap tetangga `v` dari `u`:
            * Jika `v` belum dikunjungi:
                * Panggil `DFS(v, graph, visited)`.
        * Ketika semua tetangga `u` telah diproses (dan semua cabang yang berasal dari `u` telah dieksplorasi secara rekursif), fungsi kembali ke pemanggilnya, yang merupakan *backtracking* implisit.

## Contoh Visualisasi Graf

Misalkan kita memiliki graf dengan simpul-simpul berikut: 0, 1, 2, 3, 4, 5.

```
      0 -- 1
     /    / \
    2    3   4
     \  /
      5
```

Representasi graf ini dalam Adjacency List:
* 0: [1, 2]
* 1: [0, 3, 4]
* 2: [0, 5]
* 3: [1]
* 4: [1]
* 5: [2]

Asumsi, kita memulai DFS dari simpul 0.

**Langkah-langkah Simulasi DFS dari 0 (menggunakan stack implisit dari rekursi, atau eksplisit):**

1.  **Mulai DFS dari 0:**
    * Kunjungi 0. Output: 0. Tandai 0 dikunjungi.
    * Tetangga 0: 1, 2. Pilih 1 (asumsi urutan menaik).

2.  **Panggil DFS(1):**
    * Kunjungi 1. Output: 0, 1. Tandai 1 dikunjungi.
    * Tetangga 1: 0, 3, 4.
    * 0 sudah dikunjungi. Pilih 3.

3.  **Panggil DFS(3):**
    * Kunjungi 3. Output: 0, 1, 3. Tandai 3 dikunjungi.
    * Tetangga 3: 1.
    * 1 sudah dikunjungi. Tidak ada tetangga yang belum dikunjungi.
    * **Backtrack** ke 1.

4.  **Lanjut dari 1 (setelah 3):**
    * Tetangga 1 yang belum dikunjungi: 4.

5.  **Panggil DFS(4):**
    * Kunjungi 4. Output: 0, 1, 3, 4. Tandai 4 dikunjungi.
    * Tetangga 4: 1.
    * 1 sudah dikunjungi. Tidak ada tetangga yang belum dikunjungi.
    * **Backtrack** ke 1.

6.  **Lanjut dari 1 (setelah 4):**
    * Semua tetangga 1 sudah dikunjungi.
    * **Backtrack** ke 0.

7.  **Lanjut dari 0 (setelah 1):**
    * Tetangga 0 yang belum dikunjungi: 2.

8.  **Panggil DFS(2):**
    * Kunjungi 2. Output: 0, 1, 3, 4, 2. Tandai 2 dikunjungi.
    * Tetangga 2: 0, 5.
    * 0 sudah dikunjungi. Pilih 5.

9.  **Panggil DFS(5):**
    * Kunjungi 5. Output: 0, 1, 3, 4, 2, 5. Tandai 5 dikunjungi.
    * Tetangga 5: 2.
    * 2 sudah dikunjungi. Tidak ada tetangga yang belum dikunjungi.
    * **Backtrack** ke 2.

10. **Lanjut dari 2 (setelah 5):**
    * Semua tetangga 2 sudah dikunjungi.
    * **Backtrack** ke 0.

11. **Lanjut dari 0 (setelah 2):**
    * Semua tetangga 0 sudah dikunjungi.
    * **Backtrack** ke pemanggil awal.

**Urutan Penjelajahan (Output DFS):** 0, 1, 3, 4, 2, 5.
Ini menunjukkan penelusuran yang mendalam di satu cabang sebelum beralih ke cabang lain.

## Implementasi Kode C++

(Bagian ini merujuk pada kode C++ yang ditampilkan dalam presentasi. Untuk implementasi lengkap, pembaca dapat melihat kode C++ yang disediakan dalam materi asli.)

Implementasi DFS dalam C++ umumnya menggunakan pendekatan rekursif. Struktur kode akan mencakup:

```cpp
#include <iostream>
#include <vector>
#include <stack> // Untuk implementasi iteratif, jika diperlukan

// Fungsi DFS rekursif
void DFS(int node, const std::vector<std::vector<int>>& graph, std::vector<bool>& visited) {
    visited[node] = true; // Tandai node saat ini sebagai dikunjungi
    std::cout << node << " "; // Proses node (misal: cetak)

    // Jelajahi semua tetangga dari node saat ini
    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) { // Jika tetangga belum dikunjungi
            DFS(neighbor, graph, visited); // Panggil rekursif untuk tetangga
        }
    }
}

int main() {
    int n = 6; // Jumlah node/simpul
    // Representasi graf menggunakan Adjacency List
    std::vector<std::vector<int>> graph(n);

    // Menambahkan sisi-sisi (edges) ke graf
    graph[0].push_back(1); // 0 terhubung ke 1
    graph[0].push_back(2); // 0 terhubung ke 2
    graph[1].push_back(0); // 1 terhubung ke 0
    graph[1].push_back(3); // 1 terhubung ke 3
    graph[1].push_back(4); // 1 terhubung ke 4
    graph[2].push_back(0); // 2 terhubung ke 0
    graph[2].push_back(5); // 2 terhubung ke 5
    graph[3].push_back(1); // 3 terhubung ke 1
    graph[4].push_back(1); // 4 terhubung ke 1
    graph[5].push_back(2); // 5 terhubung ke 2

    // Vektor boolean untuk melacak node yang sudah dikunjungi
    std::vector<bool> visited(n, false); // Inisialisasi semua node sebagai belum dikunjungi

    std::cout << "DFS traversal starting from node 0: ";
    DFS(0, graph, visited); // Mulai DFS dari node 0
    std::cout << std::endl;

    // Output: DFS traversal starting from node 0: 0 1 3 4 2 5
    // Catatan: Urutan mungkin sedikit berbeda tergantung implementasi urutan tetangga

    return 0;
}

```

## Aplikasi DFS

DFS memiliki berbagai aplikasi penting dalam ilmu komputer dan bidang lainnya:

1.  **Pencarian Jalur (Path Finding):** Digunakan untuk menemukan jalur antara dua simpul dalam graf. Meskipun tidak menjamin jalur terpendek (seperti BFS pada graf tak berbobot), DFS dapat menemukan jalur.
2.  **Deteksi Siklus (Cycle Detection):** Dapat digunakan untuk mendeteksi apakah ada siklus dalam graf, baik berarah maupun tak berarah.
3.  **Topological Sort:** Dalam graf berarah asiklik (DAG), DFS digunakan untuk menghasilkan urutan linear simpul-simpul sehingga untuk setiap sisi berarah dari `u` ke `v`, `u` muncul sebelum `v` dalam urutan. Ini penting dalam penjadwalan tugas.
4.  **Mencari Komponen Terhubung (Connected Components):** Untuk menemukan semua simpul yang dapat dijangkau dari simpul awal dalam graf tak berarah.
5.  **Penyelesaian Labirin dan Game Puzzle:** Digunakan dalam algoritma AI untuk memecahkan labirin atau teka-teki dengan menjelajahi setiap kemungkinan jalan.
6.  **Finding Strongly Connected Components (SCCs):** Dalam graf berarah, DFS adalah bagian inti dari algoritma seperti Tarjan's algorithm atau Kosaraju's algorithm untuk menemukan komponen terhubung kuat.
7.  **Backtracking Algorithms:** DFS adalah dasar dari banyak algoritma backtracking, seperti yang digunakan dalam masalah N-Queens, Sudoku solver, atau subset sum.

---