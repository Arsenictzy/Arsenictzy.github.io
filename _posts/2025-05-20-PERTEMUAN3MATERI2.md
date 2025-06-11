---
title: "PERTEMUAN 3 MATERI 2"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, N-Queens Problem]
tags: [daa, N-Queens Problem, desain, analisis algoritma]
---

## Queens Problem

## Definisi N-Queens Problem

N-Queens Problem adalah permasalahan klasik yang menantang kita untuk menempatkan N buah ratu catur pada papan catur berukuran $N \times N$ sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang. Dalam aturan catur, ratu dapat bergerak secara horizontal (baris), vertikal (kolom), dan diagonal. Oleh karena itu, solusi yang valid harus memastikan tidak ada dua ratu yang berada pada baris, kolom, atau diagonal yang sama. Contoh paling terkenal adalah masalah 8-Queens, yaitu menempatkan 8 ratu di papan $8 \times 8$.

## Tujuan N-Queens Problem

Tujuan utama dari N-Queens Problem meliputi:

1.  Menemukan semua konfigurasi penempatan ratu yang memenuhi syarat tidak saling menyerang.
2.  Mengembangkan dan menguji berbagai algoritma pencarian dan optimasi, seperti backtracking, Depth-First Search (DFS), heuristic search, atau algoritma genetika.
3.  Melatih logika pemrograman dan pemecahan masalah, terutama dalam konteks *constraint satisfaction problem* (CSP).

## Pentingnya N-Queens Problem

N-Queens Problem memiliki signifikansi dalam berbagai konteks:

1.  **Sebagai Studi Kasus dalam AI dan Algoritma:** Masalah ini digunakan secara luas untuk mengajarkan teknik pencarian seperti backtracking, branch and bound, serta algoritma heuristik dan metaheuristik. Ini menjadikannya landasan dalam studi kecerdasan buatan (Artificial Intelligence) dan riset operasi (Operations Research).
2.  **Model Permasalahan Constraint Satisfaction:** N-Queens Problem adalah contoh ideal dari masalah CSP, di mana kita harus menetapkan nilai (posisi ratu) ke dalam variabel (baris/kolom) tanpa melanggar kendala (serangan).
3.  **Aplikasi dalam Dunia Nyata:** Meskipun berbasis permainan catur, prinsip-prinsip di balik N-Queens Problem dapat diterapkan dalam masalah nyata seperti penjadwalan tugas (di mana konflik harus dihindari), penempatan modul dalam sirkuit elektronik, dan pengalokasian sumber daya yang saling eksklusif.
4.  **Kompleksitas dan Skalabilitas:** N-Queens Problem menunjukkan bagaimana kompleksitas meningkat secara eksponensial dengan bertambahnya nilai N, sehingga cocok sebagai bahan evaluasi efisiensi algoritma dalam skala besar.

## Mengapa N-Queens Problem adalah Masalah Backtracking

N-Queens Problem sangat cocok diselesaikan dengan teknik backtracking karena beberapa alasan:

1.  **Pendekatan Rekursif dan Bertahap:** Dalam penyelesaian N-Queens Problem, ratu ditempatkan satu per satu, biasanya dimulai dari baris pertama. Untuk setiap baris, kita mencoba meletakkan ratu di setiap kolom dan memeriksa apakah posisi tersebut aman (tidak diserang oleh ratu sebelumnya). Jika aman, kita lanjut ke baris berikutnya. Jika tidak ada posisi yang aman, kita kembali ke baris sebelumnya dan mencoba posisi lain. Proses inilah yang disebut backtracking.
2.  **Pohon Pencarian Solusi:** Setiap penempatan ratu mewakili satu simpul dalam pohon pencarian. Jalur dari akar ke daun mewakili satu kemungkinan solusi. Jika sebuah jalur tidak bisa menghasilkan solusi yang valid, jalur itu akan dipangkas (*pruned*) dan algoritma akan mencoba cabang lain.
3.  **Sifat Non-deterministik:** Karena ada banyak kemungkinan posisi untuk setiap ratu, dan posisi yang benar tidak diketahui sejak awal, kita harus mencoba semua kemungkinan dengan sistematis. Ini menjadikan backtracking sebagai teknik yang sangat cocok.

## Relevansi dalam Mata Kuliah Design and Analysis of Algorithms (DAA)

N-Queens Problem sangat relevan dalam mata kuliah Desain dan Analisis Algoritma (DAA) karena:

1.  **Studi Kasus Teknik Backtracking:** N-Queens Problem adalah contoh klasik yang digunakan untuk mengilustrasikan konsep backtracking secara sistematis. Mahasiswa dapat belajar bagaimana menyusun solusi secara bertahap dan menghindari eksplorasi solusi yang tidak mungkin.
2.  **Analisis Kompleksitas Algoritma:** Masalah ini membantu memahami analisis waktu dan ruang dari algoritma brute-force versus algoritma berbasis backtracking yang lebih efisien. Meskipun backtracking memiliki kompleksitas waktu eksponensial dalam kasus terburuk, teknik ini tetap jauh lebih cepat dibanding mencoba semua kemungkinan secara buta.
3.  **Pengenalan Constraint Satisfaction Problem (CSP):** N-Queens Problem memperkenalkan mahasiswa pada CSP, sebuah topik penting dalam kecerdasan buatan dan optimasi. Teknik backtracking dapat diperluas menjadi backtracking dengan *forward checking* atau *backjumping*, yang relevan dalam studi algoritma canggih.

## Backtracking

Backtracking adalah teknik penyelesaian masalah yang mencoba membangun solusi langkah demi langkah dan "mundur" (*backtrack*) ketika menemui jalan buntu (*dead end*). Ini adalah pendekatan *brute-force* yang sistematis dengan optimasi, di mana solusi yang tidak valid dibuang secepat mungkin.

### Langkah-langkah dalam Algoritma Backtracking:

1.  **Pilih Keputusan (Decision Choice):** Pada setiap langkah, pilih opsi yang mungkin dari kandidat solusi. Contoh: Dalam N-Queens Problem, pilih kolom untuk menempatkan ratu di baris berikutnya.
2.  **Batasan (Constraint Check):** Periksa apakah pilihan tersebut valid berdasarkan aturan masalah. Jika valid, lanjut ke langkah berikutnya. Jika tidak valid, abaikan opsi ini dan coba opsi lain (backtrack).
3.  **Rekursi (Recursive Exploration):** Jika pilihan valid, rekursif melanjutkan pencarian solusi dengan keputusan ini.
4.  **Backtrack (Kembali jika Dead End):** Jika tidak ada solusi yang ditemukan setelah memilih opsi tertentu, batalkan keputusan terakhir (*undo*) dan coba opsi lain.
5.  **Basis Kasus (Base Case):** Jika semua keputusan telah mengarah ke solusi lengkap, catat solusinya (atau kembalikan solusi).

### Contoh dalam Permutasi Angka

Mari kita cari semua permutasi dari `[1, 2, 3]` menggunakan backtracking.

Langkah Algoritma:

1.  **Pilih angka pertama: 1**
    * Subproblem: Cari permutasi `[2, 3]` yang menghasilkan `[1, 2, 3]` dan `[1, 3, 2]`.
    * Backtrack: Kembali ke pemilihan angka pertama.
2.  **Pilih angka pertama: 2**
    * Subproblem: Cari permutasi `[1, 3]` yang menghasilkan `[2, 1, 3]` dan `[2, 3, 1]`.
    * Backtrack: Kembali ke pemilihan angka pertama.
3.  **Pilih angka pertama: 3**
    * Subproblem: Cari permutasi `[1, 2]` yang menghasilkan `[3, 1, 2]` dan `[3, 2, 1]`.

Solusi Akhir:
`[[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]`

### Kesimpulan dari Backtracking

Backtracking adalah pendekatan *exhaustive search* dengan optimasi, di mana solusi dibangun bertahap dan dibatalkan jika tidak valid. Alurnya melibatkan eksplorasi rekursif, pemeriksaan batasan, dan pengembalian (*undo*) jika gagal.

## Contoh di Dunia Nyata: Penempatan Karyawan di Ruang Kerja

Bayangkan sebuah perusahaan yang memiliki N karyawan dan ingin menempatkan mereka dalam N ruang kerja yang tersedia di kantor. Setiap karyawan harus ditempatkan di ruang yang tidak mengganggu satu sama lain. Aturan yang berlaku adalah:

1.  Ruang yang berdekatan tidak boleh digunakan oleh dua karyawan yang sama (analog dengan baris dan kolom dalam N-Queens Problem).
2.  Karyawan yang berada dalam ruang yang sama atau saling berdekatan tidak boleh berada dalam garis lurus yang sama (analog dengan diagonal N-Queens Problem).
3.  Tujuan: Menempatkan setiap karyawan di ruang yang berbeda dengan aturan ini, tanpa ada dua yang saling bertabrakan.

### Langkah-langkah Penempatan Karyawan:

1.  **Ruang pertama:** Kita mulai dengan menempatkan karyawan pertama di ruang pertama. Tidak ada masalah di sini karena belum ada karyawan lain yang ditempatkan.
2.  **Ruang kedua:** Sekarang kita ingin menempatkan karyawan kedua. Dia tidak bisa ditempatkan di ruang pertama karena sudah diisi oleh karyawan pertama. Jadi kita lanjutkan mencari ruang yang tidak bertabrakan.
3.  **Ruang ketiga:** Ketika kita sampai pada ruang ketiga, kita mencari ruang yang tidak bertabrakan dengan dua karyawan sebelumnya. Setelah mencoba beberapa ruang, kita menemukan ruang yang valid dan menempatkan karyawan ketiga di sana.
4.  **Proses Berlanjut:** Proses ini berlanjut untuk semua karyawan, dengan aturan yang sama: tidak ada dua karyawan yang berada pada garis lurus atau di ruang yang saling berdekatan. Jika kita menemukan situasi di mana tidak ada ruang yang valid, kita akan kembali ke langkah sebelumnya dan mencoba opsi lain (backtrack).

### Kasus Backtracking dalam Penempatan Karyawan

Jika kita sudah menempatkan beberapa karyawan dan ternyata, pada langkah terakhir, tidak ada ruang lagi yang valid untuk karyawan ke-N, kita harus mundur (*backtrack*) dan mencoba posisi yang berbeda untuk karyawan yang sudah ditempatkan sebelumnya. Misalnya, jika kita sudah menempatkan beberapa karyawan dan pada langkah akhir tidak bisa melanjutkan, kita akan mundur dan mencoba menempatkan karyawan yang sebelumnya di ruang yang berbeda. Begitu kita menemukan ruang yang valid, kita akan melanjutkan sampai semua karyawan ditempatkan dengan benar.

Analogi untuk Dunia Nyata: Masalah ini mirip dengan bagaimana kita mengatur tempat duduk atau penempatan karyawan dalam ruang terbatas dengan berbagai aturan dan batasan, baik itu ruang fisik di kantor, gedung, atau dalam sistem yang lebih abstrak (seperti pengaturan sumber daya yang terbatas).

## Kode C++ untuk N-Queens Problem

(Bagian ini merujuk pada kode C++ yang ditampilkan dalam presentasi. Karena Markdown tidak dapat merepresentasikan gambar kode secara langsung, deskripsi akan bersifat umum. Untuk implementasi lengkap, pembaca dapat melihat kode C++ yang disediakan dalam materi asli.)

Kode C++ untuk menyelesaikan N-Queens Problem umumnya melibatkan fungsi-fungsi rekursif dengan logika backtracking. Struktur utama kode akan mencakup:

* **Fungsi `printSolution()`:** Untuk menampilkan solusi yang ditemukan, menunjukkan posisi ratu ('Q') dan kotak kosong ('.') pada papan.
* **Fungsi `isSafe(row, col)`:** Untuk memeriksa apakah menempatkan ratu pada `(row, col)` aman, yaitu tidak ada ratu lain yang menyerang secara horizontal, vertikal, atau diagonal.
* **Fungsi `solveNQueensUtil(col)`:** Fungsi rekursif inti yang mencoba menempatkan ratu pada kolom `col`. Jika ratu berhasil ditempatkan, ia akan memanggil dirinya sendiri untuk kolom berikutnya. Jika tidak ada posisi aman, ia akan melakukan backtracking.
* **Fungsi `solveNQueens()`:** Fungsi pembungkus yang menginisialisasi papan dan memanggil `solveNQueensUtil(0)` untuk memulai proses dari kolom pertama.
* **Fungsi `main()`:** Menerima input `N` dari pengguna dan memanggil `solveNQueens()` untuk menemukan dan menampilkan solusi.

Logika `isSafe` akan memeriksa tiga kondisi:
1.  Baris yang sama.
2.  Diagonal atas kiri ke bawah kanan.
3.  Diagonal bawah kiri ke atas kanan.

Fungsi rekursif akan mencoba menempatkan ratu di setiap baris pada kolom saat ini. Jika penempatan aman, ratu ditempatkan, dan fungsi dipanggil lagi untuk kolom berikutnya. Jika tidak, ratu dihapus (backtrack), dan baris berikutnya dicoba.

---