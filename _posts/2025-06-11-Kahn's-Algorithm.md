---
title: KAHN'S ALGORITHM
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, KAHN'S ALGORITHM]
tags: [daa, algorithm, backtracking, kahn]     # TAG names should always be lowercase
---

Dalam berbagai sistem seperti manajemen proyek, kompilasi program, dan pemrosesan data, sering kali kita menemui ketergantungan antar tugas atau proses. Misalnya, dalam proyek pembangunan rumah, fondasi harus selesai terlebih dahulu sebelum dinding dapat dibangun, dan dinding harus selesai sebelum atap dapat dipasang. Hubungan semacam ini membentuk struktur yang disebut **graf berarah tanpa siklus (DAG - Directed Acyclic Graph)**.

Untuk menyelesaikan tugas-tugas seperti ini, kita membutuhkan **topological sorting**, yaitu urutan tugas sedemikian rupa sehingga setiap tugas dilakukan setelah semua tugas yang menjadi prasyaratnya selesai. Di sinilah **Kahn’s Algorithm** menjadi penting.

**Kahn’s Algorithm** adalah salah satu algoritma paling populer dan efisien untuk melakukan topological sort pada graf berarah tanpa siklus. Algoritma ini bekerja dengan pendekatan **BFS (Breadth-First Search)** dan secara sistematis memproses simpul yang tidak memiliki ketergantungan (in-degree nol), sambil terus memperbarui ketergantungan dari simpul-simpul lainnya.


### Kapan Algoritma Kahn Dibutuhkan?

Algoritma ini sangat berguna dalam berbagai skenario praktis, seperti:
* Menjadwalkan tugas berdasarkan dependensi.
* Mendeteksi adanya siklus dalam sebuah grafik terarah.
* Memproses dependensi dalam urutan yang benar.

### Bagaimana Algoritma Kahn Bekerja?

Proses kerja Algoritma Kahn mengikuti langkah-langkah berikut:
1.  Gunakan struktur *in-degree* (jumlah sisi masuk) untuk tiap simpul.
2.  Tambahkan semua simpul dengan *in-degree* = 0 ke dalam sebuah antrean (*queue*).
3.  Proses antrean satu per satu.
4.  Jika semua simpul telah diproses, maka dapat dipastikan graf tersebut tidak memiliki siklus.

## ❓ Permasalahan

Bayangkan kamu mengembangkan sistem kompilasi proyek perangkat lunak yang memiliki ketergantungan antar modul. Misalnya, kamu harus mengkompilasi file `parser.cpp` sebelum `compiler.cpp`, dan `compiler.cpp` sebelum `main.cpp`. Tugasmu adalah menentukan urutan kompilasi yang benar agar semua file dapat dikompilasi tanpa kesalahan dependensi.

### 🎯 Input:
- Jumlah simpul (tugas/modul).
- Daftar ketergantungan antar simpul dalam bentuk pasangan `(a, b)` yang artinya **`a` harus diselesaikan sebelum `b`**.

### 🎯 Output:
- Urutan topologis dari simpul, atau pesan kesalahan jika terdapat siklus (urutan tidak mungkin).

---

## ✅ Solusi (Implementasi C++)

### 💡 Langkah-langkah Kahn’s Algorithm:

1. Hitung in-degree (jumlah masuknya sisi) untuk setiap simpul.
2. Masukkan semua simpul dengan in-degree = 0 ke dalam queue.
3. Selama queue tidak kosong:
   - Ambil simpul dari queue dan masukkan ke urutan topologis.
   - Kurangi in-degree semua simpul tetangganya.
   - Jika in-degree salah satu simpul menjadi 0, masukkan ke queue.
4. Jika semua simpul telah diproses → urutan valid.
5. Jika tidak → terdapat siklus dalam graf.

---

### 💻 Kode C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

void kahnAlgorithm(int V, vector<vector<int>>& adj) {
    vector<int> in_degree(V, 0);

    // Hitung in-degree setiap simpul
    for (int i = 0; i < V; i++) {
        for (int neighbor : adj[i]) {
            in_degree[neighbor]++;
        }
    }

    queue<int> q;
    // Masukkan semua simpul dengan in-degree 0
    for (int i = 0; i < V; i++) {
        if (in_degree[i] == 0)
            q.push(i);
    }

    vector<int> topo_order;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        topo_order.push_back(node);

        for (int neighbor : adj[node]) {
            in_degree[neighbor]--;
            if (in_degree[neighbor] == 0)
                q.push(neighbor);
        }
    }

    // Cek apakah ada siklus
    if (topo_order.size() != V) {
        cout << "Terdapat siklus, topological sort tidak mungkin.\n";
    } else {
        cout << "Urutan Topological: ";
        for (int node : topo_order) {
            cout << node << " ";
        }
        cout << endl;
    }
}

int main() {
    int V = 6;
    vector<vector<int>> adj(V);

    // Misal: 5->0, 5->2, 4->0, 4->1, 2->3, 3->1
    adj[5].push_back(0);
    adj[5].push_back(2);
    adj[4].push_back(0);
    adj[4].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(1);

    kahnAlgorithm(V, adj);
    return 0;
}

Output:

Urutan Topological: 4 5 2 3 1 0 
```
-----

### Kelebihan dan Kekurangan

**Kelebihan:**
* **Kompleksitas Waktu Efisien**: Memiliki kompleksitas waktu $O(V+E)$ yang sangat efisien.
* **Deteksi Siklus**: Dapat dengan mudah mendeteksi adanya siklus dalam sebuah graf berarah.
* **Relevan untuk Masalah Dependensi**: Sangat cocok untuk menyelesaikan masalah yang melibatkan dependensi seperti prasyarat mata kuliah, *build system*, atau manajemen tugas proyek.

**Kekurangan:**
* **Tidak untuk Graf Bersiklus**: Algoritma ini tidak dapat digunakan pada graf yang mengandung siklus.
* **Output Bervariasi**: Dapat menghasilkan lebih dari satu urutan topologis yang valid.
* **Memerlukan Struktur Data Tambahan**: Membutuhkan struktur data tambahan seperti array atau map untuk menyimpan *in-degree* dan representasi graf itu sendiri.

### Kesimpulan

Algoritma Kahn merupakan metode yang efisien dan sistematis untuk melakukan *topological sorting* pada *Directed Acyclic Graph* (DAG). Dengan memanfaatkan struktur *in-degree* dan antrean, algoritma ini mampu menyusun simpul-simpul berdasarkan ketergantungan yang ada, serta mendeteksi keberadaan siklus dalam graf. Implementasinya dalam bahasa C++ memperlihatkan bagaimana struktur data seperti `unordered_map` dan `vector` dapat digunakan untuk memodelkan graf dan proses penyusunannya secara elegan. Dengan kompleksitas waktu $O(V+E)$, algoritma ini sangat berguna dalam berbagai aplikasi nyata, seperti penjadwalan tugas, kompilasi program, dan pengelolaan prasyarat mata kuliah.