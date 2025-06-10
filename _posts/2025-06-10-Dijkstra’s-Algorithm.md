---
layout: post
title: "Dijkstra’s Algorithm"
date: 2025-06-10 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Dijkstra’s Algorithm?
Dijkstra’s Algorithm adalah algoritma pencarian jalur terpendek dari satu titik asal (source) ke semua simpul lainnya dalam graf berbobot non-negatif. Algoritma ini dikembangkan oleh Edsger W. Dijkstra pada tahun 1956 dan merupakan salah satu algoritma paling populer untuk perhitungan rute atau jarak terpendek.

## Prinsip Kerja
Prinsip utama dari Kahn’s Algorithm adalah:
1. Inisialisasi jarak ke semua node sebagai ∞ (tak hingga), kecuali jarak ke node awal (source) = 0.
2. Gunakan priority queue (min-heap) atau array untuk memilih node dengan jarak terkecil yang belum dikunjungi.
3. Tandai node tersebut sebagai telah diproses (visited).
4. Perbarui jarak ke semua tetangganya jika ditemukan jalur yang lebih pendek.
5. Ulangi proses sampai semua node telah diproses.

n: Dijkstra tidak cocok untuk graf dengan bobot negatif, karena bisa memberikan hasil yang salah.

## Contoh Permasalahan
Graf Berarah dan Berbobot:
```
    (0)
   /   \
  4     1
 /       \
(1)---2-->(2)
```
Representasi:
0 → 1 = 4
0 → 2 = 1
1 → 2 = 2

Jarak Terpendek dari node 0:
Langkah-langkah:
- Jarak awal: [0, ∞, ∞]
- Ambil node 0: update jarak ke 1 = 4, ke 2 = 1 → [0, 4, 1]
- Ambil node 2: dari 2 tidak ada outgoing edge → tetap
- Ambil node 1: dari 1 ke 2 → 4 + 2 = 6 > 1 (tidak update)
- Hasil akhir: jarak = [0, 4, 1]

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

typedef pair<int, int> pii;

void dijkstra(int start, vector<vector<pii>> &adj, int V) {
    vector<int> dist(V, INT_MAX);
    priority_queue<pii, vector<pii>, greater<pii>> pq;

    dist[start] = 0;
    pq.push({0, start}); // (jarak, node)

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue;

        for (auto [v, weight] : adj[u]) {
            if (dist[v] > dist[u] + weight) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    cout << "Jarak terpendek dari node " << start << ":\n";
    for (int i = 0; i < V; ++i)
        cout << "Node " << i << " : " << dist[i] << endl;
}

int main() {
    int V = 3;
    vector<vector<pii>> adj(V);

    // Graph
    adj[0].push_back({1, 4});
    adj[0].push_back({2, 1});
    adj[1].push_back({2, 2});

    dijkstra(0, adj, V);
    return 0;
}

{% endraw %}
```

## Implementasi Dalam Kehidupan
Dijkstra’s Algorithm banyak digunakan dalam:
1. GPS dan Aplikasi Navigasi (Google Maps, Waze)
2. Routing jaringan (protokol OSPF)
3. Video game (AI pathfinding)
4. Sistem transportasi (penjadwalan jalur kereta/bus)
5. Penyelesaian puzzle (misalnya: pencarian jalur optimal dalam game)

## Kelebihan dan Kekurangan
### Kelebihan:
1. Menjamin jalur terpendek dari satu titik ke semua titik lain.
2. Optimal untuk graf dengan bobot non-negatif.
3. Efisien dengan struktur data seperti priority queue / heap.

### Kekurangan:
1. Tidak dapat menangani graf dengan bobot negatif.
2. Kompleksitas bisa tinggi jika tidak menggunakan heap (O(V²)).
3. Tidak cocok untuk mencari jalur antara dua titik saja pada graf sangat besar (lebih efisien menggunakan A* atau bidirectional search).

## Kesimpulan
Dijkstra’s Algorithm adalah metode yang efisien dan optimal untuk menghitung jalur terpendek dari satu simpul ke semua simpul lainnya dalam graf berbobot non-negatif. Dengan memanfaatkan teknik greedy dan struktur data seperti priority queue, algoritma ini menjadi pilihan utama dalam sistem navigasi, jaringan komputer, dan permainan.
Meskipun tidak dapat menangani graf dengan bobot negatif dan memiliki kompleksitas tinggi pada graf besar tanpa optimisasi, Dijkstra tetap menjadi salah satu algoritma dasar yang sangat berpengaruh dan banyak digunakan dalam berbagai aplikasi dunia nyata yang memerlukan efisiensi dalam pencarian jalur.