---
layout: post
title: "Fractional Knapsack"
date: 2025-06-10 10:00:00 +0800
categories: greedy cpp
tags: [c++, greedy]
---

## Apa itu Fractional Knapsack?
Fractional Knapsack Problem adalah salah satu jenis masalah Greedy Algorithm di mana kita dapat mengambil sebagian (fraksi) dari suatu item untuk dimasukkan ke dalam tas (knapsack), dengan tujuan untuk memaksimalkan total nilai (value) dari item yang dibawa tanpa melebihi kapasitas tas. Berbeda dengan 0/1 Knapsack, pada fractional knapsack kita boleh mengambil sebagian dari item, misalnya setengah atau seperempat dari item tersebut.

## Prinsip Kerja
Prinsip greedy digunakan berdasarkan nilai per unit berat (value/weight). Langkah-langkahnya:

1. Hitung rasio value/weight untuk setiap item.
2. Urutkan item berdasarkan rasio tersebut secara menurun (descending).
3. Ambil item dari yang rasio-nya paling besar: Jika tas masih muat seluruh item, ambil semua. Jika tidak muat, ambil sebagian hingga tas penuh.
4. Proses selesai saat kapasitas tas habis.

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

1. Hitung rasio nilai/berat:
- Emas: 60 / 10 = 6
- Permata: 100 / 20 = 55
- Berlian: 120 / 30 = 4
2. Urutkan: Emas → Permata → Berlian
3. Ambil:
- Emas 10 kg → 60 koin → sisa 40 kg
- Permata 20 kg → 100 koin → sisa 20 kg
- Berlian 20 kg dari 30 kg → (20/30)×120 = 80 koin

Hasil :
Total nilai = 60 + 100 + 80 = 240 koin
Total berat = 50 kg

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Item {
    int weight;
    int value;
};

bool compare(Item a, Item b) {
    double r1 = (double)a.value / a.weight;
    double r2 = (double)b.value / b.weight;
    return r1 > r2;
}

double fractionalKnapsack(int capacity, vector<Item> items) {
    sort(items.begin(), items.end(), compare);

    double totalValue = 0.0;

    for (Item& item : items) {
        if (capacity >= item.weight) {
            capacity -= item.weight;
            totalValue += item.value;
        } else {
            totalValue += item.value * ((double)capacity / item.weight);
            break;  // tas sudah penuh
        }
    }

    return totalValue;
}

int main() {
    vector<Item> items = {{10, 60}, {20, 100}, {30, 120}};
    int capacity = 50;

    double maxValue = fractionalKnapsack(capacity, items);
    cout << "Nilai maksimum yang bisa dibawa: " << maxValue << endl;

    return 0;
}
{% endraw %}
```
## Implementasi Dalam Kehidupan
1. Logistik dan Transportasi: Memilih barang-barang paling bernilai untuk dikirim jika kapasitas pengiriman terbatas.
2. Cloud Storage: Menyimpan data penting lebih dulu saat ruang penyimpanan terbatas.
3. Portofolio Investasi: Mengalokasikan dana ke saham/obligasi yang punya rasio return terbaik, meskipun tidak bisa membeli satu lot penuh.
4. Pertolongan Bencana: Mengirimkan bantuan yang memiliki rasio manfaat/berat tertinggi terlebih dahulu.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Lebih fleksibel: bisa mengambil sebagian item.
2. Solusi optimal dijamin dengan pendekatan greedy.
3. Lebih cepat dibandingkan 0/1 knapsack karena tidak memerlukan pemrograman dinamis.
4. Kompleksitas waktu: O(n log n) karena proses pengurutan.

### Kekurangan:
1. Tidak bisa digunakan untuk masalah knapsack yang item-nya tidak bisa dibagi (misalnya: laptop, TV, hewan ternak).
2. Tidak cocok untuk kasus dengan nilai diskrit atau logika boolean (ambil semua atau tidak sama sekali).
3. Kadang tidak realistis jika sebagian item tidak bisa dipisahkan dalam dunia nyata.

## Kesimpulan
Fractional Knapsack Problem adalah penyelesaian optimal dari masalah alokasi terbatas yang memungkinkan pembagian item. Pendekatan greedy yang berdasarkan rasio value/weight sangat efisien dan praktis untuk berbagai aplikasi nyata. Namun, model ini hanya cocok ketika pembagian sebagian item memang masuk akal.



