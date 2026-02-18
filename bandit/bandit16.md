# Bandit Level 16 → Level 17

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## 🎯 Objective
Mencari server yang mendengarkan (listening) di port antara **31000 sampai 32000**. Server yang benar menggunakan SSL dan akan memberikan kredensial (SSH Key) jika dikirimi password saat ini.

## 🛠 The Process
1. **Scanning Port:** Menggunakan `nmap` untuk mencari port yang terbuka di rentang spesifik.
   ```bash
   nmap -p 31000-32000 localhost
   ```
2. **Scanning Port:** Menggunakan `nmap` untuk mengecek port yang terbuka di 31046, 31518, 31691, 31790, 31960
   ```bash
   nmap -sV -p 31046,31518,31691,31790,31960 localhost
   ```
    
3. **Identifikasi Layanan:** Dari hasil scan, saya mengecek port mana yang menjalankan SSL.
    ```Bash
    openssl s_client -connect localhost:31790
    ```
    (Port mungkin berbeda, sesuaikan dengan hasil scan).

4. **Mendapatkan Kunci:** Setelah mengirim password ke port yang tepat, server memberikan RSA Private Key.
    ```Bash
    openssl s_client -connect localhost:31790 -quite
    ```

5. **Login:** Saya menyimpan kunci tersebut ke file (misal key17), mengubah permission menjadi 600, dan login.
    ```Bash
    nano kunci_bandit17.pem      # Paste key di sini
    chmod 600 kunci_bandit17.pem # Penting! SSH menolak key yang terlalu terbuka
    ssh -i kunci_bandit17.pem bandit17@bandit.labs.overthewire.org -p 2220
    ```
    
## 💡 What I Learned
- Port Scanning: Mengidentifikasi layanan yang berjalan di jaringan menggunakan nmap.
- Permission SSH Key: File private key harus memiliki permission 600 (hanya owner yang bisa baca/tulis) agar bisa digunakan.

[⬅️ Back To Home](../README.md)
