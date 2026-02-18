# Bandit Level 15 → Level 16

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Mengirimkan password level saat ini ke port **30001** di **localhost** menggunakan enkripsi **SSL/TLS**.

## 🛠 The Process
Netcat biasa tidak mendukung enkripsi SSL secara default. Oleh karena itu, saya menggunakan `openssl s_client` untuk melakukan koneksi aman.

```bash
openssl s_client -connect localhost:30001
```

Setelah koneksi "CONNECTED" dan handshake berhasil, saya memasukkan password level 15, dan server membalas dengan password level 16.

## 💡 What I Learned
- SSL/TLS: Memahami bahwa data bisa dikirim secara aman (terenkripsi) melalui jaringan.
- OpenSSL: Tool standar industri untuk berinteraksi dengan protokol SSL/TLS, debugging sertifikat, dan koneksi aman.

[⬅️ Back To Home](../README.md)
