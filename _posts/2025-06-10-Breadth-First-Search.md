---
layout: post
title: "Breadth-First Search (BFS)"
date: 2025-06-10 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Breadth-First Search (BFS)?
Breadth-First Search (BFS) adalah algoritma pencarian dalam struktur data graf atau pohon yang menjelajahi semua simpul pada level saat ini terlebih dahulu sebelum pindah ke level berikutnya. Dalam istilah graf, BFS dimulai dari simpul sumber dan mengunjungi semua tetangganya terlebih dahulu sebelum menjelajahi tetangga dari tetangga tersebut. BFS sangat berguna untuk mencari jalur terpendek dalam graf tak berbobot.

## Prinsip Kerja
1. BFS menggunakan struktur data queue (antrian) untuk menyimpan simpul yang akan dikunjungi.
2. Mulai dari simpul awal (source), masukkan ke dalam queue dan tandai sebagai telah dikunjungi.
3. Selama queue tidak kosong:
- Ambil simpul dari depan queue.
- Kunjungi semua tetangganya yang belum dikunjungi.
- Tambahkan tetangga yang belum dikunjungi tersebut ke dalam queue dan tandai sebagai dikunjungi.
4. Ulangi sampai semua simpul telah dikunjungi atau simpul tujuan ditemukan.

## Contoh Permasalahan
```
A -- B -- E
|    |
C -- D
```
Representasi:
- A: [B, C]
- B: [A, D, E]
- C: [A, D]
- D: [B, C]
- E: [B]

Proses BFS dari A:
- Queue = [A]
- Visit A → queue = [B, C]
- Visit B → queue = [C, D, E]
- Visit C → queue = [D, E]
- Visit D → queue = [E]
- Visit E → selesai

Jalur Terpendek dari A ke E:
- A → B → E

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <list>
#include <queue>
using namespace std;

class Graph {
    int V; // jumlah simpul
    list<int>* adj; // array of adjacency list

public:
    Graph(int V);
    void addEdge(int v, int w);
    void BFS(int s); // traversal dari simpul s
};

Graph::Graph(int V) {
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // tambahkan w ke daftar v
    adj[w].push_back(v); // tambahkan v ke daftar w (jika tidak directed)
}

void Graph::BFS(int s) {
    vector<bool> visited(V, false);
    queue<int> q;

    visited[s] = true;
    q.push(s);

    while (!q.empty()) {
        int node = q.front();
        cout << node << " ";
        q.pop();

        for (auto i : adj[node]) {
            if (!visited[i]) {
                visited[i] = true;
                q.push(i);
            }
        }
    }
}

int main() {
    Graph g(5);
    g.addEdge(0, 1); // A-B
    g.addEdge(0, 2); // A-C
    g.addEdge(1, 3); // B-D
    g.addEdge(2, 3); // C-D
    g.addEdge(1, 4); // B-E

    cout << "BFS traversal dari simpul 0 (A): ";
    g.BFS(0);

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Pencarian Jalur Terpendek: Dalam GPS atau peta, BFS digunakan untuk mencari rute tercepat dalam graf tak berbobot.
2. AI dalam Game: BFS digunakan untuk pathfinding NPC agar menavigasi ruang.
3. Web Crawling: Search engine seperti Google menggunakan BFS untuk menjelajahi halaman web.
4. Jaringan Sosial: Menemukan koneksi terdekat antara dua pengguna di jaringan sosial (LinkedIn, Facebook).
5. Broadcasting dalam Jaringan: Menyebarkan informasi dari satu simpul ke seluruh simpul dalam jaringan.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Menemukan jalur terpendek dalam graf tak berbobot.
2. Mudah diimplementasikan menggunakan queue.
3. Cocok untuk graf yang tidak dalam (shallow).

### Kekurangan:
1. Penggunaan memori besar pada graf besar atau dalam.
2. Kurang efisien untuk mencari node yang sangat dalam.
3. Tidak mempertimbangkan bobot (tidak cocok untuk graf berbobot).

## Kesimpulan
Breadth-First Search (BFS) adalah algoritma penting untuk eksplorasi graf dan pohon, yang bekerja dengan menjelajahi simpul demi simpul berdasarkan level. BFS cocok digunakan untuk mencari jalur terpendek dalam graf tak berbobot dan memiliki banyak aplikasi dalam kehidupan nyata seperti pencarian rute, AI, dan jaringan sosial. Namun, BFS tidak cocok untuk graf berbobot dan membutuhkan memori besar jika banyak simpul dan hubungan. Untuk pencarian dengan bobot, algoritma seperti Dijkstra atau A* lebih cocok.