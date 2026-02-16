# Bandit Level 9 → Level 10
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Mengambil *string* yang dapat dibaca manusia (*human-readable*) dari sebuah file biner `data.txt`, di mana password diawali dengan beberapa karakter `=`.

## 🛠️ The Process
File `data.txt` di level ini adalah file biner. Jika dibuka dengan `cat`, terminal akan menampilkan karakter sampah. Saya menggunakan perintah `strings` untuk mengekstrak teks ASCII dari file biner tersebut, lalu memfilternya.

```bash
strings data.txt | grep "="
```

Hasilnya menunjukkan beberapa baris, dan saya mengambil teks di sebelah tanda ==========.

## 💡 What I Learned

- Binary vs Text: Memahami bahwa file biner mengandung instruksi mesin yang tidak bisa dibaca langsung.
- Strings Command: Alat forensik dasar untuk mengintip isi file biner (biasanya dipakai untuk analisis malware atau reverse engineering sederhana).
