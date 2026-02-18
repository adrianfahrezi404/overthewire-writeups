# Bandit Level 19 → Level 20

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

## 🎯 Objective
Menggunakan binary *setuid* bernama `bandit20-do` di homedirectory untuk membaca password yang tersimpan di `/etc/bandit_pass/bandit20`.

## 🛠 The Process
File binary `bandit20-do` memiliki *setuid bit* milik user `bandit20`. Ini berarti saat dijalankan, program ini berjalan dengan hak akses `bandit20`, bukan user kita (`bandit19`).

```bash
ls -la
./bandit20-do cat /etc/bandit_pass/bandit20
```

Dengan menjalankan perintah di atas, perintah cat dieksekusi dengan privilege bandit20, sehingga file password bisa terbaca.

## 💡 What I Learned
- Setuid (Set User ID): Izin file khusus di Linux yang mengizinkan user untuk menjalankan file eksekutabel dengan izin dari pemilik file (file owner), bukan user yang menjalankannya. Ini adalah konsep krusial dalam privilege escalation.

[⬅️ Back To Home](../README.md)
