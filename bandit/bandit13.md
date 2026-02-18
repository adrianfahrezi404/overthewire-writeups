# Bandit Level 13 → Level 14

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
## 🎯 Objective
Password disimpan di `/etc/bandit_pass/bandit14` dan hanya bisa dibaca oleh user `bandit14`. Kita diberikan private SSH key untuk login sebagai `bandit14`.

## 🛠 The Process
Kita tidak perlu mencari password teks, melainkan langsung menggunakan kunci privat (`sshkey.private`) yang ada di direktori home untuk login ke localhost sebagai user selanjutnya.

```bash
cat sshkey.private
scp -p 2220 bandit13@bandit.labs.overthewire.org:sshkey.private kunci_bandit14.pem
chmod 600 kunci_bandit14.pem
ssh -i sshkey.private kunci_bandit14.pem bandit14@bandit.labs.overthewire.org -p 2220
```

Jangan lupa opsi -i untuk menentukan file identitas (private key).

## 💡 What I Learned
- SSH Keys: Login menggunakan pasangan kunci kriptografi (public/private key) lebih aman daripada password biasa.
- Localhost Login: Kita bisa melakukan SSH ke mesin yang sama (localhost) untuk berpindah user jika memiliki kredensial yang tepat.

[⬅️ Back To Home](../README.md)
