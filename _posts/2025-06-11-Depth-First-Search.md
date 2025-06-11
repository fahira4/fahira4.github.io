---
title: DEPTH-FIRST SEARCH (DFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, dfs]     # TAG names should always be lowercase
---

![Desktop View](https://cdn.educba.com/academy/wp-content/uploads/2020/03/Depth-First-Search.jpg){: width="450"}
_---_

Dalam dunia yang penuh dengan jaringan kompleks—seperti jejaring sosial, jalur transportasi, atau struktur folder pada sistem file—kita sering kali ingin mengetahui bagaimana cara menelusuri semua elemen atau simpul yang terhubung dalam sistem tersebut. Salah satu pendekatan klasik dan mendasar dalam ilmu komputer untuk menyelesaikan masalah ini adalah Depth-First Search (DFS).

DFS adalah algoritma penelusuran yang menjelajahi graf dengan menyusuri jalur sejauh mungkin sebelum kembali (backtrack) ke simpul sebelumnya dan mencoba jalur lain. Pendekatan ini menyerupai cara kerja manusia saat menjelajahi labirin: memilih satu arah dan mengikuti terus hingga mentok, lalu mundur dan mencoba arah lain.

DFS umumnya diimplementasikan menggunakan rekursi (secara implisit menggunakan call stack) atau stack eksplisit. Berbeda dengan BFS yang menjelajahi semua tetangga terlebih dahulu (meluas ke lebar), DFS menjelajahi cabang terlebih dahulu (menyelam ke dalam).

### Manfaat DFS dalam dunia nyata:

- **Menemukan komponen terhubung** dalam graf
- **Pencarian solusi** dalam permainan seperti puzzle atau labirin
- **Mendeteksi siklus** dalam graf
- **Penjadwalan tugas** menggunakan topological sort
- **Analisis ketergantungan** dalam proyek atau sistem

DFS sangat berguna dalam memahami struktur dalam, mencari jalur, dan menyelidiki sifat-sifat graf yang lebih dalam, terutama dalam graf besar dan kompleks.

---


### Prinsip Utama dan Langkah-Langkah

Prinsip utama DFS adalah penggunaan struktur data Tumpukan (*Stack*) yang mengikuti metode LIFO (Last-In, First-Out).

Algoritma DFS bekerja melalui langkah-langkah berikut:
1.  Masukkan simpul (node) akar ke dalam *stack*.
2.  Ambil satu simpul dari bagian teratas *stack*, lalu periksa apakah simpul tersebut merupakan solusi yang dicari.
    * Jika ya, pencarian selesai dan hasilnya dikembalikan.
    * Jika bukan, masukkan seluruh node anak (tetangga yang belum dikunjungi) dari simpul tersebut ke dalam *stack*.
3.  Jika *stack* tidak kosong, ulangi proses pencarian dari langkah ke-2.
4.  Jika *stack* kosong dan setiap simpul sudah diperiksa, maka pencarian berakhir.

***

## Permasalahan

Bayangkan kamu sedang membuat aplikasi manajemen sistem file seperti File Explorer. Sistem file terdiri dari direktori (folder) dan file yang disusun secara hierarkis, di mana setiap folder bisa berisi file dan folder lainnya.

Tugas kamu adalah menelusuri seluruh file dan folder yang berada di dalam folder utama (root) dan mencetak nama semua file yang ditemukan.

Struktur folder:
Root
├── Folder1
│ ├── FileA
│ └── FileB
├── Folder2
│ ├── Folder3
│ │ └── FileC
│ └── FileD
└── FileE


Bagaimana kita bisa menjelajahi seluruh struktur ini secara rekursif?

---

## Solusi (Dengan Implementasi C++)

Untuk menyelesaikan masalah ini, kita akan menggunakan DFS untuk menjelajahi semua direktori dan file yang bersarang di dalam folder root.

### 💻 Kode C++

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <string>
using namespace std;

// Representasi struktur file sebagai graf
unordered_map<string, vector<string>> fileSystem = {
    {"Root", {"Folder1", "Folder2", "FileE"}},
    {"Folder1", {"FileA", "FileB"}},
    {"Folder2", {"Folder3", "FileD"}},
    {"Folder3", {"FileC"}},
    {"FileA", {}},
    {"FileB", {}},
    {"FileC", {}},
    {"FileD", {}},
    {"FileE", {}}
};

void dfs(const string& current, int depth = 0) {
    for (int i = 0; i < depth; ++i) cout << "  "; // indentasi
    cout << "- " << current << "\n";

    for (const string& child : fileSystem[current]) {
        dfs(child, depth + 1);
    }
}

int main() {
    cout << "Isi sistem file:\n";
    dfs("Root");
    return 0;
}

Output:
Isi sistem file:
- Root
  - Folder1
    - FileA
    - FileB
  - Folder2
    - Folder3
      - FileC
    - FileD
  - FileE

```

### Kelebihan dan Kekurangan

Sama seperti algoritma lainnya, DFS memiliki kelebihan dan kekurangan.

**Kelebihan :**
* Penggunaan memori lebih efisien.
* Mudah diimplementasikan.
* Sangat cocok untuk menemukan solusi pada kedalaman maksimal.
* Menjadi dasar bagi banyak algoritma penting.

**Kekurangan :**
* Tidak menjamin penemuan solusi terbaik atau terpendek.
* Bisa terjebak dalam *infinite loop* jika diimplementasikan pada graf siklik tanpa penanganan node yang sudah dikunjungi.
* Kurang efisien jika diterapkan pada graf yang sangat luas tetapi dangkal.
* Tidak cocok untuk semua jenis masalah pencarian.

***

### Kesimpulan

*Depth-First Search* (DFS) adalah algoritma penelusuran yang menjelajahi simpul sedalam mungkin pada satu cabang sebelum melakukan *backtracking* untuk melanjutkan ke simpul lainnya. Proses penelusuran ini dilakukan dengan bantuan struktur data *stack* yang bekerja berdasarkan prinsip LIFO (*Last-In, First-Out*). Penelusuran dimulai dari simpul akar, lalu terus menyusuri anak-anak simpul hingga mencapai simpul terdalam, sebelum kembali untuk menjelajahi cabang lain yang belum dikunjungi. DFS sangat cocok digunakan untuk pencarian solusi yang berada di kedalaman maksimal dan dapat menghasilkan jalur penelusuran yang berbeda-beda tergantung urutan pemrosesan simpulnya.

---

![Desktop View](https://i.pinimg.com/736x/72/5c/e4/725ce4ffc8bfc9772f8d677ba387ebb2.jpg){: width="300"}
_----_

---