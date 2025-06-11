---
title: "Subset Sum Problem"
date: 2025-05-06
categories: [Desan dan Analisis Algoritma, Subset Sum Problem]
tags: [daa, Subset Sum Problem, desain, analisis algoritma]
---

## Subset Sum Problem

## Apa itu Subset Sum Problem?

Subset Sum Problem (SSP) adalah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target.

**Definisi Formal:**
Input: `arr = [1, 2, 3]`, `target_sum = 3`
Output: `True`
Penjelasan: Terdapat subset `{1, 2}` yang jumlahnya 3.

**Contoh lain:**
Input: `arr = {10, 20, 30, 40, 50}`, `sum = 25`
Output: `False`
Penjelasan: Tidak ada subset yang jumlahnya 25.

Subset Sum Problem termasuk dalam *decision problem*, yaitu jenis masalah yang hanya membutuhkan jawaban "ya" atau "tidak". Inti dari masalah ini adalah mencari apakah mungkin memilih sejumlah angka dari sekumpulan bilangan bulat sehingga totalnya pas sama dengan angka target. Dalam implementasinya di dunia nyata, Subset Sum Problem bisa ditemukan dalam kriptografi, pengelolaan keuangan, perencanaan sumber daya, bahkan kecerdasan buatan.

## Variasi Masalah Subset Sum Problem

Subset Sum Problem memiliki beberapa variasi:

1.  **Bounded Subset Sum Problem:** Setiap elemen dalam himpunan hanya dapat digunakan sekali untuk membentuk subset yang jumlahnya sama dengan target. Artinya, jika sebuah angka muncul sekali dalam himpunan, kita hanya bisa menggunakannya sekali saja. Ini cocok untuk kasus di mana barang atau sumber daya hanya tersedia satu unit.
    * Contoh Kasus: `Set = {3, 34, 4, 12, 5, 2}`, Target = 9. Apakah mungkin? Ya. Subset `{4, 5}` menghasilkan total 9.

2.  **Partition Problem:** Masalah membagi sebuah himpunan bilangan bulat menjadi dua subset yang memiliki jumlah total yang sama. Secara teknis, ini setara dengan mencari subset dengan jumlah sama dengan setengah dari total seluruh elemen himpunan. Masalah ini penting dalam manajemen sumber daya, seperti membagi beban server, tugas antar tim, atau membagi file secara seimbang.
    * Contoh Kasus: `Set = {1, 5, 11, 5}`, Total = 22 $\rightarrow$ Target subset = 11. Kita bisa buat dua subset: `{11}` dan `{1, 5, 5}` $\rightarrow$ keduanya berjumlah 11.

3.  **Exact k Elements Subset Sum:** Mencari subset yang jumlahnya sama dengan target dan terdiri dari tepat k elemen. Variasi ini menambahkan batasan tambahan yaitu jumlah elemen dalam subset harus tepat sebanyak k elemen. Masalah ini cocok untuk memilih tim beranggotakan k orang dengan total nilai tertentu, atau memilih k item dengan total harga tepat.
    * Contoh Kasus: `Set = {1, 2, 3, 4, 5}`, Target = 9, k = 2. Apakah mungkin? Ya. Subset `{4, 5}` terdiri dari 2 elemen dan jumlahnya 9.

4.  **Unbounded Subset Sum Problem:** Setiap elemen boleh digunakan berulang kali untuk mencapai target. Ini berarti jika kita memiliki angka 3 dalam himpunan, kita bisa memakainya dua, tiga, atau bahkan lebih kali selama tidak melebihi target.
    * Contoh Kasus: `Set = {1, 3, 4}`, Target = 6. Apakah mungkin? Ya. Beberapa kemungkinan: $1+1+1+3=6$, $3+3=6$, $2 \times 1 + 4 = 6$.

5.  **Multi-target Subset Sum Problem:** Mencari subset yang memenuhi lebih dari satu kriteria, misalnya jumlah total dan batas berat. Dalam variasi ini, masalah subset sum menjadi lebih kompleks karena tidak hanya melibatkan satu target jumlah, tetapi lebih dari satu kriteria atau batasan yang harus dipenuhi secara bersamaan. Masalah ini sering muncul dalam e-commerce (checkout produk dengan batas ongkir) atau logistik pengiriman.
    * Contoh Kasus: Set barang: Barang A (harga=40, berat=1 kg), Barang B (harga=60, berat=1.5 kg), Barang C (harga=30, berat=0.5 kg). Target: total harga $\le 100$ dan total berat $\le 2$ kg. Kombinasi Barang A+C $\rightarrow$ total harga 70, berat 1.5 kg $\rightarrow$ valid. Tapi A+B $\rightarrow$ harga 100, berat 2.5 kg $\rightarrow$ tidak valid karena melebihi berat.

6.  **Approximate Subset Sum:** Tidak ada subset yang jumlahnya tepat sama dengan target, jadi dicari subset terbaik yang mendekati target, biasanya tidak boleh melebihi.
    * Contoh Kasus: `Set = {2, 5, 10, 14}`, Target = 15. Tidak ada subset yang tepat 15. Tapi: `{5, 10} = 15` (tepat). Kalau target = 16, dan tidak ada kombinasi pas, kita bisa ambil `{14}` atau `{10, 5} = 15` $\rightarrow$ solusi terbaik.

## Pendekatan Subset Sum Problem

### Pendekatan Rekursif (Recursive Approach)

Pendekatan ini mengecek semua subset secara eksplisit. Untuk setiap elemen, ada dua pilihan: sertakan ATAU abaikan.

* **Basis kasus:**
    * Jika `sum == 0`, hasilnya `True`.
    * Jika `n == 0` dan `sum != 0`, hasilnya `False`.
* **Kompleksitas:** $O(2^n)$.
* **Kelemahan:** Tidak efisien untuk array besar.

### Dynamic Programming Approach

Pendekatan *dynamic programming* lebih optimal baik dari segi waktu maupun ruang.

**A. Memoization (Top-Down DP)**
Kombinasi rekursi dengan penyimpanan hasil submasalah. Gunakan struktur `dp[n][sum]` untuk menyimpan hasil (*cache*). Pendekatan ini mengurangi pemanggilan ulang fungsi yang sama. Efisien untuk input sedang, tetapi masih membutuhkan *stack* rekursi.
* Kompleksitas Waktu: $O(n \times sum)$
* Kompleksitas Memori: $O(n \times sum)$

**B. Tabulation (Bottom-Up DP)**
Pendekatan iteratif yang dimulai dari kasus paling kecil. Buat tabel `dp[n+1][sum+1]`. `dp[i][j]` akan bernilai `True` jika subset `arr[0..i-1]` bisa menghasilkan `j`.
* **Inisialisasi:**
    * `dp[i][0] = True` (karena subset kosong = 0)
    * `dp[0][j] = False` (tidak bisa dapat sum $>0$ tanpa elemen)
* Iterasi solusi dari bawah ke atas.

**C. Optimasi Ruang pada Subset Sum (Space Optimization)**
Dalam pendekatan tabulasi, kita hanya membutuhkan baris sebelumnya (`i-1`) untuk menghitung baris saat ini. Karena itu, kita bisa menghemat ruang dari $O(n \times sum)$ menjadi $O(sum)$ dengan dua array 1D: `prev` dan `curr`.
* `prev[j]`: apakah jumlah `j` bisa dicapai dengan elemen sebelumnya.
* `curr[j]`: status jumlah `j` saat mempertimbangkan elemen saat ini.
* **Aturan pengisian:**
    * Jika `j < arr[i]`: `curr[j] = prev[j]`
    * Jika `j >= arr[i]`: `curr[j] = prev[j]` atau `prev[j - arr[i]]`
* Setelah satu iterasi, salin `curr` ke `prev`.
* **Kompleksitas Waktu:** $O(n \times sum)$
* **Kompleksitas Ruang:** $O(sum)$
Pendekatan ini sangat berguna saat nilai `sum` besar, karena mengurangi penggunaan memori secara signifikan.

## Aplikasi Permasalahan Subset Sum di Dunia Nyata

Subset Sum Problem memiliki berbagai aplikasi nyata:

1.  **Kriptografi:** Digunakan dalam sistem kriptografi berbasis ransel, di mana kesulitan menyelesaikan Subset Sum Problem menjadi dasar keamanan kunci publik.
2.  **Alokasi Sumber Daya:** Membantu memilih subset proyek atau item agar sesuai dengan anggaran atau target tertentu.
3.  **Genetika dan Bioinformatika:** Digunakan untuk menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
4.  **Keuangan dan Investasi:** Membantu menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
5.  **Perancangan Permainan dan Teka-Teki:** Muncul dalam permainan atau teka-teki yang melibatkan pencarian kombinasi angka sesuai skor target.

---

## Kesimpulan

Subset Sum Problem (SSP) adalah masalah dalam ilmu komputer yang bertujuan untuk menentukan apakah terdapat subset dari sekumpulan bilangan bulat yang jumlahnya sama dengan nilai target tertentu. Masalah ini tergolong dalam kategori NP-Complete dan memiliki berbagai variasi, seperti *bounded*, *unbounded*, *exact k elements*, *partition*, *multi-target*, hingga *approximate subset sum*, yang masing-masing memiliki aplikasi dan batasan berbeda.

Untuk menyelesaikan SSP, digunakan pendekatan rekursif yang sederhana namun kurang efisien, serta *dynamic programming* yang lebih optimal baik dari segi waktu maupun ruang. Subset Sum memiliki aplikasi nyata dalam bidang kriptografi, keuangan, pengelolaan sumber daya, hingga kecerdasan buatan, menjadikannya masalah penting yang tidak hanya teoritis, tetapi juga relevan dalam dunia praktis.

---