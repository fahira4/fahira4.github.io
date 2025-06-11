---
title: BREADTH-FIRST SEARCH (BFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, BFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, bfs]     # TAG names should always be lowercase
---

---

Dalam dunia pemrograman dan rekayasa perangkat lunak, struktur data graf merupakan salah satu alat paling kuat untuk memodelkan hubungan antar objek. Di dalam graf, simpul (nodes) mewakili entitas, dan sisi (edges) mewakili koneksi antar entitas tersebut. Salah satu algoritma dasar yang digunakan untuk menelusuri graf adalah Breadth-First Search (BFS).

Breadth-First Search adalah teknik penelusuran graf yang bekerja dengan menjelajahi seluruh simpul pada satu tingkat (level) sebelum melanjutkan ke tingkat berikutnya. Ini dilakukan menggunakan struktur data antrian (queue) untuk memastikan bahwa simpul-simpul yang lebih awal ditemukan akan diproses lebih dahulu. BFS menjamin bahwa jika ada jalur dari simpul awal ke simpul tujuan, maka jalur pertama yang ditemukan adalah jalur dengan jumlah langkah (edges) paling sedikit, meskipun bukan selalu jalur dengan bobot terkecil jika bobot digunakan.

BFS sangat efisien ketika diterapkan pada graf tak berbobot dan memiliki banyak aplikasi di dunia nyata. Di antaranya:
- Sistem penunjuk arah atau navigasi pada peta (seperti Google Maps)
- Pencarian teman terdekat dalam jejaring sosial (misalnya: mencari teman yang hanya berjarak 1–2 tingkat koneksi)
- Web crawling (mengindeks halaman web berdasarkan tautan)
- Analisis jaringan komputer
- Sistem antrian pada game untuk menjangkau area terdekat terlebih dahulu

Dengan memahami dan mengimplementasikan BFS, kita bisa menyelesaikan berbagai masalah penting yang berkaitan dengan konektivitas, penjadwalan, dan optimalisasi sistem.

---

***

### Konsep Dasar dan Cara Kerja BFS

Konsep utama di balik BFS sangat sederhana dan sistematis.

* **Menggunakan Antrian (*Queue*)**: BFS memanfaatkan struktur data *queue* (antrian) untuk mengelola urutan simpul yang akan dikunjungi.
* **Penelusuran per Level**: Algoritma ini memulai dari simpul awal, mengunjungi semua tetangganya, lalu melanjutkan ke tetangga dari tetangga tersebut, dan seterusnya. Proses ini memastikan penelusuran terjadi lapis demi lapis, yang juga dikenal sebagai *level-order traversal*.

***

### Langkah-Langkah Algoritma

Proses pencarian menggunakan BFS mengikuti langkah-langkah berikut:
1.  **Tentukan Simpul Awal**: Pilih satu simpul sebagai titik awal (*start node*).
2.  **Masukkan ke Antrian**: Masukkan simpul awal tersebut ke dalam *queue*.
3.  **Proses Antrian**: Selama *queue* tidak kosong, lakukan langkah-langkah berikut:
    * Ambil simpul terdepan dari *queue* dan tandai sebagai simpul yang telah dikunjungi.
    * Periksa apakah simpul ini adalah tujuan (*goal node*). Jika ya, pencarian selesai.
    * Jika bukan tujuan, kunjungi semua tetangga dari simpul ini yang belum pernah dikunjungi.
    * Tandai semua tetangga tersebut sebagai "sudah dikunjungi" dan masukkan mereka ke dalam *queue*.
4.  **Ulangi**: Ulangi proses hingga tujuan ditemukan atau *queue* menjadi kosong, yang menandakan tidak ada jalur yang ditemukan.



Berikut adalah simulasi cara kerja BFS pada sebuah graf dengan **S** sebagai *start node* dan **G** sebagai *goal node*.

| SIMPUL AKTIF | QUEUE | VISITED |
| :--- | :--- | :--- |
| **S** | S | S |
| **A** | A, B | SA |
| **B** | B, C, D | SAB |
| **C** | C, D, E, F | SABC |
| **D** | D, E, F | SABCD |
| **E** | E, F | SABCDE |
| **F** | F, H, G | SABCDEF |
| **H** | H, G | SABCDEFH |
| **G** | G | SABCDEFHG |

***

## ❓ Permasalahan

Bayangkan kamu adalah pengelola sistem transportasi di sebuah kota yang terdiri dari beberapa stasiun metro. Stasiun-stasiun ini terhubung melalui jalur kereta tanpa bobot (semua jarak dianggap sama). Kamu ingin membuat fitur **pencarian jalur tercepat** (dalam jumlah stasiun yang dilalui) dari satu stasiun ke stasiun lainnya.

Berikut adalah peta sambungan antar stasiun:
Stasiun: A, B, C, D, E, F, G
Koneksi:
A - B
A - C
B - D
C - E
D - F
E - F
F - G


Tujuannya adalah untuk mencari tahu:
- Apakah stasiun G dapat dicapai dari stasiun A?
- Jika ya, berapa banyak langkah minimum yang harus ditempuh?
- Jalur apa saja yang mungkin dilalui?

---

## ✅ Solusi (Dengan Implementasi C++)

Untuk menyelesaikan masalah ini, kita akan menerapkan algoritma BFS yang melacak:
1. Simpul yang telah dikunjungi
2. Jumlah langkah dari simpul awal
3. Jalur yang dilalui (dengan menggunakan map untuk melacak parent)

### 💻 Kode C++

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>
#include <vector>
#include <set>
#include <stack>
using namespace std;

void bfs(const unordered_map<string, vector<string>>& graph, const string& start, const string& end) {
    queue<string> q;
    unordered_map<string, string> parent; // Untuk merekonstruksi jalur
    set<string> visited;

    q.push(start);
    visited.insert(start);
    parent[start] = "";

    while (!q.empty()) {
        string current = q.front();
        q.pop();

        if (current == end) break;

        for (const string& neighbor : graph.at(current)) {
            if (visited.find(neighbor) == visited.end()) {
                visited.insert(neighbor);
                parent[neighbor] = current;
                q.push(neighbor);
            }
        }
    }

    if (parent.find(end) == parent.end()) {
        cout << "Tidak ada jalur dari " << start << " ke " << end << ".\n";
        return;
    }

    // Hitung langkah dan tampilkan jalur
    vector<string> path;
    string node = end;
    while (node != "") {
        path.push_back(node);
        node = parent[node];
    }

    reverse(path.begin(), path.end());

    cout << "Jalur ditemukan dari " << start << " ke " << end << " dalam " << path.size() - 1 << " langkah:\n";
    for (size_t i = 0; i < path.size(); ++i) {
        cout << path[i];
        if (i < path.size() - 1) cout << " -> ";
    }
    cout << endl;
}

int main() {
    unordered_map<string, vector<string>> graph = {
        {"A", {"B", "C"}},
        {"B", {"A", "D"}},
        {"C", {"A", "E"}},
        {"D", {"B", "F"}},
        {"E", {"C", "F"}},
        {"F", {"D", "E", "G"}},
        {"G", {"F"}}
    };

    string start = "A";
    string end = "G";

    bfs(graph, start, end);

    return 0;
}

### Contoh Kode (C++)

Berikut adalah implementasi sederhana dari algoritma BFS menggunakan C++.

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <algorithm>

using namespace std;

// Inisialisasi graf dengan adjacency list
unordered_map<char, vector<char>> graf;
// Menyimpan simpul yang sudah dikunjungi
unordered_map<char, bool> sudahDikunjungi;
// Menyimpan jalur: simpul_sekarang -> simpul_sebelumnya (parent)
unordered_map<char, char> parent;

void bfs(char start, char goal) {
    queue<char> q;
    q.push(start);
    sudahDikunjungi[start] = true;
    parent[start] = '/0'; // Titik awal tidak punya parent

    while (!q.empty()) {
        char sekarang = q.front();
        q.pop();

        cout << "Kunjungi node: " << sekarang << endl;

        // Jika goal ditemukan, hentikan pencarian
        if (sekarang == goal) break;

        // Iterasi ke semua tetangga dari node 'sekarang'
        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }
    }

    // Cetak jalur terpendek dari goal ke start
    cout << "/n=== HASIL ===" << endl;
    cout << "Start Node: " << start << endl;
    cout << "Goal Node: " << goal << endl;

    vector<char> jalur;
    char current = goal;
    while (current != '/0') {
        jalur.push_back(current);
        current = parent[current];
    }
    reverse(jalur.begin(), jalur.end()); // Balik urutan jalur

    cout << "Jalur Terpendek: ";
    for (size_t i = 0; i < jalur.size(); i++) {
        cout << jalur[i];
        if (i != jalur.size() - 1) cout << " -> ";
    }
    cout << endl;
}

Output:
Jalur ditemukan dari A ke G dalam 4 langkah:
A -> B -> D -> F -> G

```

***

### Aplikasi Nyata BFS

BFS sangat efektif dan banyak digunakan dalam berbagai aplikasi dunia nyata.

* **Pencarian Jalur dalam Labirin atau Game**: BFS digunakan untuk menemukan jalan terpendek dari titik awal ke tujuan. Contohnya adalah game Pac-Man yang menghitung rute terpendek untuk mengejar pemain.
* **Rekomendasi di Media Sosial**: Platform seperti Facebook dan LinkedIn menggunakan BFS untuk fitur "Orang yang Mungkin Anda Kenal". Algoritma ini bekerja dengan menelusuri teman langsung (level 1), lalu teman dari teman (level 2), dan seterusnya.
* **Pemetaan Jaringan Komputer**: BFS dapat memetakan semua perangkat (PC, server, router) dalam sebuah jaringan. Dimulai dari router utama, BFS akan menelusuri perangkat yang terhubung per level, seperti switch di level 1 dan PC di level 2.
* **Sistem Navigasi dan Transportasi**: Aplikasi seperti Google Maps, Grab, atau Gojek menggunakan BFS untuk menemukan rute terpendek, terutama jika semua jalur dianggap memiliki bobot yang sama (misalnya, mencari rute dengan jumlah persimpangan paling sedikit).

***

### Kelebihan dan Kekurangan

* **Kelebihan**: BFS menjamin penemuan solusi yang paling baik (optimal dan komplit), terutama untuk mencari jalur terpendek pada graf tak berbobot.
* **Kekurangan**: Membutuhkan memori dan waktu yang cukup banyak, terutama jika graf atau pohon sangat lebar.

***

### Kesimpulan

BFS adalah algoritma penelusuran graf yang menjelajahi simpul secara berlapis dari titik awal. Dengan bantuan struktur data *queue*, BFS memastikan semua simpul terdekat dijelajahi terlebih dahulu, menjadikannya metode yang ideal untuk mencari jalur terpendek pada graf tak berbobot. Berkat efektivitasnya, BFS banyak diterapkan dalam berbagai aplikasi modern, mulai dari game, peta digital, hingga analisis jaringan sosial.

![Desktop View](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTttgR1killt0xv2UYUV1Gkc9eU4_eSviJYmA&s){: width="350"}
_---_
