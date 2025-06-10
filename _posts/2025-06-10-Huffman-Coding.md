---
layout: post
title: "Huffman Coding"
date: 2025-06-10 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Huffman Coding?
Huffman Coding adalah algoritma pengkodean data lossless (tanpa kehilangan informasi) yang digunakan untuk kompresi data dengan cara mengganti karakter-karakter dalam data dengan kode biner yang panjangnya bervariasi, tergantung pada frekuensi kemunculan karakter tersebut. Algoritma ini ditemukan oleh David A. Huffman pada tahun 1952, ketika ia masih menjadi mahasiswa pascasarjana di MIT. Huffman Coding termasuk dalam kategori algoritma greedy karena pada setiap langkahnya, ia memilih solusi lokal terbaik (yaitu menggabungkan dua simbol dengan frekuensi terkecil).

### Karakteristik Huffman Coding:
- Lossless: Data asli dapat direkonstruksi secara sempurna dari data terkompresi.
- Variable-length encoding: Karakter yang sering muncul diberi kode yang lebih pendek, sedangkan karakter yang jarang muncul diberi kode yang lebih panjang.
- Prefix-free: Tidak ada kode yang menjadi prefix dari kode lainnya, sehingga decoding dapat dilakukan tanpa ambigu.

## Prinsip Kerja
Prinsip dasar Huffman Coding:
1. Hitung frekuensi kemunculan setiap karakter.
2. Buat node pohon untuk setiap karakter dan masukkan ke priority queue (berdasarkan frekuensi).
3. Ambil dua node dengan frekuensi terkecil, lalu gabungkan jadi satu node baru.
4. Ulangi proses hingga hanya ada satu node (root).
5. Traversal pohon untuk menghasilkan kode biner: kiri = 0, kanan = 1.
6. Gantikan setiap karakter dalam teks dengan kode Huffman-nya.

## Contoh Permasalahan
Misalnya teks: "ABRACADABRA"

Frekuensi:
- A = 5
- B = 2
- R = 2
- C = 1
- D = 1

Bangun pohon Huffman dan dapatkan kode:
- A = 0
- B = 10
- R = 110
- C = 1110
- D = 1111

Teks dikompresi menjadi kode biner berdasarkan frekuensi tersebut.

## Implementasi (C++)

```cpp
{% raw %}
#include <iostream>
#include <queue>
#include <unordered_map>
using namespace std;

struct Node {
    char ch;
    int freq;
    Node *left, *right;
    
    Node(char ch, int freq) : ch(ch), freq(freq), left(nullptr), right(nullptr) {}
};

struct Compare {
    bool operator()(Node* a, Node* b) {
        return a->freq > b->freq;
    }
};

void generateCodes(Node* root, string code, unordered_map<char, string>& huffmanCode) {
    if (!root) return;
    
    if (!root->left && !root->right) huffmanCode[root->ch] = code;
    
    generateCodes(root->left, code + "0", huffmanCode);
    generateCodes(root->right, code + "1", huffmanCode);
}

void huffmanCoding(string text) {
    unordered_map<char, int> freq;
    for (char ch : text) freq[ch]++;
    
    priority_queue<Node*, vector<Node*>, Compare> pq;
    
    for (auto pair : freq) pq.push(new Node(pair.first, pair.second));
    
    while (pq.size() > 1) {
        Node *left = pq.top(); pq.pop();
        Node *right = pq.top(); pq.pop();
        
        Node* merged = new Node('\0', left->freq + right->freq);
        merged->left = left;
        merged->right = right;
        pq.push(merged);
    }
    
    unordered_map<char, string> huffmanCode;
    generateCodes(pq.top(), "", huffmanCode);
    
    cout << "Huffman Codes:\n";
    for (auto pair : huffmanCode)
        cout << pair.first << ": " << pair.second << '\n';
}

int main() {
    string text = "ABRACADABRA";
    huffmanCoding(text);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Kompresi File: ZIP, RAR menggunakan Huffman Coding untuk efisiensi ruang.
2. Kompresi Gambar dan Video: JPEG, PNG, dan MP4 memakai Huffman untuk encoding akhir.
3. Transmisi Data: Digunakan dalam protokol komunikasi untuk menghemat bandwidth.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Efisien dalam mengurangi ukuran data.
2. Sifat lossless, artinya data dapat direkonstruksi 100%.
3. Cocok untuk karakter dengan distribusi frekuensi yang tidak merata.

### Kekurangan:
1. Kurang efisien jika semua karakter memiliki frekuensi hampir sama.
2. Memerlukan overhead untuk menyimpan pohon Huffman.
3. Tidak sebaik algoritma modern seperti LZ77/LZW dalam banyak aplikasi nyata.


## Kesimpulan
Huffman Coding adalah algoritma kompresi data yang cerdas dan efisien dengan menggunakan prinsip frekuensi kemunculan karakter. Sangat berguna dalam dunia nyata terutama untuk file kompresi dan transmisi data, namun tetap memiliki keterbatasan terutama pada distribusi data yang seragam.



