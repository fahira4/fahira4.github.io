---
title: SUBSET SUM PROBLEM
date: 2025-05-20
categories: [DESAIN ANALISIS ALGORITMA, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking]     # TAG names should always be lowercase
---

# Lohaaa !

![Desktop View](https://i.ytimg.com/vi/0FAUzs23RX4/maxresdefault.jpg){: width="500"}
_---_

Dalam kehidupan sehari-hari, kita sering menghadapi masalah di mana kita ingin tahu apakah mungkin untuk mencapai suatu nilai tertentu dengan menjumlahkan sejumlah nilai dari suatu kumpulan. Misalnya, dalam konteks keuangan, kita bisa bertanya: *apakah mungkin mendapatkan total pengeluaran sebesar Rp 100.000 dengan memilih beberapa item dari daftar belanja tertentu?*

Masalah semacam ini dikenal dengan nama **Subset Sum Problem**, sebuah permasalahan mendasar yang sering menjadi pintu gerbang untuk memahami berbagai algoritma pencarian dan optimasi, termasuk yang digunakan dalam **knapsack problem**, **cryptography**, dan **analisis kombinatorik**.

Subset Sum merupakan bagian dari kelas masalah **NP-complete**, artinya meskipun mudah untuk memverifikasi solusi yang benar, tidak ada algoritma efisien yang diketahui untuk menyelesaikan semua kasusnya dengan cepat. Namun, dalam banyak situasi praktis, kita bisa menyelesaikannya menggunakan **algoritma rekursif**, **backtracking**, atau **pemrograman dinamis**.

---


***

### Definisi Formal

Secara formal, masalah ini dapat didefinisikan sebagai berikut:

Diberikan sebuah himpunan bilangan bulat `arr` dan nilai `target_sum`, tentukan apakah ada subset dari `arr` yang jumlah elemennya sama dengan `target_sum`.

***

### Variasi Masalah Subset Sum

*Subset Sum Problem* punya beberapa variasi, masing-masing dengan batasan dan aplikasi yang berbeda:

| Variasi | Deskripsi | Contoh Kasus |
| :--- | :--- | :--- |
| **Bounded Subset Sum Problem** | Setiap elemen dalam himpunan hanya dapat digunakan sekali. Ini cocok untuk masalah di mana sumber daya bersifat unik atau terbatas. | **Set**: `{3, 34, 4, 12, 5, 2}`, **Target**: 9. **Solusi**: Ya, subset `{4, 5}`. |
| **Unbounded Subset Sum Problem** | Setiap elemen boleh digunakan berulang kali untuk mencapai target. Ini berarti sebuah angka bisa dipakai beberapa kali selama totalnya tidak melebihi target. | **Set**: `{1, 3, 4}`, **Target**: 6. **Solusi**: Ya, beberapa kemungkinannya adalah `{3, 3}` atau `{1, 1, 4}`. |
| **Partition Problem** | Membagi sebuah himpunan bilangan bulat menjadi dua subset yang jumlah totalnya sama. Ini setara dengan mencari subset yang jumlahnya sama dengan setengah dari total seluruh elemen. Masalah ini penting dalam manajemen sumber daya seperti pembagian beban kerja. | **Set**: `{1, 5, 11, 5}`. Totalnya 22, targetnya 11. **Solusi**: Ya, `{11}` dan `{1, 5, 5}`. |
| **Exact k Elements Subset Sum** | Mencari subset yang jumlahnya sama dengan target dan terdiri dari tepat *k* elemen. Variasi ini sering digunakan untuk memilih tim dengan jumlah anggota dan total skor tertentu. | **Set**: `{1, 2, 3, 4, 5}`, **Target**: 9, **k**: 2. **Solusi**: Ya, subset `{4, 5}`. Subset `{2, 3, 4}` juga berjumlah 9, tapi tidak valid karena terdiri dari 3 elemen. |
| **Multi-target Subset Sum** | Mencari subset yang memenuhi lebih dari satu kriteria secara bersamaan, misalnya jumlah total dan batas berat. Sering muncul dalam kasus e-commerce dengan batasan ongkos kirim atau logistik. | **Set**: Barang A (harga 40, berat 1kg), B (harga 60, berat 1.5kg), C (harga 30, berat 0.5kg). **Target**: harga *\le 100* dan berat *\le 2* kg. **Solusi Valid**: A+C (harga 70, berat 1.5kg). **Solusi Tidak Valid**: A+B (harga 100, berat 2.5kg, melebihi batas berat). |
| **Approximate Subset Sum** | Ketika tidak ada subset yang jumlahnya tepat sama dengan target, maka dicari subset terbaik yang jumlahnya mendekati target (biasanya tidak boleh melebihi). | **Set**: `{2, 5, 10, 14}`, **Target**: 16. **Solusi**: Tidak ada subset yang tepat 16. Solusi terbaik yang mendekati adalah `{5, 10}` dengan jumlah 15. |

***

### Pendekatan Penyelesaian

Ada beberapa pendekatan untuk menyelesaikan SSP, mulai dari yang sederhana hingga yang lebih optimal.

#### 1. Pendekatan Rekursif (Recursive Approach)

Pendekatan ini secara eksplisit memeriksa semua kemungkinan subset. Untuk setiap elemen, ada dua pilihan: menyertakannya dalam subset atau mengabaikannya.
* **Logika**:
    * Sertakan elemen saat ini: `cariSubset(arr, n-1, target - arr[n-1])`
    * Abaikan elemen saat ini: `cariSubset(arr, n-1, target)`
* **Kasus Basis**:
    * Jika `target == 0`, maka `True` (subset ditemukan).
    * Jika `n == 0` dan `target != 0`, maka `False` (tidak ada elemen tersisa).
* **Kompleksitas Waktu**: *O(2^n)*. Sangat tidak efisien untuk himpunan data yang besar.

#### 2. Pendekatan Pemrograman Dinamis (Dynamic Programming)

Pendekatan ini lebih efisien karena menyimpan hasil dari submasalah yang tumpang tindih untuk menghindari perhitungan berulang.

**A. Memoization (Top-Down)**
Ini adalah kombinasi dari rekursi dengan penyimpanan hasil (caching). Sebuah tabel `dp[n][sum]` digunakan untuk menyimpan hasil submasalah yang sudah diselesaikan.
* **Kompleksitas Waktu**: *O(n \times sum)*
* **Kompleksitas Ruang**: *O(n \times sum)*

**B. Tabulation (Bottom-Up)**
Pendekatan ini bersifat iteratif, membangun solusi dari kasus terkecil.
* **Logika**: Sebuah tabel boolean `dp[n+1][sum+1]` dibuat. `dp[i][j]` akan bernilai `True` jika subset dari `arr[0...i-1]` bisa menghasilkan jumlah `j`.
* **Inisialisasi**:
    * `dp[i][0] = True` untuk semua `i` (jumlah 0 selalu bisa dicapai dengan subset kosong).
    * `dp[0][j] = False` untuk `j > 0` (tidak mungkin dapat jumlah positif tanpa elemen).
* Hasil akhir adalah nilai dari `dp[n][sum]`.

**C. Optimasi Ruang pada Pemrograman Dinamis**
Dalam pendekatan tabulasi, untuk menghitung baris saat ini (`i`), kita hanya butuh informasi dari baris sebelumnya (`i-1`). Oleh karena itu, kita bisa mengoptimalkan memori dari *O(n \times sum)* menjadi *O(sum)* dengan hanya menggunakan dua array 1D.
* **Logika**: Gunakan array `prev` (untuk status sebelumnya) dan `curr` (untuk status saat ini). Aturan pengisiannya: `curr[j] = prev[j] OR prev[j - arr[i]]`.
* **Kompleksitas Waktu**: *O(n \times sum)*
* **Kompleksitas Ruang**: *O(sum)*

***

## Contoh Permasalahan

### Deskripsi
Diberikan:
- Sebuah himpunan `S` yang berisi `n` bilangan bulat.
- Sebuah target nilai `T`.

Tujuan:
- Menentukan apakah ada subset dari `S` yang elemen-elemennya jika dijumlahkan akan menghasilkan `T`.

---

## Solusi: Backtracking (Recursive)

Pendekatan:
- Untuk setiap elemen, kita punya dua pilihan: **ikut sertakan** atau **abaikan**.
- Kita menjelajahi seluruh kombinasi kemungkinan hingga mencapai subset yang jumlahnya sama dengan target, atau tidak ada yang sesuai.

---

## Implementasi C++

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSubsetSum(vector<int>& nums, int n, int target) {
    // Basis: jika target 0, maka selalu bisa
    if (target == 0) return true;
    // Basis: jika tidak ada item lagi dan target belum 0
    if (n == 0) return false;

    // Jika elemen terakhir lebih besar dari target, tidak bisa diambil
    if (nums[n - 1] > target)
        return isSubsetSum(nums, n - 1, target);

    // Periksa dua kemungkinan:
    // 1. Elemen terakhir diabaikan
    // 2. Elemen terakhir dimasukkan
    return isSubsetSum(nums, n - 1, target) ||
           isSubsetSum(nums, n - 1, target - nums[n - 1]);
}

int main() {
    vector<int> set = {3, 34, 4, 12, 5, 2};
    int target = 9;
    int n = set.size();

    if (isSubsetSum(set, n, target))
        cout << "Terdapat subset yang berjumlah " << target << endl;
    else
        cout << "Tidak ditemukan subset dengan jumlah " << target << endl;

    return 0;
}

```

***

### Aplikasi di Dunia Nyata

*Subset Sum Problem* bukan hanya teori, tapi punya aplikasi praktis yang luas:
* **Kriptografi**: Menjadi dasar keamanan beberapa sistem kriptografi kunci publik berbasis ransel (*knapsack cryptosystem*).
* **Alokasi Sumber Daya**: Membantu memilih proyek atau item agar sesuai dengan anggaran tertentu.
* **Keuangan dan Investasi**: Digunakan untuk menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
* **Genetika dan Bioinformatika**: Menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
* **Perancangan Permainan dan Teka-Teki**: Muncul dalam permainan yang melibatkan pencarian kombinasi angka untuk mencapai skor target.

***

### Kesimpulan

*Subset Sum Problem* adalah masalah fundamental dalam ilmu komputer untuk menentukan keberadaan subset dengan jumlah tertentu dari sebuah himpunan. Sebagai masalah *NP-Complete*, ia menantang untuk dipecahkan secara efisien. Masalah ini punya banyak variasi seperti *bounded, unbounded, partition,* dan lainnya, yang masing-masing punya kegunaan spesifik. Meskipun pendekatan rekursif sederhana, ia tidak efisien, sehingga pendekatan *dynamic programming* menjadi solusi yang lebih optimal dari segi waktu dan ruang. Relevansinya terbukti melalui aplikasinya di berbagai bidang penting seperti kriptografi, keuangan, dan manajemen sumber daya.

---

![Desktop View](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fnklexsqp82ylqyzlljm5.jpg){: width="300"}
_---_
