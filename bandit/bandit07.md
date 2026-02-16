# Bandit Level 7 → Level 8
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Menemukan password di dalam file `data.txt` yang berisi ribuan baris teks, tepat di sebelah kata kunci **"millionth"**.

## 🛠️ The Process
Membaca file `data.txt` secara manual tidak mungkin dilakukan karena ukurannya yang besar. Saya menggunakan utilitas `grep` untuk memfilter baris yang mengandung kata spesifik.

Perintah yang saya gunakan:
```bash
grep "millionth" data.txt
```

## 💡 What I Learned

- Grep (Global Regular Expression Print): Salah satu tool paling kuat di Linux untuk mencari pola teks (pattern matching) di dalam file atau output perintah

[⬅️ Back To Home](../README.md)
