---
title: HUFFMAN CODING
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]     # TAG names should always be lowercase
---
Dalam dunia digital modern, efisiensi dalam penyimpanan dan transmisi data adalah hal yang sangat penting. Dari pesan teks, file gambar, hingga data audio—semuanya harus dikompresi seefisien mungkin agar dapat disimpan dan dikirimkan dengan cepat dan hemat ruang. Salah satu teknik kompresi data yang paling dikenal dan banyak digunakan adalah **Huffman Coding**.

**Huffman Coding** adalah algoritma pengkodean lossless yang digunakan untuk mengompresi data berdasarkan frekuensi kemunculan karakter. Intinya, karakter yang sering muncul akan diberikan kode yang lebih pendek, sementara karakter yang jarang muncul akan mendapatkan kode yang lebih panjang. Hal ini membuat total ukuran data setelah dikodekan menjadi lebih kecil dibandingkan representasi aslinya.

### 📚 Mengapa Penting?

Huffman Coding adalah pondasi dari berbagai sistem kompresi seperti:

- Format file: JPEG, MP3, PNG
- Protokol komunikasi
- Kompresi teks dan data dalam sistem informasi

Dengan mengerti bagaimana Huffman Coding bekerja, kita memahami cara komputer berpikir secara efisien dalam mengelola informasi.

---

### Konsep Dasar

Prinsip kerja Huffman Coding didasarkan pada frekuensi karakter dalam data.

* Karakter dengan frekuensi tinggi akan diberikan kode yang lebih pendek.
* Karakter dengan frekuensi rendah akan diberikan kode yang lebih panjang.
* Representasi data menggunakan pohon biner.

## Proses Pembuatan Kode

Langkah-langkah dalam proses pembuatan kode Huffman Coding adalah sebagai berikut:
1.  Hitung frekuensi tiap karakter dalam data.
2.  Buat simpul (*node*) untuk setiap karakter.
3.  Gabungkan dua simpul dengan frekuensi terkecil.
4.  Ulangi langkah 3 hingga terbentuk satu pohon Huffman.
5.  Tentukan kode biner untuk tiap karakter (0 untuk sisi kiri, 1 untuk sisi kanan).

## Permasalahan


Tugas Anda adalah membuat representasi **bit** dari string tersebut menggunakan Huffman Coding sehingga total panjang bit-nya menjadi sekecil mungkin. Setiap karakter dalam string memiliki frekuensi tertentu, dan kita ingin menyandikan setiap karakter dengan bit yang panjangnya bervariasi berdasarkan frekuensinya.

---

## ✅ Solusi (Dengan Implementasi C++)

### 💡 Langkah-Langkah Huffman Coding:

1. Hitung frekuensi setiap karakter.
2. Buat node untuk setiap karakter dan simpan di min-heap berdasarkan frekuensi.
3. Gabungkan dua node dengan frekuensi terkecil menjadi node baru.
4. Ulangi langkah 3 hingga tinggal satu node → ini adalah **akar pohon Huffman**.
5. Lakukan traversal untuk menghasilkan kode Huffman untuk setiap karakter.

---

### 💻 Kode C++

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
#include <vector>
using namespace std;

// Struktur node untuk Huffman Tree
struct Node {
    char ch;
    int freq;
    Node *left, *right;

    Node(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
};

// Perbandingan untuk priority_queue
struct Compare {
    bool operator()(Node* a, Node* b) {
        return a->freq > b->freq;
    }
};

// Fungsi rekursif untuk menghasilkan kode Huffman
void generateCodes(Node* root, string code, unordered_map<char, string>& huffmanCode) {
    if (!root) return;

    if (!root->left && !root->right) {
        huffmanCode[root->ch] = code;
    }

    generateCodes(root->left, code + "0", huffmanCode);
    generateCodes(root->right, code + "1", huffmanCode);
}

// Fungsi utama
void huffmanCoding(string text) {
    unordered_map<char, int> freq;
    for (char ch : text) {
        freq[ch]++;
    }

    priority_queue<Node*, vector<Node*>, Compare> pq;

    for (auto pair : freq) {
        pq.push(new Node(pair.first, pair.second));
    }

    // Bangun pohon Huffman
    while (pq.size() > 1) {
        Node* left = pq.top(); pq.pop();
        Node* right = pq.top(); pq.pop();

        Node* merged = new Node('\0', left->freq + right->freq);
        merged->left = left;
        merged->right = right;

        pq.push(merged);
    }

    Node* root = pq.top();
    unordered_map<char, string> huffmanCode;
    generateCodes(root, "", huffmanCode);

    cout << "Kode Huffman:\n";
    for (auto pair : huffmanCode) {
        cout << pair.first << " : " << pair.second << '\n';
    }

    cout << "\nTeks Asli: " << text << '\n';

    cout << "Teks Terkompresi (bit): ";
    for (char ch : text) {
        cout << huffmanCode[ch];
    }
    cout << endl;
}

int main() {
    string text = "FAHIRAFAHIRA";
    huffmanCoding(text);
    return 0;
}

Output:
Kode Huffman:
                F : 00
                A : 01
                H : 10
                I : 110
                R : 111

Teks Asli: FAHIRAFAHIRA
Teks Terkompresi (bit): 0001101011110100011010111101



## Kelebihan dan Kekurangan Huffman Coding

### Kelebihan
* ✅**Lossless:** Tidak ada data yang hilang selama proses kompresi, artinya data yang didekompresi identik dengan data aslinya.
* ✅**Efisien:** Sangat efisien untuk data dengan distribusi karakter yang tidak merata (ada karakter yang jauh lebih sering muncul daripada yang lain).
* ✅**Digunakan Luas:** Merupakan dasar dan digunakan luas di berbagai sistem kompresi file.

### Kekurangan
* ❌**Kurang Optimal:** Kurang optimal jika frekuensi karakter merata (semua karakter muncul dengan frekuensi yang hampir sama), karena perbedaan panjang kode tidak akan signifikan.
* ❌**Memerlukan Tabel Kode:** Memerlukan tabel kode (pohon Huffman) untuk dekompresi. Tabel ini harus disimpan bersama dengan data terkompresi atau dibuat ulang, yang menambah sedikit *overhead*.

![Desktop View](https://upload-os-bbs.hoyolab.com/upload/2024/01/09/137652040/586aa1a23ffe39e6955e3d49bd0c59bc_6338591603245794027.jpg?x-oss-process=image%2Fresize%2Cs_1000%2Fauto-orient%2C0%2Finterlace%2C1%2Fformat%2Cwebp%2Fquality%2Cq_70){: width="450"}
_---_

