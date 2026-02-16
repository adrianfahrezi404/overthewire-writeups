# Bandit Level 5 → Level 6
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Mencari file password yang tersembunyi di dalam struktur direktori yang kompleks (sub-folder) berdasarkan kriteria spesifik:
1.  **Size:** 1033 bytes
2.  **Type:** Human-readable
3.  **Permission:** Not executable

## 🛠️ The Process
Mencari secara manual di folder `maybehere00` - `maybehere19` sangat tidak efisien. Saya menggunakan utilitas `find` untuk melakukan filter pencarian otomatis.

Perintah yang saya gunakan:
```bash
find . -size 1033c
```

Note: c suffix berarti bytes.

Perintah tersebut langsung mengembalikan satu lokasi file yang cocok (misal: ./maybehere07/.file2). Saya kemudian membaca isinya:
```Bash
cat ./maybehere07/.file2
```

## 💡 What I Learned
- Automation with find: Perintah ini adalah tool fundamental bagi SysAdmin untuk mencari file berdasarkan metadata (ukuran, tanggal, permission, user) tanpa harus mengetahui nama filenya.

[⬅️ Back To Home](../README.md)
