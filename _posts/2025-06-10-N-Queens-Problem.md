---
layout: post
title: "N-Queens Problem"
date: 2025-06-10 10:00:00 +0800
categories: cpp backtracking
tags: [c++, backtracking]
---

## Apa itu N-Queens Problem?
N-Queens Problem adalah salah satu permasalahan klasik dalam bidang algoritma dan kecerdasan buatan. Tujuannya adalah menempatkan N buah ratu (queen) di atas papan catur berukuran N × N sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang. Ratu dalam catur bisa bergerak secara horizontal, vertikal, dan diagonal, sehingga tidak boleh ada dua ratu dalam baris, kolom, atau diagonal yang sama.

## Prinsip Kerja
Masalah ini biasanya diselesaikan menggunakan pendekatan Backtracking, yaitu teknik eksplorasi solusi dengan mencoba semua kemungkinan, dan kembali ke kondisi sebelumnya jika menemui jalan buntu.
Langkah-langkahnya:
1. Tempatkan ratu satu per satu di setiap baris.
2. Cek apakah posisi aman (tidak ada konflik kolom dan diagonal).
3. Jika aman, lanjut ke baris berikutnya.
4. Jika tidak, backtrack dan coba posisi lain

## Contoh Permasalahan
Papan: 4×4

Solusi:
Letakkan satu ratu di setiap baris sehingga tidak saling menyerang. Salah satu solusi:

```
. Q . .
. . . Q
Q . . .
. . Q .
```

Representasi koordinat posisi ratu:
(0,1), (1,3), (2,0), (3,2)

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(vector<int> &board, int row, int col, int n) {
    for (int i = 0; i < row; i++) {
        int qCol = board[i];
        if (qCol == col || abs(qCol - col) == abs(i - row))
            return false;
    }
    return true;
}

void solveNQueens(vector<int> &board, int row, int n) {
    if (row == n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                cout << (board[i] == j ? "Q " : ". ");
            cout << endl;
        }
        cout << endl;
        return;
    }

    for (int col = 0; col < n; col++) {
        if (isSafe(board, row, col, n)) {
            board[row] = col;
            solveNQueens(board, row + 1, n);
        }
    }
}

int main() {
    int n = 4;
    vector<int> board(n, -1);
    solveNQueens(board, 0, n);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
Walau berakar dari permainan catur, N-Queens digunakan dalam berbagai konteks:
1. Penjadwalan: Penempatan tugas tanpa konflik.
2. Penempatan frekuensi radio: Menghindari interferensi antar frekuensi.
3. Desain sirkuit: Peletakan komponen agar tidak saling mengganggu.
4. AI dan constraint satisfaction problem (CSP): Studi dan pengembangan algoritma.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Melatih pemahaman Backtracking dan rekursi.
2. Cocok sebagai benchmark algoritma AI dan CSP.
3. Dapat dikembangkan ke variasi masalah kompleks.

### Kekurangan:
1. Eksponensial: Kompleksitasnya O(N!), sehingga lambat untuk N besar.
2. Tidak cocok untuk sistem real-time jika tidak dioptimalkan.
3. Solusi brute-force cepat menjadi tidak efisien.

## Kesimpulan
N-Queens Problem adalah permasalahan kombinatorik klasik yang merepresentasikan konflik penempatan objek dalam ruang terbatas. Dengan pendekatan backtracking, kita bisa menyusun solusi optimal secara efisien. Meski sederhana, masalah ini memiliki banyak penerapan penting dan membantu memahami teknik algoritma penting seperti rekursi, backtracking, dan pencarian solusi dalam constraint problem.



