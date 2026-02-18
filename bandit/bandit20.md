# Bandit Level 20 → Level 21

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Ada binary *setuid* bernama `suconnect` yang akan menghubungkan diri ke port localhost yang kita tentukan. Jika kita mengirimkan password level saat ini ke koneksi tersebut, binary akan membalas dengan password level selanjutnya.

## 🛠 The Process
Saya membutuhkan dua terminal (sesi SSH) untuk menyelesaikan ini.

1. **Terminal 1 (Listener):** Saya membuat listener menggunakan Netcat di port sembarang (misal 5555) yang akan otomatis mengirimkan password level 20 saat ada yang connect.
   
   ```bash
   echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l -p 4444
   ```
2. **Terminal 2 (Executor):** Saya menjalankan binary suconnect dan mengarahkannya ke port listener saya.
    ```Bash
    ./suconnect 4444
    ```
    
Setelah binary connect, Netcat di Terminal 1 mengirim password lama, binary memverifikasi, lalu binary mengirim balik password baru yang akan muncul di Terminal 2.

## 💡 What I Learned
- Network Listener & Client: Mempraktikkan konsep server (yang menunggu/listen) dan client (yang menghubugi/connect) secara manual.
- Interprocess Communication: Bagaimana dua proses (nc dan suconnect) bertukar data melalui jaringan lokal.

[⬅️ Back To Home](../README.md)
