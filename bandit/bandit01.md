# Bandit Level 1 → Level 2
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Membaca isi file yang memiliki nama berupa karakter simbol strip (`-`).

## 🛠️ The Process
File bernama `-` tidak bisa dibaca dengan perintah `cat -` biasa. Hal ini karena terminal Linux menginterpretasikan tanda strip tunggal sebagai instruksi untuk membaca dari *Standard Input* (keyboard), bukan sebagai nama file.

Untuk mengatasinya, saya harus mendefinisikan lokasi absolut atau relatif file tersebut:
```bash
cat ./-
```

Atau menggunakan path lengkap:
```Bash
cat /home/bandit1/-
```

## 💡 What I Learned
- Dash (-) Ambiguity: Memahami bagaimana shell menangani karakter spesial.
-  Relative Path (./): Teknik menunjuk file di direktori saat ini secara eksplisit untuk menghindari ambiguitas argumen perintah.
