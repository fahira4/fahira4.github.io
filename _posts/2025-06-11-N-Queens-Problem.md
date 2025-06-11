---
title: N-QUEENS PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking]     # TAG names should always be lowercase
---


![Desktop View](https://media.geeksforgeeks.org/wp-content/uploads/20230814111624/N-Queen-Problem.png){: width="500"}
_---_

Dalam dunia komputasi dan matematika, **N-Queens Problem** merupakan salah satu contoh klasik dari masalah pencarian solusi atau *constraint satisfaction problem* yang memperlihatkan kekuatan rekursi dan *backtracking*. Masalah ini didasarkan pada permainan catur, dengan tujuannya adalah menempatkan `N` ratu pada papan catur berukuran `N x N` sedemikian rupa sehingga **tidak ada dua ratu yang saling menyerang**.

Ratu dalam permainan catur dapat bergerak ke segala arah: horizontal, vertikal, dan diagonal. Maka dari itu, tantangannya terletak pada bagaimana menempatkan setiap ratu di papan catur agar **tidak ada ratu yang berada pada baris, kolom, atau diagonal yang sama**.

Masalah ini tidak hanya menjadi latihan algoritmik yang populer, tetapi juga digunakan dalam bidang:
- **Penjadwalan** (misalnya penjadwalan tugas tanpa konflik),
- **Pemrograman berbasis AI**,
- **Pencarian solusi logis**,
- Dan pengujian algoritma backtracking.
---

## N-Queens Problem

### Definisi Masalah

Masalah N-Queens adalah sebuah permasalahan klasik dalam bidang ilmu komputer dan matematika kombinatorik yang melibatkan penempatan N buah ratu catur pada sebuah papan catur berukuran *N \times N* sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang.

* Dalam aturan catur, seorang ratu dapat bergerak secara horizontal (baris), vertikal (kolom), dan diagonal.
* Oleh karena itu, solusi dari masalah ini harus memastikan bahwa tidak ada dua ratu yang berada pada baris, kolom, atau diagonal yang sama.
* Contoh paling terkenal adalah masalah 8-Queens, yaitu menempatkan 8 ratu di papan *8 \times 8*.

### Tujuan Masalah N-Queens

Tujuan utama dari masalah ini adalah:
1.  Menemukan semua konfigurasi penempatan ratu yang memenuhi syarat tidak saling menyerang.
2.  Mengembangkan dan menguji algoritma pencarian dan optimasi, seperti *backtracking*, DFS, *heuristic search*, atau algoritma genetika.
3.  Melatih logika pemrograman dan pemecahan masalah, terutama dalam konteks *constraint satisfaction problem* (CSP).

### Pentingnya Masalah N-Queens

Masalah N-Queens penting dalam berbagai konteks, di antaranya:
1.  **Sebagai Studi Kasus dalam AI dan Algoritma:**
    * Masalah ini digunakan secara luas untuk mengajarkan teknik pencarian seperti *backtracking*, *branch and bound*, serta algoritma *heuristic* dan *metaheuristic*. Ini menjadikannya landasan dalam studi *artificial intelligence* dan *operations research*.
2.  **Model Permasalahan *Constraint Satisfaction*:**
    * N-Queens adalah contoh ideal dari masalah CSP, di mana kita harus menetapkan nilai (posisi ratu) ke dalam variabel (baris/kolom) tanpa melanggar kendala (serangan).
3.  **Aplikasi dalam Dunia Nyata:**
    * Walau berbasis permainan catur, prinsip-prinsip di balik N-Queens dapat diterapkan dalam masalah nyata seperti:
        * Penjadwalan tugas (di mana konflik harus dihindari).
        * Penempatan modul dalam sirkuit elektronik.
        * Dan pengalokasian sumber daya yang saling eksklusif.
4.  **Kompleksitas dan Skalabilitas:**
    * Masalah ini menunjukkan bagaimana kompleksitas meningkat secara eksponensial dengan bertambahnya nilai N, sehingga cocok sebagai bahan evaluasi efisiensi algoritma dalam skala besar.

## Mengapa N-Queens adalah Masalah Backtracking

N-Queens adalah masalah klasik yang paling sering diselesaikan menggunakan teknik *backtracking*. Ini karena:

1.  **Pendekatan Rekursif dan Bertahap:**
    * Dalam penyelesaian N-Queens, kita menempatkan ratu satu per satu, biasanya dimulai dari baris pertama.
    * Untuk setiap baris, kita mencoba meletakkan ratu di setiap kolom satu per satu dan memeriksa apakah posisi tersebut aman (tidak diserang oleh ratu sebelumnya).
    * Jika aman, kita lanjut ke baris berikutnya. Jika tidak ada posisi yang aman, kita kembali ke baris sebelumnya dan mencoba posisi lain—proses inilah yang disebut *backtracking*.
2.  **Pohon Pencarian Solusi:**
    * Setiap penempatan ratu mewakili satu simpul dalam pohon pencarian.
    * Jalur dari akar ke daun mewakili satu kemungkinan solusi. Jika sebuah jalur tidak bisa menghasilkan solusi yang valid, kita *prune* (pangkas) jalur itu dan mencoba cabang lain.
3.  **Sifat Non-deterministik:**
    * Karena ada banyak kemungkinan posisi untuk setiap ratu, dan tidak diketahui posisi yang benar sejak awal, kita harus mencoba semua kemungkinan dengan sistematis. Ini menjadikan *backtracking* sebagai teknik yang sangat cocok.

### Relevansi dalam Mata Kuliah Design and Analysis of Algorithms (DAA)

1.  **Studi Kasus Teknik Backtracking:**
    * N-Queens adalah contoh klasik yang digunakan untuk mengilustrasikan konsep *backtracking* secara sistematis, sehingga sangat relevan dalam DAA. Mahasiswa bisa belajar bagaimana menyusun solusi secara bertahap dan menghindari eksplorasi solusi yang tidak mungkin.
2.  **Analisis Kompleksitas Algoritma:**
    * Masalah ini membantu memahami analisis waktu dan ruang dari algoritma *brute-force* versus algoritma berbasis *backtracking* yang lebih efisien. Meskipun *backtracking* memiliki kompleksitas waktu eksponensial dalam kasus terburuk, teknik ini tetap jauh lebih cepat dibanding mencoba semua kemungkinan secara buta.
3.  **Pengenalan *Constraint Satisfaction Problem* (CSP):**
    * N-Queens memperkenalkan mahasiswa pada CSP, sebuah topik penting dalam kecerdasan buatan dan optimasi. Teknik *backtracking* dapat diperluas menjadi *backtracking* dengan *forward checking* atau *backjumping*, yang relevan dalam studi algoritma canggih.

## Backtracking

**Backtracking** adalah teknik penyelesaian masalah yang mencoba membangun solusi langkah demi langkah dan "mundur" (*backtrack*) ketika menemui jalan buntu (*dead end*). Ini adalah pendekatan *brute-force* yang sistematis dengan optimasi, di mana solusi yang tidak valid dibuang secepat mungkin.

### Langkah-langkah dalam Algoritma Backtracking:

1.  **Pilih Keputusan (*Decision Choice*):**
    * Pada setiap langkah, pilih opsi yang mungkin dari kandidat solusi.
    * Contoh: Dalam masalah N-Queens, pilih kolom untuk menempatkan ratu di baris berikutnya.
2.  **Batasan (*Constraint Check*):**
    * Periksa apakah pilihan tersebut valid berdasarkan aturan masalah.
    * Jika valid, lanjut ke langkah berikutnya.
    * Jika tidak valid, abaikan opsi ini dan coba opsi lain (*backtrack*).
3.  **Rekursi (*Recursive Exploration*):**
    * Jika pilihan valid, rekursif melanjutkan pencarian solusi dengan keputusan ini.
4.  **Backtrack (Kembali jika *Dead End*):**
    * Jika tidak ada solusi yang ditemukan setelah memilih opsi tertentu, batalkan keputusan terakhir (*undo*) dan coba opsi lain.
5.  **Basis Kasus (*Base Case*):**
    * Jika semua keputusan telah mengarah ke solusi lengkap, catat solusinya (atau kembalikan solusi).

### Contoh dalam Permutasi Angka

Mari kita cari semua permutasi dari `[1, 2, 3]` menggunakan algoritma *backtracking*.

**Langkah Algoritma:**
1.  **Pilih angka pertama: 1**
    * Subproblem: Cari permutasi dari `[2, 3]` *\rightarrow* `[1,2,3]`, `[1,3,2]`
    * Backtrack: Kembali ke pilihan awal.
2.  **Pilih angka pertama: 2**
    * Subproblem: Cari permutasi dari `[1, 3]` *\rightarrow* `[2,1,3]`, `[2,3,1]`
    * Backtrack: Kembali ke pilihan awal.
3.  **Pilih angka pertama: 3**
    * Subproblem: Cari permutasi dari `[1, 2]` *\rightarrow* `[3,1,2]`, `[3,2,1]`

**Solusi Akhir:**
`[[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]`

### Kesimpulan dari Backtracking

*Backtracking* adalah pendekatan *exhaustive search* dengan optimasi, di mana solusi dibangun bertahap dan dibatalkan jika tidak valid. Alurnya melibatkan eksplorasi rekursif, pemeriksaan batasan, dan pengembalian (*undo*) jika gagal.

## ❓ Permasalahan

Diberikan papan catur `N x N`, tempatkan `N` buah ratu sedemikian rupa sehingga **tidak ada dua ratu yang saling menyerang**, artinya:
- Tidak ada dua ratu di baris atau kolom yang sama.
- Tidak ada dua ratu di diagonal yang sama.

### Input:
- Bilangan bulat `N`, ukuran papan dan jumlah ratu.

### Output:
- Satu atau semua konfigurasi papan catur di mana ratu-ratu bisa ditempatkan dengan aman.

---

## Solusi (Implementasi C++)

Pendekatan yang umum digunakan adalah **backtracking**, yaitu mencoba satu per satu kemungkinan posisi ratu dan kembali ke langkah sebelumnya bila terjadi konflik.

---

### Kode C++

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(int row, int col, vector<string>& board, int n) {
    // Cek kolom atas
    for (int i = 0; i < row; i++)
        if (board[i][col] == 'Q') return false;

    // Cek diagonal kiri atas
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
        if (board[i][j] == 'Q') return false;

    // Cek diagonal kanan atas
    for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
        if (board[i][j] == 'Q') return false;

    return true;
}

void solve(int row, vector<string>& board, vector<vector<string>>& solutions, int n) {
    if (row == n) {
        solutions.push_back(board);
        return;
    }

    for (int col = 0; col < n; col++) {
        if (isSafe(row, col, board, n)) {
            board[row][col] = 'Q';
            solve(row + 1, board, solutions, n);
            board[row][col] = '.'; // backtrack
        }
    }
}

void nQueens(int n) {
    vector<vector<string>> solutions;
    vector<string> board(n, string(n, '.'));

    solve(0, board, solutions, n);

    cout << "Jumlah solusi: " << solutions.size() << endl;
    for (const auto& sol : solutions) {
        for (const string& row : sol)
            cout << row << endl;
        cout << "----------" << endl;
    }
}

int main() {
    int N = 4;
    nQueens(N);
    return 0;
}


##Kesimpulan

N-Queens Problem adalah masalah klasik yang menguji kemampuan kita dalam penalaran kombinatorik dan penerapan algoritma. Dengan menggunakan pendekatan *backtracking*, kita dapat secara sistematis mengeksplorasi semua kemungkinan penempatan ratu, memangkas cabang yang tidak valid, dan menemukan setiap konfigurasi yang memenuhi batasan.

Masalah ini bukan hanya sekedar teka-teki catur; ia berfungsi sebagai studi kasus fundamental dalam ilmu komputer untuk mengajarkan konsep-konsep kunci seperti pencarian rekursif, manajemen batasan, dan analisis kompleksitas algoritma. Penerapannya meluas hingga ke penjadwalan, alokasi sumber daya, dan bidang optimasi lainnya di dunia nyata. Dengan demikian, penguasaan N-Queens Problem memberikan dasar yang kuat untuk memahami dan menyelesaikan berbagai masalah komputasi yang lebih kompleks.

---

![Desktop View](data:image/jpeg;base64,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){: width="250"}
_---_

