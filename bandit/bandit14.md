# Bandit Level 14 → Level 15

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## 🎯 Objective
Mengirimkan password level saat ini ke port **30000** di **localhost** untuk mendapatkan password selanjutnya.

## 🛠 The Process
Saya menggunakan `nc` (Netcat) untuk terhubung ke port 30000 dan mengirimkan isi file password saat ini.

```bash
cat /etc/bandit_pass/bandit14
nc localhost 30000
```

Server merespons dengan memberikan password untuk level 15.

## 💡 What I Learned
- Network Socket: Konsep dasar komunikasi data antar proses melalui jaringan.
- Netcat (nc): "Pisau lipat" jaringan Swiss Army yang bisa digunakan untuk membaca dan menulis data melalui koneksi jaringan (TCP/UDP).

[⬅️ Back To Home](../README.md)
