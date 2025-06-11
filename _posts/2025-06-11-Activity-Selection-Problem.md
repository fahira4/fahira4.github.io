---
title: ACTIVITY SELECTION PROBLEM
date: 2025-05-06
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]     # TAG names should always be lowercase
---

HI!. Kali ini kita akan membahas sebuah konsep fundamental dalam bidang algoritma dan optimasi, yaitu **Activity Selection Problem**.

---

Dalam kehidupan sehari-hari maupun dalam sistem komputasi, kita kerap dihadapkan pada kebutuhan untuk menjadwalkan serangkaian aktivitas secara efisien. Setiap aktivitas memiliki batasan waktu tertentu—kapan dimulai dan kapan harus selesai—sementara sumber daya yang tersedia, seperti ruang pertemuan, tenaga kerja, atau prosesor, hanya mampu menangani satu aktivitas dalam satu waktu.

Permasalahan muncul ketika jumlah aktivitas melebihi kapasitas penanganan secara bersamaan. Di sinilah kita perlu menjawab pertanyaan penting: Bagaimana memilih kombinasi aktivitas sebanyak mungkin tanpa terjadi tumpang tindih waktu? Tujuan akhirnya adalah memaksimalkan jumlah aktivitas yang dapat dijalankan tanpa saling mengganggu.

Inilah inti dari Activity Selection Problemsebuah studi klasik dalam dunia algoritma yang mengajarkan kita pentingnya membuat keputusan secara strategis. Dengan pendekatan algoritma *greedy*, kita berupaya memilih aktivitas satu per satu dengan mengutamakan waktu selesai paling awal. Pendekatan ini terbukti mampu memberikan hasil yang optimal dalam banyak kasus nyata.

Memahami dan mengimplementasikan solusi untuk masalah ini tidak hanya membangun fondasi berpikir algoritmik, tetapi juga memberikan manfaat nyata dalam bidang penjadwalan, pengelolaan proyek, alokasi tugas, dan optimalisasi sistem.

Mari kita eksplorasi lebih jauh dan temukan bagaimana keputusan sederhana yang tepat waktu dapat menghasilkan efisiensi maksimal.

---


## Pendahuluan dan Definisi Masalah

**Activity Selection Problem** adalah masalah pemilihan aktivitas maksimum yang tidak saling tumpang tindih. Diberikan sekumpulan aktivitas dengan waktu mulai dan waktu selesai. Tujuan utamanya adalah memilih jumlah aktivitas maksimum yang dapat dilakukan oleh satu orang/resource.

Activity Selection Problem merupakan masalah optimasi klasik dalam ilmu komputer. Kita diberikan sejumlah aktivitas yang masing-masing didefinisikan dengan waktu mulai dan waktu selesai . Dua aktivitas dikatakan kompatibel jika mereka tidak tumpang tindih secara waktu, artinya salah satu aktivitas selesai sebelum aktivitas lainnya dimulai. Tantangannya adalah menentukan subset terbesar dari aktivitas yang semuanya kompatibel satu sama lain.

## Konsep Dasar Algoritma Greedy

Algoritma *greedy* adalah strategi pemecahan masalah optimasi yang bekerja dengan membuat pilihan yang tampak paling baik pada setiap langkah, dengan harapan rangkaian pilihan ini akan mengarah pada solusi yang optimal secara keseluruhan. Algoritma ini bersifat "serakah" karena langsung mengambil pilihan terbaik saat itu tanpa mempertimbangkan konsekuensi di masa depan.

Dalam konteks Activity Selection Problem, algoritma *greedy* secara efektif diterapkan dengan memilih aktivitas yang memiliki waktu selesai paling awal di setiap langkah. Pemilihan yang optimal ini didasarkan pada gagasan bahwa dengan menyelesaikan suatu aktivitas lebih awal, kita memaksimalkan sisa waktu yang tersedia untuk memilih aktivitas-aktivitas lain yang tidak bertabrakan. Strategi *greedy* ini terbukti menghasilkan solusi dengan jumlah aktivitas maksimal yang dapat dipilih tanpa adanya konflik waktu.

## Algoritma Activity Selection Problem

Algoritma Activity Selection Problem menggunakan pendekatan *greedy* dengan memilih aktivitas berdasarkan waktu selesai (*finish time*). Ide kuncinya adalah dengan memilih aktivitas yang selesai paling awal, kita memaksimalkan waktu tersisa untuk aktivitas lainnya.

Langkah-langkah algoritma:
1.  Urutkan semua aktivitas berdasarkan waktu selesai (*finish time*).
2.  Pilih aktivitas pertama (aktivitas dengan waktu selesai paling awal).
3.  Untuk aktivitas berikutnya, pilih jika waktu mulainya lebih besar atau sama dengan waktu selesai aktivitas yang dipilih sebelumnya.

### Pseudocode

```bash
ACTIVITY-SELECTOR(s, f, n)
A = {a1} // Pilih aktivitas pertama
j = 1
for i = 2 to n
    if s[i] >= f[j] // Waktu mulai lebih besar atau sama dengan waktu selesai
        A = A U {ai} // Pilih aktivitas ai
        j = i // Update aktivitas terakhir yang dipilih
return A
```
* `s` adalah array yang berisi waktu mulai dari setiap aktivitas.
* `f` adalah array yang berisi waktu selesai dari setiap aktivitas (sudah diurutkan).
* `n` adalah jumlah total aktivitas.
* `A` adalah himpunan aktivitas yang terpilih.
* `j` adalah indeks aktivitas terakhir yang dipilih.

Dengan algoritma ini, kita dapat memilih aktivitas sebanyak mungkin tanpa ada tumpang tindih, yang merupakan solusi optimal dari masalah Activity Selection.

# 📅 Activity Selection Problem: Jadwal Seminar Terbanyak dalam Sehari

## 📌 Deskripsi Permasalahan

Seorang mahasiswa diminta menjadi moderator dalam seminar kampus. Dalam satu hari terdapat banyak seminar dengan waktu mulai dan selesai yang berbeda-beda. Mahasiswa tersebut hanya bisa memoderatori satu seminar dalam satu waktu. Tujuannya adalah memilih sebanyak mungkin seminar yang bisa dimoderatori tanpa bentrok waktu.

### Format Kegiatan
Setiap kegiatan memiliki:
- Waktu mulai
- Waktu selesai

Contoh:
| Seminar | Mulai | Selesai |
|---------|-------|---------|
| A       | 1     | 4       |
| B       | 3     | 5       |
| C       | 0     | 6       |
| D       | 5     | 7       |
| E       | 8     | 9       |
| F       | 5     | 9       |
| G       | 6     | 10      |
| H       | 2     | 14      |

---

## Tujuan

Memilih kombinasi seminar terbanyak yang **tidak tumpang tindih** (non-overlapping) berdasarkan waktu selesai paling awal.

---

## Algoritma yang Digunakan

Activity Selection Problem diselesaikan dengan algoritma **greedy**:
1. Urutkan aktivitas berdasarkan **waktu selesai**.
2. Pilih aktivitas pertama.
3. Selalu pilih aktivitas berikutnya yang waktu mulainya ≥ waktu selesai aktivitas sebelumnya.

---

## Implementasi dalam C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
    string name;
};

bool compare(Activity a, Activity b) {
    return a.finish < b.finish;
}

void activitySelection(vector<Activity>& activities) {
    sort(activities.begin(), activities.end(), compare);

    cout << "Seminar yang bisa dimoderatori:" << endl;

    int lastFinishTime = -1;
    for (auto& act : activities) {
        if (act.start >= lastFinishTime) {
            cout << act.name << " (Mulai: " << act.start << ", Selesai: " << act.finish << ")" << endl;
            lastFinishTime = act.finish;
        }
    }
}

int main() {
    vector<Activity> activities = {
        {1, 4, "A"},
        {3, 5, "B"},
        {0, 6, "C"},
        {5, 7, "D"},
        {8, 9, "E"},
        {5, 9, "F"},
        {6, 10, "G"},
        {2, 14, "H"}
    };

    activitySelection(activities);

    return 0;
}


## Implementasi (Contoh Kode C++)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Activity {
    int start, finish, index;
};

// Fungsi komparasi untuk mengurutkan aktivitas berdasarkan waktu selesai
bool activityCompare(Activity s1, Activity s2) {
    return (s1.finish < s2.finish);
}

// Fungsi untuk mencetak aktivitas yang terpilih
void printMaxActivities(vector<Activity>& arr, int n) {
    // Urutkan aktivitas berdasarkan waktu selesai
    sort(arr.begin(), arr.end(), activityCompare);

    cout << "Aktivitas yang terpilih: ";

    // Pilih aktivitas pertama (selalu aktivitas dengan waktu selesai paling awal)
    int i = 0;
    cout << "A" << arr[i].index << " ";

    // Iterasi melalui aktivitas yang tersisa
    for (int j = 1; j < n; j++) {
        // Jika waktu mulai aktivitas saat ini lebih besar atau sama dengan
        // waktu selesai aktivitas yang terakhir dipilih, maka aktivitas ini kompatibel
        if (arr[j].start >= arr[i].finish) {
            cout << "A" << arr[j].index << " ";
            i = j; // Perbarui aktivitas terakhir yang dipilih
        }
    }
    cout << endl;
}

int main() {
    // Definisi aktivitas
    vector<Activity> arr = {
        {1, 4, 1}, // A1
        {3, 5, 2}, // A2
        {0, 6, 3}, // A3
        {5, 7, 4}, // A4
        {8, 9, 5}, // A5
        {5, 9, 6}  // A6
    };
    int n = arr.size();

    // Panggil fungsi untuk mencetak aktivitas yang terpilih
    printMaxActivities(arr, n);

    return 0;
}

```
**Output:**
```
Seminar yang bisa dimoderatori:
A (Mulai: 1, Selesai: 4)
D (Mulai: 5, Selesai: 7)
E (Mulai: 8, Selesai: 9)

Aktivitas yang terpilih: A1 A4 A5
```


## Analisis Kompleksitas

### Kompleksitas Waktu:
* Pengurutan aktivitas berdasarkan waktu selesai: *O(n \log n)*.
    * Langkah pertama dalam algoritma ini adalah mengurutkan aktivitas berdasarkan waktu selesai.
    * Menggunakan algoritma pengurutan yang efisien seperti Quick Sort atau Merge Sort membutuhkan waktu *O(n \log n)* untuk *n* aktivitas.
* Pemilihan aktivitas: *O(n)*.
* **Total kompleksitas waktu:** *O(n \log n)*.

### Kompleksitas Ruang:
* Menyimpan aktivitas: *O(n)*.
    * Algoritma memerlukan ruang *O(n)* untuk menyimpan *n* aktivitas dalam array atau vektor.
* Tidak memerlukan ruang tambahan yang signifikan selain untuk menyimpan input dan output.
* Selain itu, kita memerlukan ruang tambahan untuk menyimpan hasil (subset aktivitas yang dipilih), yang dalam kasus terburuk juga *O(n)*.
* Operasi pengurutan mungkin memerlukan ruang tambahan *O(\log n)* atau *O(n)*, tergantung pada implementasi algoritma pengurutan yang digunakan.

## Aplikasi Dunia Nyata dan Karakteristik

### Aplikasi Dunia Nyata:
* **Penjadwalan & Fasilitas:** Jadwal ruang kelas, *meeting*, lab, olahraga.
* **Sistem Operasi:** Jadwal proses CPU, alokasi memori.
* **Logistik:** Jadwal pengiriman & rute kendaraan.
* **Telekomunikasi:** Alokasi *bandwidth* & jadwal transmisi data.

### Kekuatan Algoritma Greedy (Activity Selection):
* Sederhana dan mudah diimplementasikan.
* Efisien untuk *dataset* besar.
* Memberikan solusi optimal dalam kasus tanpa batasan kompleks.
  
### Keterbatasan:
* Membutuhkan proses pengurutan awal.
* Tidak cocok untuk masalah dengan banyak batasan tambahan (misalnya, prioritas, jarak, atau biaya).

## Kesimpulan

Activity Selection Problem adalah masalah optimasi untuk memilih aktivitas sebanyak mungkin tanpa tumpang tindih. Masalah ini diselesaikan dengan algoritma *greedy* yang mengurutkan aktivitas berdasarkan waktu selesai, menghasilkan solusi optimal dengan efisiensi *O(n \log n)*. Cocok untuk aplikasi penjadwalan, namun untuk kasus kompleks yang melibatkan banyak batasan tambahan, dibutuhkan metode lain seperti pemrograman dinamis atau metaheuristik.

---
