---
layout: post
title: "Rat in a Maze"
date: 2025-06-10 10:00:00 +0800
categories: cpp backtracking
tags: [c++, backtracking]
---

## Apa itu Rat in a Maze?
Rat in a Maze adalah salah satu masalah klasik dalam pemrograman menggunakan teknik backtracking. Dalam masalah ini, seekor tikus berada di sel awal dari sebuah labirin 2D (biasanya di pojok kiri atas) dan harus mencapai sel tujuan (biasanya pojok kanan bawah), hanya dengan bergerak ke arah tertentu (umumnya ke bawah dan ke kanan, atau ke semua 4 arah). Tujuannya adalah mencari semua jalur yang memungkinkan atau satu jalur dari awal ke akhir, tanpa melewati dinding (sel yang tidak bisa dilalui).

## Prinsip Kerja
Masalah ini diselesaikan menggunakan backtracking, yaitu:
1. Mulai dari sel awal.
2. Periksa apakah langkah saat ini valid (tidak keluar dari batas, tidak menabrak dinding).
3. Tandai sel sebagai bagian dari solusi.
4. Rekursif ke arah bawah, kanan, atas, kiri (jika diperbolehkan).
5. Jika arah tersebut gagal, backtrack (kembali dan hapus tanda sel).
6. Ulangi sampai solusi ditemukan atau semua kemungkinan telah dicoba.

## Contoh Permasalahan
Maze 4x4
Tujuan: Dari (0,0) ke (3,3).
```
1 0 0 0
1 1 0 1
0 1 0 0
1 1 1 1
```
1: jalur yang bisa dilewati
0: dinding / tidak bisa dilewati

Solusi:
```
1 0 0 0
1 1 0 0
0 1 0 0
0 1 1 1
```

Langkah-langkah:
- Mulai dari (0,0)
- ke (1,0)
- ke (1,1)
- ke (2,1)
- ke (3,1)
- ke (3,2)
- ke (3,3)

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#define N 4
using namespace std;

bool isSafe(int maze[N][N], int x, int y) {
    return (x >= 0 && x < N && y >= 0 && y < N && maze[x][y] == 1);
}

bool solveMazeUtil(int maze[N][N], int x, int y, int sol[N][N]) {
    if (x == N - 1 && y == N - 1 && maze[x][y] == 1) {
        sol[x][y] = 1;
        return true;
    }

    if (isSafe(maze, x, y)) {
        sol[x][y] = 1;

        if (solveMazeUtil(maze, x + 1, y, sol)) return true;
        if (solveMazeUtil(maze, x, y + 1, sol)) return true;

        sol[x][y] = 0; // backtrack
        return false;
    }

    return false;
}

void solveMaze(int maze[N][N]) {
    int sol[N][N] = { {0} };

    if (!solveMazeUtil(maze, 0, 0, sol)) {
        cout << "No solution found\n";
        return;
    }

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            cout << sol[i][j] << " ";
        cout << "\n";
    }
}

int main() {
    int maze[N][N] = {
        {1, 0, 0, 0},
        {1, 1, 0, 1},
        {0, 1, 0, 0},
        {1, 1, 1, 1}
    };

    solveMaze(maze);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Robot Navigasi: Menemukan jalur dari titik awal ke tujuan dalam ruang terbatas.
2. Game AI: NPC mencari jalur optimal di peta.
3. Sistem Rute / Pathfinding: Seperti GPS atau logistik untuk menemukan jalur tercepat di grid.
4. Maze Solving Robots: Digunakan dalam kompetisi robotik (micromouse).
5. Puzzle dan permainan edukatif.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Mudah dipahami dengan representasi visual.
2. Latihan bagus untuk memahami backtracking.
3. Bisa disesuaikan untuk solusi tunggal atau semua solusi.
4. Bisa dikembangkan menjadi algoritma lain seperti A*, DFS, BFS.

### Kekurangan:
1. Kurang efisien untuk labirin besar karena rekursi berulang.
2. Tidak optimal untuk pencarian jalur terpendek.
3. Tidak memperhatikan bobot/jarak antar sel (berat graf).

## Kesimpulan
Rat in a Maze adalah masalah yang mengajarkan teknik rekursif dan backtracking untuk menyelesaikan persoalan jalur dalam grid. Meskipun sederhana, prinsip di baliknya dapat diaplikasikan dalam berbagai aspek kehidupan nyata, dari robotika hingga sistem navigasi.

Meskipun efisien untuk labirin kecil, untuk skala besar atau jalur optimal, algoritma lain seperti A*, BFS, atau Dijkstra lebih tepat. Namun, Rat in a Maze tetap menjadi fondasi penting dalam pembelajaran algoritma eksplorasi jalur.