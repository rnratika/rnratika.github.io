---
layout: post
title: "Activity Selection Problem"
date: 2025-06-10 10:00:00 +0800
categories: greedy cpp
tags: [c++, greedy]
---

## Apa itu Activity Selection Problem?
Activity Selection Problem adalah salah satu bentuk Greedy Algorithm yang bertujuan untuk memilih sebanyak mungkin aktivitas dari sejumlah aktivitas yang diberikan, dengan syarat tidak ada dua aktivitas yang saling tumpang tindih waktunya. Setiap aktivitas memiliki waktu mulai (start) dan waktu selesai (finish). Tujuan dari masalah ini adalah memaksimalkan jumlah aktivitas yang bisa dilakukan, tanpa melakukan dua aktivitas secara bersamaan.

## Prinsip Kerja
Activity Selection Problem bekerja dengan pendekatan greedy, yaitu selalu memilih aktivitas yang selesai paling awal terlebih dahulu.

Langkah-langkah utamanya:

1. Urutkan semua aktivitas berdasarkan waktu selesai (ascending).
2. Pilih aktivitas pertama (karena paling cepat selesai).
3. Untuk setiap aktivitas berikutnya, pilih hanya jika waktu mulai aktivitas tersebut ≥ waktu selesai aktivitas sebelumnya yang dipilih.
4. Ulangi sampai akhir daftar aktivitas.

## Contoh Permasalahan
Bayangkan kamu adalah seorang koordinator acara di sebuah gedung serbaguna. Dalam satu hari, banyak komunitas ingin menyewa gedung tersebut untuk kegiatan mereka. Namun, karena hanya ada satu ruangan, kamu harus memilih jadwal kegiatan yang tidak saling tumpang tindih agar sebanyak mungkin komunitas bisa menggunakan ruangan itu.

Ada enam komunitas yang mengajukan permintaan dengan jadwal sebagai berikut:
- Komunitas A ingin menggunakan ruangan dari pukul 1 sampai 3
- Komunitas B dari pukul 0 sampai 4
- Komunitas C dari pukul 5 sampai 9
- Komunitas D dari pukul 5 sampai 7
- Komunitas E dari pukul 8 sampai 9
- Komunitas F dari pukul 2 sampai 6
Tugas kamu adalah memilih sebanyak mungkin komunitas yang bisa menggunakan ruangan tanpa ada jadwal yang bertabrakan.
### Langkah Penyelesaian

1. Urutkan berdasarkan waktu selesai: A1(3), A2(4), A6(6), A4(7), A3(9), A5(9)
2. Pilih A1 → selesai pukul 3
3. A2 dimulai sebelum A1 selesai → lewati
4. A6 dimulai pukul 2 < 3 → lewati
5. A4 dimulai pukul 5 ≥ 3 → pilih
6. A3 dimulai pukul 5 < 7 → lewati
7. A5 dimulai pukul 8 ≥ 7 → pilih

Aktivitas Terpilih: A1, A4, A5

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
};

bool compare(Activity a, Activity b) {
    return a.finish < b.finish;
}

void selectActivities(vector<Activity>& activities) {
    sort(activities.begin(), activities.end(), compare);

    cout << "Aktivitas yang dipilih:\n";

    int lastFinish = activities[0].finish;
    cout << "(" << activities[0].start << ", " << activities[0].finish << ")\n";

    for (int i = 1; i < activities.size(); i++) {
        if (activities[i].start >= lastFinish) {
            cout << "(" << activities[i].start << ", " << activities[i].finish << ")\n";
            lastFinish = activities[i].finish;
        }
    }
}

int main() {
    vector<Activity> activities = {{1, 3}, {0, 4}, {5, 9}, {5, 7}, {8, 9}, {2, 6}};
    selectActivities(activities);
    return 0;
}
{% endraw %}
```
## Implementasi Dalam Kehidupan
1. Penjadwalan Ruang Rapat: Memilih jadwal rapat yang tidak tumpang tindih untuk ruangan terbatas.
2. Penjadwalan Mesin Produksi: Mengatur urutan kerja mesin dengan waktu penggunaan minimum tanpa konflik.
3. Penyiaran Acara Televisi: Menentukan siaran mana yang akan ditayangkan tanpa tumpang tindih.
4. Reservasi Kamar Hotel/Studio: Menyusun jadwal seefisien mungkin agar bisa menerima lebih banyak klien.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Efisien (kompleksitas waktu O(n log n) setelah sorting)
2. Mudah diimplementasikan
3. Cocok untuk kasus penjadwalan real-time

### Kekurangan:
1. Tidak selalu menghasilkan solusi optimal jika masalah dimodifikasi (misalnya ada bobot/profit di tiap aktivitas).
2. Terbatas pada kasus tanpa konflik (aktivitas saling bebas).

## Kesimpulan
Activity Selection Problem adalah contoh klasik dari algoritma Greedy. Dengan memilih aktivitas berdasarkan waktu selesai paling awal, kita dapat memaksimalkan jumlah aktivitas tanpa konflik waktu. Meski sangat efisien untuk masalah standar, pendekatan ini perlu dimodifikasi atau diganti (misalnya Dynamic Programming) jika terdapat kompleksitas tambahan seperti prioritas atau bobot aktivitas.



