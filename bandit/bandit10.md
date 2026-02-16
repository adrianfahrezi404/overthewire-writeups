# Bandit Level 10 → Level 11
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Mendapatkan password yang disandikan (*encoded*) menggunakan format **Base64** di dalam file `data.txt`.

## 🛠️ The Process
Isi file `data.txt` terlihat seperti deretan huruf acak (`VGhlIHBhc3N3b3JkIGlz...`), yang merupakan ciri khas *encoding* Base64. Untuk membacanya, saya perlu melakukan *decoding*.

Perintah yang saya gunakan:
```bash
base64 -d data.txt
```

Atau alternatif menggunakan piping:
```Bash
cat data.txt | base64 --decode
```

## 💡 What I Learned
- Encoding vs Encryption: Base64 bukan enkripsi (pengamanan), melainkan encoding (representasi data) agar data biner aman dikirim melalui media teks (seperti email atau URL).
- Decoding: Proses mengembalikan data encoded ke format aslinya.

  [⬅️ Back To Home](../README.md)
