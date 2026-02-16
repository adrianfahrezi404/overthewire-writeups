# Bandit Level 8 → Level 9
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Menemukan satu-satunya baris teks yang **unik** (hanya muncul satu kali) di dalam file `data.txt` yang penuh dengan baris duplikat.

## 🛠️ The Process
Perintah `uniq` berfungsi untuk memfilter baris duplikat, tetapi ia hanya bekerja pada baris yang *berurutan*. Oleh karena itu, saya harus mengurutkan (*sort*) isi file terlebih dahulu sebelum memfilternya.

Saya menggunakan teknik *piping* (`|`) untuk menggabungkan dua perintah:
```bash
sort data.txt | uniq -u
```

Note: Flag -u berarti hanya tampilkan baris yang unik.

## 💡 What I Learned

- Piping ( | ): Konsep fundamental Linux untuk mengoper output dari satu perintah menjadi input untuk perintah berikutnya.
- Sort & Uniq: Kombinasi klasik untuk analisis data statistik sederhana di CLI.
