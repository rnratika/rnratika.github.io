---
layout: post
title: "Kahn’s Algorithm"
date: 2025-06-10 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Kahn’s Algorithm?
Kahn’s Algorithm adalah algoritma untuk melakukan Topological Sorting pada Directed Acyclic Graph (DAG). Topological sorting adalah urutan linear dari semua simpul (node) di graf sedemikian rupa sehingga untuk setiap edge (u → v), simpul u muncul sebelum v dalam urutan.

Kahn’s Algorithm menggunakan pendekatan Breadth-First Search (BFS) dan sangat berguna untuk menyelesaikan masalah penjadwalan, kompilasi, dan dependency resolution.

## Prinsip Kerja
Prinsip utama dari Kahn’s Algorithm adalah:
1. Hitung in-degree (jumlah edge masuk) untuk setiap node.
2. Masukkan semua node dengan in-degree 0 ke dalam antrian.
3. Selama antrian tidak kosong:
- Ambil node dari antrian, masukkan ke hasil topologis.
- Kurangi in-degree semua tetangganya.
- Jika ada tetangga yang in-degree-nya menjadi 0, masukkan ke antrian.
4. Jika jumlah node yang diproses < total node, berarti ada siklus → Topological sort tidak mungkin.

## Contoh Permasalahan
Misal kita punya graf dependensi seperti ini:
```
0 → 1
0 → 2
1 → 3
2 → 3
```
Artinya:
- File 0 harus dikompilasi sebelum 1 dan 2
- File 1 dan 2 harus dikompilasi sebelum 3

Langkah-langkah Kahn’s Algorithm:
1. In-degree awal:
- 0: 0
- 1: 1 (dari 0)
- 2: 1 (dari 0)
- 3: 2 (dari 1 dan 2)
2. Queue awal: [0]
3. Proses:
- Ambil 0 → hasil: [0], kurangi in-degree 1 dan 2 → jadi 0 → Queue: [1, 2]
- Ambil 1 → hasil: [0,1], kurangi in-degree 3 → jadi 1
- Ambil 2 → hasil: [0,1,2], kurangi in-degree 3 → jadi 0 → Queue: [3]
- Ambil 3 → hasil: [0,1,2,3]
Topological Order: [0,1,2,3] (atau [0,2,1,3])

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

void kahnAlgorithm(int V, vector<vector<int>> &adj) {
    vector<int> in_degree(V, 0);

    // Hitung in-degree
    for (int u = 0; u < V; u++) {
        for (int v : adj[u]) {
            in_degree[v]++;
        }
    }

    // Masukkan semua node dengan in-degree 0 ke queue
    queue<int> q;
    for (int i = 0; i < V; i++) {
        if (in_degree[i] == 0)
            q.push(i);
    }

    vector<int> topo_order;

    while (!q.empty()) {
        int u = q.front();
        q.pop();
        topo_order.push_back(u);

        for (int v : adj[u]) {
            in_degree[v]--;
            if (in_degree[v] == 0)
                q.push(v);
        }
    }

    // Cek siklus
    if (topo_order.size() != V) {
        cout << "Graph memiliki siklus, topological sort tidak mungkin.\n";
    } else {
        cout << "Topological Sort: ";
        for (int node : topo_order)
            cout << node << " ";
        cout << endl;
    }
}

int main() {
    int V = 4;
    vector<vector<int>> adj(V);
    adj[0] = {1, 2};
    adj[1] = {3};
    adj[2] = {3};

    kahnAlgorithm(V, adj);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
Kahn’s Algorithm digunakan di banyak bidang praktis:
1. Dependency resolution (misalnya: npm, pip, makefile)
2. Penjadwalan tugas dengan dependensi (misalnya: proyek konstruksi)
3. Urutan kompilasi file (C/C++ build system)
4. Sistem build seperti Make, Gradle
5. Data pipeline (memastikan urutan eksekusi node DAG)

## Kelebihan dan Kekurangan
### Kelebihan:
1. Mendeteksi siklus dalam graf secara otomatis
2. Lebih efisien dan mudah dipahami (menggunakan BFS)
3. Cocok untuk graf besar dengan banyak dependensi

### Kekurangan:
1. Hanya bisa digunakan pada Directed Acyclic Graph (DAG)
2. Tidak cocok untuk pencarian jalur atau traversal mendalam
3. Bisa menghasilkan lebih dari satu urutan topologis yang valid → tidak deterministik

## Kesimpulan
Kahn’s Algorithm adalah metode efektif untuk melakukan topological sorting pada graf berarah tanpa siklus (DAG) menggunakan pendekatan BFS dan in-degree. Algoritma ini sangat berguna untuk menyusun urutan pekerjaan atau entitas yang saling bergantung, seperti penjadwalan proyek, sistem kompilasi, dan penyelesaian dependensi perangkat lunak. 
Dengan menggunakan antrian dan pelacakan in-degree, algoritma ini mampu memberikan urutan valid dan juga mendeteksi adanya siklus dalam graf. Meski tidak menjamin satu urutan tetap (karena bisa ada banyak solusi), Kahn’s Algorithm tetap menjadi salah satu pendekatan yang efisien dan banyak digunakan dalam berbagai aplikasi sistem dan pemrograman modern.