# Bandit Level 4 → Level 5
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Mengidentifikasi satu-satunya file tipe teks (*human-readable*) di antara sekumpulan file data biner.

## 🛠️ The Process
Direktori `inhere` berisi banyak file bernama `-file00` hingga `-file09`. Jika dibaca dengan `cat`, sebagian besar berisi karakter sampah (binary data) yang mengacaukan tampilan terminal.

Saya menggunakan perintah `file` untuk melakukan analisis tipe data (reconnaissance):
```bash
file ./*
```

Output menunjukkan hanya satu file yang berjenis ASCII text.

```bash
./-file07: ASCII text
```

Maka, file itulah yang berisi password:

```Bash
cat ./-file07
```

## 💡 What I Learned

- File Signatures: Ekstensi di Linux tidak menentukan isi file. Perintah file sangat krusial untuk menentukan jenis data (berdasarkan Magic Numbers) sebelum kita membukanya.

[⬅️ Back To Home](../README.md)
