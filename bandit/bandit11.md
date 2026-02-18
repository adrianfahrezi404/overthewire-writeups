# Bandit Level 11 → Level 12

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Password disimpan dalam file `data.txt`, di mana semua huruf kecil (a-z) dan huruf besar (A-Z) telah dirotasi sebanyak 13 posisi (ROT13).

## 🛠 The Process
Isi file ini terenkripsi dengan algoritma substitusi sederhana bernama ROT13. Saya menggunakan perintah `tr` (translate) untuk mengembalikan karakter ke posisi semula.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Perintah di atas menukar huruf A-M dengan N-Z dan sebaliknya, yang secara efektif mendekripsi ROT13.

## 💡 What I Learned
- ROT13: Sebuah cipher substitusi sederhana yang mengganti sebuah huruf dengan huruf ke-13 setelahnya dalam alfabet.
- Perintah tr: Utility command-line untuk menerjemahkan atau menghapus karakter.

[⬅️ Back To Home](../README.md)
