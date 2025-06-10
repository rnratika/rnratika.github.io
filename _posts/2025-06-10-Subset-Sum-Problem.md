---
layout: post
title: "Subset Sum Problem"
date: 2025-06-10 10:00:00 +0800
categories: cpp backtracking
tags: [c++, backtracking]
---

## Apa itu Subset Sum Problem?
Subset Sum Problem adalah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target. Subset Sum Problem (SSP) termasuk dalam decision problem, yaitu jenis masalah yang hanya membutuhkan jawaban “ya” atau “tidak”. Inti dari masalah ini adalah mencari apakah mungkin memilih sejumlah angka dari sekumpulan bilangan bulat sehingga totalnya pas sama dengan angka target.

## Prinsip Kerja
Ada beberapa cara untuk menyelesaikan masalah ini:

### A. Brute Force (Eksponensial)
1. Periksa semua kemungkinan subset (2ⁿ subset).
2. Jumlahkan setiap subset.
3. Cek apakah ada yang sama dengan target.
4. Waktu: O(2ⁿ)

### B. Dynamic Programming (Efisien)
1. Gunakan matriks dp[n+1][sum+1].
2. dp[i][j] = true jika subset dari i elemen bisa membentuk jumlah j.
3. Berdasarkan dua pilihan:
- Tidak memasukkan elemen i: dp[i-1][j]
- Memasukkan elemen i: dp[i-1][j - arr[i-1]]
4. Waktu: O(n × sum)

## Contoh Permasalahan
Array: [3, 34, 4, 12, 5, 2]
Target: 9

Penyelesaian:
Apakah ada subset yang jumlahnya 9?

Periksa kombinasi:
- {3, 4, 2} = 9 ✅
- {4, 5} = 9 ✅

Jadi jawabannya adalah YA, subset yang jumlahnya 9 memang ada.

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
using namespace std;

bool isSubsetSum(int arr[], int n, int sum) {
    bool dp[n+1][sum+1];

    // Inisialisasi: sum = 0 bisa selalu dicapai
    for (int i = 0; i <= n; i++) dp[i][0] = true;
    // Tidak bisa membentuk sum > 0 dari 0 elemen
    for (int j = 1; j <= sum; j++) dp[0][j] = false;

    // Pengisian tabel DP
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            if (arr[i-1] > j)
                dp[i][j] = dp[i-1][j];  // elemen terlalu besar, tidak digunakan
            else
                dp[i][j] = dp[i-1][j] || dp[i-1][j - arr[i-1]];
        }
    }

    return dp[n][sum];
}

int main() {
    int arr[] = {3, 34, 4, 12, 5, 2};
    int sum = 9;
    int n = sizeof(arr)/sizeof(arr[0]);

    if (isSubsetSum(arr, n, sum))
        cout << "YA, subset dengan jumlah 9 ditemukan." << endl;
    else
        cout << "TIDAK, tidak ada subset dengan jumlah 9." << endl;

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Kriptografi: Digunakan dalam sistem kriptografi berbasis ransel, di mana kesulitan menyelesaikan Permasalahan Subset Sum menjadi dasar keamanan kunci publik.
2. Alokasi Sumber Daya: Membantu memilih subset proyek atau item agar sesuai dengan anggaran atau target tertentu.
3. Genetika dan Bioinformatika: Digunakan untuk menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
4. Keuangan dan Investasi: Membantu menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
5. Perancangan Permainan dan Teka-Teki: Muncul dalam permainan atau teka-teki yang melibatkan pencarian kombinasi angka sesuai skor target.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Sederhana secara konsep.
2. Bisa diselesaikan dengan berbagai pendekatan (rekursif, DP).
3. Relevan dalam berbagai aplikasi praktis dan algoritma dasar AI/optimasi.

### Kekurangan:
1. Termasuk NP-Complete: tidak ada solusi efisien untuk skala besar.
2. Brute force tidak efektif untuk array > 20 elemen.
3. Konsumsi memori besar untuk DP jika nilai target besar.

## Kesimpulan
Subset Sum Problem (SSP) adalah masalah dalam ilmu komputer yang bertujuan untuk menentukan apakah terdapat subset dari sekumpulan bilangan bulat yang jumlahnya sama dengan nilai target tertentu. Masalah ini tergolong dalam kategori NP-Complete dan memiliki berbagai variasi, seperti bounded, unbounded, exact k elements, partition, multi-target, hingga approximate subset sum, yang masing- masing memiliki aplikasi dan batasan berbeda.

Untuk menyelesaikan SSP, digunakan pendekatan rekursif yang sederhana namun kurang efisien, serta dynamic programming yang lebih optimal baik dari segi waktu maupun ruang. Subset Sum memiliki aplikasi nyata dalam bidang kriptografi, keuangan, pengelolaan sumber daya, hingga kecerdasan buatan, menjadikannya masalah penting yang tidak hanya teoritis, tetapi juga relevan dalam dunia praktis.