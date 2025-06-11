---
title: RAT IN MAZE
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking]     # TAG names should always be lowercase
---

![Desktop View](assets/images/POST/PERTEMUAN4/RatInMaze (1).webp){: width="500"}
_---_

HALO!, **Rat in a Maze** adalah sebuah masalah algoritma klasik di mana seekor tikus harus menemukan jalan dari titik awal ke titik tujuan di dalam sebuah labirin. Labirin itu sendiri direpresentasikan oleh sebuah grid atau matriks, dengan sel-sel yang bisa dilewati atau terhalang. Masalah ini adalah contoh penerapan dari **algoritma lacak-balik (backtracking)**. Pendekatan ini melibatkan tikus yang mencoba bergerak selangkah demi selangkah, dan jika jalur yang dipilih ternyata buntu atau salah, ia akan "mundur" (lacak-balik) ke posisi sebelumnya untuk mencoba arah yang berbeda.

***

### Cara Kerjanya

Prinsip utamanya melibatkan seekor tikus yang mencoba menemukan jalur dari posisi awal ke tujuan dalam labirin berbentuk matriks.

* **Representasi**: Labirin adalah sebuah grid di mana nilai sel menentukan jalurnya. Nilai **1** menandakan jalur yang valid, sedangkan nilai **0** merepresentasikan dinding atau rintangan.
* **Pergerakan**: Tikus mulai dari sel yang ditentukan, biasanya (0, 0), dan bertujuan untuk mencapai tujuan, biasanya di (N-1, N-1) dalam matriks N/*N. Tikus dapat bergerak ke empat arah: Atas (U), Bawah (D), Kiri (L), dan Kanan (R).
* **Validasi**: Sebuah langkah dianggap valid hanya jika tetap berada di dalam batas labirin dan tidak mendarat di sel yang terhalang (nilai '0'). Tidak ada sel yang boleh dikunjungi lebih dari satu kali dalam satu jalur.
* **Lacak-balik (Backtracking)**: Tikus mencoba satu arah pada satu waktu. Jika posisi baru mengarah ke jalan buntu atau tidak menawarkan langkah valid lebih lanjut menuju tujuan, tikus akan mundur ke sel sebelumnya untuk menjelajahi arah lain yang tersedia.

***

### Contoh Permasalahan

Bayangkan seekor tikus yang terjebak dalam labirin persegi berukuran `N x N`. Tikus ini berada di sudut kiri atas (0,0) dan ingin mencapai sudut kanan bawah (N-1, N-1). Jalur labirin hanya terdiri dari dua jenis sel:

- `1` berarti jalan yang dapat dilewati,
- `0` berarti dinding atau hambatan yang tidak dapat dilewati.

Tikus hanya dapat bergerak ke bawah (`D`) atau ke kanan (`R`) pada setiap langkahnya. Tujuan utamanya adalah menemukan **semua jalur** yang memungkinkan dari awal hingga akhir, atau paling tidak, **satu jalur** yang valid.

Masalah ini adalah contoh klasik dari aplikasi **algoritma backtracking**, yang merupakan teknik pemecahan masalah dengan cara mencoba setiap kemungkinan solusi, dan "mundur" ketika menemui jalan buntu. Tak hanya berguna dalam konteks labirin, pendekatan seperti ini dapat diterapkan dalam:

- Penelusuran jalur pada peta,
- Perencanaan rute dalam robotika,
- AI game-solving,
- Pengambilan keputusan dalam sistem berbasis aturan.

---

## ❓ Permasalahan

### 🎯 Input:
- Matriks `N x N` yang mewakili labirin.
- Setiap sel berisi:
  - `1` → jalan bisa dilewati,
  - `0` → jalan terhalang.

### 🎯 Tujuan:
- Cari **semua jalur** dari `(0,0)` ke `(N-1,N-1)` menggunakan langkah valid ke bawah (`D`) atau ke kanan (`R`).
- Hindari sel dengan `0`.

---

## ✅ Solusi (Backtracking)

Pendekatan ini menggunakan rekursi untuk mencoba semua kemungkinan langkah dari setiap posisi, dan kembali (backtrack) jika menemui jalan buntu.

---

### 💻 Kode C++

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

void findPaths(vector<vector<int>>& maze, int x, int y, string path, vector<string>& result, int n) {
    if (x == n - 1 && y == n - 1 && maze[x][y] == 1) {
        result.push_back(path);
        return;
    }

    // Tandai posisi sebagai dikunjungi
    maze[x][y] = -1;

    // Bawah
    if (x + 1 < n && maze[x + 1][y] == 1)
        findPaths(maze, x + 1, y, path + "D", result, n);

    // Kanan
    if (y + 1 < n && maze[x][y + 1] == 1)
        findPaths(maze, x, y + 1, path + "R", result, n);

    // Kiri
    if (y - 1 >= 0 && maze[x][y - 1] == 1)
        findPaths(maze, x, y - 1, path + "L", result, n);

    // Atas
    if (x - 1 >= 0 && maze[x - 1][y] == 1)
        findPaths(maze, x - 1, y, path + "U", result, n);

    // Backtrack: Tandai kembali sebagai belum dikunjungi
    maze[x][y] = 1;
}

void ratInMaze(vector<vector<int>>& maze, int n) {
    vector<string> result;
    if (maze[0][0] == 0) {
        cout << "Tidak ada jalur dari titik awal.\n";
        return;
    }

    findPaths(maze, 0, 0, "", result, n);

    if (result.empty()) {
        cout << "Tidak ada solusi ditemukan.\n";
    } else {
        cout << "Jalur yang ditemukan:\n";
        for (const string& p : result)
            cout << p << endl;
    }
}

int main() {
    vector<vector<int>> maze = {
        {1, 0, 0, 0},
        {1, 1, 0, 1},
        {0, 1, 0, 0},
        {1, 1, 1, 1}
    };
    int n = maze.size();
    ratInMaze(maze, n);
    return 0;
}

Output:

Jalur yang ditemukan:
                        DDRDRR
                        DRDDRR

```
---

***

#### **Kelebihan** 
* **Sederhana untuk Diimplementasikan**: Logikanya lugas dan mudah untuk dikodekan.
* **Menemukan Semua Solusi**: Dapat menemukan setiap kemungkinan jalur dari awal hingga akhir.
* **Fleksibel**: Algoritma dapat diadaptasi untuk berbagai ukuran dan aturan labirin.
* **Tidak Memerlukan Struktur Data Kompleks**: Cukup efisien dari segi penggunaan memori.

#### **Kekurangan** 
* **Tidak Efisien untuk Labirin Besar**: Kinerjanya menurun secara signifikan seiring dengan bertambahnya ukuran labirin.
* **Risiko *Stack Overflow***: Rekursi yang dalam pada labirin besar dapat menghabiskan memori *stack*.
* **Tidak Optimal**: Solusi pertama yang ditemukan tidak dijamin sebagai yang terpendek.
* **Eksplorasi Berulang**: Tanpa manajemen status yang tepat (seperti array 'visited'), algoritma mungkin akan menjelajahi kembali jalur yang sama.

***

### Implementasi di Dunia Nyata

Konsep algoritma Rat in a Maze digunakan dalam berbagai aplikasi praktis.

* **Navigasi Robot**: Perangkat otonom seperti penyedot debu robot menggunakan logika pencarian jalur serupa untuk menavigasi ruangan.
* **Pencarian Jalur GPS**: Sistem navigasi menggunakan algoritma pencarian jalur untuk menemukan rute antara dua titik.
* **Simulasi dan Permainan**: Ini adalah bagian mendasar dari kecerdasan buatan karakter untuk menavigasi level atau peta dalam video game.

***

### Kesimpulan

Rat in a Maze adalah masalah fundamental yang menjadi contoh utama penggunaan algoritma lacak-balik (*backtracking*). Dengan merepresentasikan labirin sebagai matriks dan secara rekursif menjelajahi setiap kemungkinan jalur, algoritma ini mampu menemukan semua solusi yang ada. Meskipun memiliki kelemahan dalam hal efisiensi untuk skala besar, kesederhanaan dan kemampuannya untuk beradaptasi membuatnya tetap relevan. Aplikasinya dalam bidang-bidang modern seperti navigasi robot, GPS, dan pengembangan game menunjukkan bahwa prinsip dasar dari masalah ini memiliki nilai praktis yang signifikan.

---

![Desktop View](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBL4ux1Qkh5IiAeEwxJDbNITz6kzY-EFdopg&s){: width="300"}
_---_

