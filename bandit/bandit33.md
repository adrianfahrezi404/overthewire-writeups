# Bandit Level 33 → END 🏆

![Status](https://img.shields.io/badge/Status-Completed-gold)

## 🎯 Objective

Tantangan terakhir! Setelah berhasil mendapatkan kredensial untuk `bandit33` melalui celah manipulasi parameter pada *Restricted Shell*, tugas kita sekarang hanyalah masuk ke server dan mengklaim kemenangan.

## 🛠️ The Process

Tidak ada lagi jebakan *firewall*, *restricted shell*, atau *hidden files* di level ini. Ini adalah ruang selebrasi.

1. **Login Terakhir:**
   
   Saya menggunakan kredensial `bandit33` untuk masuk ke server.
   ```bash
   ssh bandit33@bandit.labs.overthewire.org -p 2220
   ```
2. **Klaim Kemenangan:**
   
    Saya memeriksa direktori utama dan menemukan sebuah file bernama `README.txt`, lalu membacanya.
    ```Bash
    ls
    cat README.txt
    ```
    
4. **Pesan Penyelesaian:**
   
    Sistem menampilkan pesan resmi dari kreator OverTheWire:

   "Congratulations on solving the last level of this game!

   At this moment, there are no more levels to play in this game. However, we are constantly working on new levels and will most likely expand this game with more levels soon. Keep an eye out for an announcement on our usual communication channels!
   In the meantime, you could play some of our other wargames.

   If you have an idea for an awesome new level, please let us know!"

## 💡 The Journey (Wrap-Up)

Menyelesaikan wargame **OverTheWire: Bandit** memberikan fondasi yang sangat kuat dalam navigasi sistem Linux dan *Cyber Security*. Beberapa teknik esensial yang berhasil saya kuasai melalui wargame ini meliputi:

  - **Linux Command Line Mastery:** Manipulasi data menggunakan `grep`, `awk`, `sed`, `sort`, `uniq`, `tar`, `tr`, dan ekspresi reguler.
  - **Network Interacting:** Menggunakan `nc` (Netcat), `nmap`, dan `openssl` untuk berinteraksi dengan layanan dan daemon jaringan.
  - **Privilege Escalation Dasar:** Mengeksploitasi *misconfigured* SUID/SGID *binaries* dan memahami *cron jobs*.
  - **Cryptography & Hashing:** Dekripsi data dasar (Base64, ROT13, Hex) dan pemahaman kunci SSH (*public/private keys*).
  - **Git Version Control Enumeration:** Membongkar rahasia dari riwayat *commit*, cabang (*branches*), tag, dan mem-*bypass* filter `.gitignore`.
  - **Restricted Shell Breakouts:** Menemukan celah pelarian dari Vim *pager*, manipulasi *environment variable* (seperti `$0`), dan *shell* interaktif kustom.

Wargame ini adalah langkah awal yang luar biasa untuk melangkah lebih jauh ke dunia *Red Teaming*, *Penetration Testing*, dan *Bug Bounty*.

[⬅️ Back To Home](../README.md)
