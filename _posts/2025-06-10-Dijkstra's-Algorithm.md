---
title: DIJKSTRA's ALGORITHM
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DIJKSTRA's ALGORITHM]
tags: [daa, algorithm, backtracking, dijkstra]    
---


### Apa itu Algoritma Dijkstra?

**Algoritma Dijkstra** adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik dalam sebuah graf. Graf ini bisa berupa jaringan yang terdiri dari simpul (titik) dan sisi (hubungan antar titik) dengan bobot tertentu pada sisi-sisinya. Algoritma ini membantu kita menentukan jalur terpendek dari titik awal ke titik tujuan.

-----

### Cara Kerja Algoritma Dijkstra

Algoritma ini bekerja dengan langkah-langkah sistematis sebagai berikut:

1.  Buat sebuah tabel dengan kolom sebagai tempat nilai atau jarak dari simpul, dan baris sebagai posisi simpul.
2.  Pilih simpul awal dan simpul tujuan, dengan syarat keduanya harus terhubung secara langsung.
3.  Hitung jarak untuk beberapa simpul tujuan yang telah dipilih.
4.  Setelah semua simpul diuji, pilih jarak yang terpendek.
5.  Simpul yang dipilih akan menjadi acuan untuk tahap selanjutnya, dan proses diulangi hingga semua simpul telah diuji.

-----

# Algoritma Dijkstra: Rute Tercepat dari Rumah ke Kampus

## Deskripsi Permasalahan

Seorang mahasiswa ingin menemukan **rute tercepat dari rumah ke kampus**. Terdapat beberapa persimpangan dan jalan dengan estimasi waktu tempuh berbeda-beda. Mahasiswa tersebut ingin mengetahui jalur mana yang paling efisien agar tidak terlambat mengikuti perkuliahan.

### 🗺️ Representasi Simpul
- **Rumah**
- **A**
- **B**
- **C**
- **D**
- **Kampus**

### 🛣️ Representasi Jaringan Jalan (Graf Berbobot)
| Dari   | Ke     | Waktu (menit) |
|--------|--------|----------------|
| Rumah  | A      | 5              |
| Rumah  | C      | 9              |
| A      | B      | 2              |
| B      | D      | 3              |
| C      | D      | 4              |
| D      | Kampus | 7              |

## ⚙️ Algoritma yang Digunakan
Permasalahan ini diselesaikan dengan **Algoritma Dijkstra**, yaitu algoritma pencarian jalur terpendek dalam graf berbobot dan tak bertanda negatif.

---

## 💻 Implementasi dalam C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

const int INF = INT_MAX;
const int N = 6; // jumlah simpul: Rumah, A, B, C, D, Kampus

string nodeNames[N] = {"Rumah", "A", "B", "C", "D", "Kampus"};

void dijkstra(int graph[N][N], int start) {
    vector<int> dist(N, INF);
    vector<bool> visited(N, false);
    vector<int> parent(N, -1);

    dist[start] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, start});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        if (visited[u]) continue;
        visited[u] = true;

        for (int v = 0; v < N; ++v) {
            if (graph[u][v] && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
                parent[v] = u;
                pq.push({dist[v], v});
            }
        }
    }

    int end = 5; // indeks Kampus
    cout << "Waktu tercepat dari Rumah ke Kampus: " << dist[end] << " menit" << endl;

    vector<int> path;
    for (int v = end; v != -1; v = parent[v]) {
        path.push_back(v);
    }
    reverse(path.begin(), path.end());

    cout << "Rute tercepat: ";
    for (size_t i = 0; i < path.size(); ++i) {
        cout << nodeNames[path[i]];
        if (i != path.size() - 1) cout << " -> ";
    }
    cout << endl;
}

int main() {
    int graph[N][N] = {
        { 0, 5, 0, 9, 0, 0 }, // Rumah
        { 0, 0, 2, 0, 0, 0 }, // A
        { 0, 0, 0, 0, 3, 0 }, // B
        { 0, 0, 0, 0, 4, 0 }, // C
        { 0, 0, 0, 0, 0, 7 }, // D
        { 0, 0, 0, 0, 0, 0 }  // Kampus
    };

    dijkstra(graph, 0); // mulai dari node Rumah (indeks 0)
    return 0;
}

```
-----

### Contoh Penggunaan lain

  * **Pengiriman Barang**: Sebuah perusahaan ekspedisi yang ingin mengirim paket dari gudang ke beberapa pelanggan dapat menggunakan Algoritma Dijkstra untuk menentukan rute pengiriman yang paling efisien agar paket sampai lebih cepat dan tidak boros bensin atau tenaga.

-----

### Kelebihan dan Kekurangan

#### Kelebihan 👍

  * **Menjamin Jalur Terpendek**: Dijkstra selalu menemukan solusi yang optimal (jalur terpendek) selama semua bobot sisi bernilai positif.
  * **Efisien untuk Banyak Aplikasi**: Algoritma ini sangat cocok untuk graf yang padat dan sering digunakan dalam aplikasi nyata seperti GPS dan *routing* jaringan.
  * **Dapat Menyelesaikan Banyak Tujuan Sekaligus**: Dengan sekali eksekusi dari satu titik awal, algoritma ini bisa memberikan informasi jarak terpendek ke semua titik lainnya.

#### Kekurangan 👎

  * **Tidak Bekerja dengan Bobot Negatif**: Algoritma ini tidak dapat digunakan jika ada sisi dengan bobot negatif.
  * **Kurang Efisien untuk Graf Besar yang Jarang Terhubung**: Pada graf yang sangat besar dan *sparse* (jarang terhubung), kinerjanya bisa menjadi lambat jika tidak dioptimalkan dengan struktur data *priority queue*.
  * **Perhitungan Bisa Terlalu Luas**: Jika hanya mencari jalur dari A ke B, Dijkstra tetap menghitung jarak ke semua titik lain, yang terkadang tidak efisien. Untuk kasus seperti ini, algoritma lain seperti A\* (A-Star) bisa lebih baik.

-----

### Kesimpulan

Algoritma Dijkstra merupakan salah satu algoritma pencarian jalur terpendek yang paling efisien dan banyak digunakan dalam teori graf. Algoritma ini bekerja dengan cara mencari jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot non-negatif. Melalui pendekatan *greedy*, Dijkstra memastikan bahwa setiap langkahnya mendekatkan solusi menuju hasil optimal. Keunggulan utama algoritma ini terletak pada keakuratannya dan efisiensinya, terutama jika dikombinasikan dengan struktur data seperti *priority queue* atau *min-heap*. Dalam implementasi praktis, algoritma Dijkstra sangat berguna dalam berbagai bidang seperti jaringan komputer, sistem navigasi, dan pemodelan transportasi.