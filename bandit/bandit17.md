# Bandit Level 17 → Level 18

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Ada dua file: `passwords.old` dan `passwords.new`. Password level selanjutnya adalah satu-satunya baris yang berubah (berbeda) antara kedua file tersebut.

## 🛠 The Process
Saya menggunakan perintah `diff` untuk membandingkan kedua file teks baris demi baris.

```bash
diff passwords.old passwords.new
```

Output akan menunjukkan perbedaan dengan tanda < (file lama) dan > (file baru). Password baru adalah baris yang ditandai dengan >.

## 💡 What I Learned
- File Comparison: Cara mencari perbedaan/perubahan dalam file konfigurasi atau kode program.
- Perintah diff: Tool legendaris Unix untuk membandingkan file.

[⬅️ Back To Home](../README.md)
