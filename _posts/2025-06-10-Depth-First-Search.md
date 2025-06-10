---
layout: post
title: "Depth-First Search (DFS)"
date: 2025-06-10 10:00:00 +0800
categories: cpp backtracking
tags: [c++, backtracking]
---

## Apa itu Depth-First Search (DFS)?
DFS (Depth-First Search) adalah algoritma pencarian atau traversing dalam struktur data graf atau pohon yang menjelajahi sedalam mungkin pada setiap cabang sebelum kembali (backtrack).DFS menggunakan rekursi atau struktur data stack (tumpukan) untuk mengingat node yang akan dieksplorasi selanjutnya. Cocok untuk masalah yang membutuhkan eksplorasi hingga ke bagian terdalam terlebih dahulu.

## Prinsip Kerja
DFS bekerja dengan prinsip backtracking:
1. Mulai dari node awal (root/source).
2. Tandai node sebagai dikunjungi.
3. Kunjungi tetangga pertama yang belum dikunjungi.
4. Ulangi langkah ini hingga tidak ada tetangga yang belum dikunjungi.
5. Backtrack ke node sebelumnya untuk melanjutkan ke tetangga berikutnya.
6. Ulangi hingga semua node telah dikunjungi.

DFS bisa diimplementasikan dengan:
- Rekursif
- Non-rekursif menggunakan Stack

## Contoh Permasalahan
Misal, graf tidak berbobot dan tidak berarah:
```
Graph:
A - B
|   |
C - D
```
Representasi :
```
A: B, C
B: A, D
C: A, D
D: B, C
```
DFS dari A:
Mulai dari A → kunjungi B → kunjungi D → kunjungi C (jika belum)
Hasil urutan kunjungan (salah satu kemungkinan): A B D C

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
using namespace std;

void dfs(int node, vector<vector<int>> &adj, vector<bool> &visited) {
    cout << node << " ";
    visited[node] = true;

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adj, visited);
        }
    }
}

int main() {
    int n = 5; // jumlah node (0 to 4)
    vector<vector<int>> adj(n);

    // menambahkan edge (graph tidak berarah)
    adj[0] = {1, 2};    // A
    adj[1] = {0, 3};    // B
    adj[2] = {0, 3};    // C
    adj[3] = {1, 2};    // D
    adj[4] = {};        // E (tidak terhubung)

    vector<bool> visited(n, false);
    dfs(0, adj, visited); // mulai dari node 0 (A)
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Pemetaan dan navigasi (menelusuri peta atau labirin)
2. Penyelesaian teka-teki seperti Sudoku dan Maze
3. Pendeteksian siklus dalam graf (misal: deteksi deadlock)
4. Penjadwalan tugas (topological sorting)
5. Web crawling (mengindeks halaman web secara mendalam)
6. Mencari komponen terhubung di jaringan sosial

## Kelebihan dan Kekurangan
### Kelebihan:
1. Lebih hemat memori dibanding BFS (hanya menyimpan satu jalur dan node)
2. Efektif untuk menemukan solusi yang dalam atau ketika solusi berada dekat dengan leaf
3. Mudah diimplementasikan dengan rekursi

### Kekurangan:
1. Bisa terjebak dalam loop jika graf memiliki siklus dan tidak dicek visited
2. Tidak menjamin menemukan solusi terpendek
3. Bisa menjadi sangat dalam (stack overflow) jika graf sangat besar dan dalam

## Kesimpulan
Depth-First Search (DFS) adalah algoritma penelusuran yang bekerja dengan menjelajahi struktur data seperti graf atau pohon secara mendalam sebelum kembali (backtrack) untuk menelusuri jalur lainnya. DFS efektif dalam mengeksplorasi semua kemungkinan secara mendalam dan cocok digunakan untuk menyelesaikan masalah yang melibatkan pencarian hingga ke bagian terdalam, seperti pemecahan teka-teki, pencarian jalur di labirin, atau deteksi siklus dalam graf.
Meskipun DFS memiliki keunggulan dalam efisiensi memori dan implementasi yang sederhana (terutama secara rekursif), kelemahannya terletak pada ketidakmampuannya menjamin solusi terpendek serta potensi terjebak dalam siklus jika tidak menggunakan penanda kunjungan. Secara keseluruhan, DFS merupakan algoritma dasar yang sangat berguna dalam pemrograman dan ilmu komputer, terutama ketika eksplorasi mendalam lebih diutamakan daripada pencarian optimal.



