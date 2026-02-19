# Bandit Level 28 → Level 29

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Terdapat sebuah repositori Git di `ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo`. Tugas kita adalah meng-*clone* repositori tersebut dan menemukan *password* untuk Level 29. Berbeda dengan level sebelumnya, *password* kali ini tidak ada secara gamblang di versi file saat ini.

## 🛠️ The Process

Level ini merepresentasikan celah keamanan nyata di mana seorang *developer* tidak sengaja mengekspos kredensial, lalu mencoba menghapusnya di masa depan tanpa menyadari bahwa sistem *version control* merekam semuanya.

1. **Meng-clone Repositori (Remote Execution):**
   
   Sama seperti taktik di level 27, saya mengeksekusi *cloning* repositori ini murni dari perimeter luar (terminal laptop lokal saya) untuk menghindari pemblokiran jaringan *localhost* di server Bandit.
   ```bash
   git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo repo28
   ```
2. **Inspeksi Awal (Reconnaissance):**
   
    Setelah repositori berhasil diunduh, saya masuk ke direktori `repo28` dan membaca file `README.md`.
    ```Bash
    cd repo28
    cat README.md
    ```
    Output menunjukkan bahwa kredensial sudah disensor:
    `password: xxxxxxxxxx`

3. **Membongkar Riwayat Git (Git Log Analysis):**
   
    Karena Git mencatat setiap perubahan kode, saya memeriksa riwayat commit beserta patch atau perbedaannya (diff) dari waktu ke waktu menggunakan parameter `-p`.
    ```Bash
    git log -p
    ```
    Saya menggulir (scroll) riwayat tersebut dan menemukan sebuah commit lawas dengan pesan `fix info leak`. Pada detail diff di bawahnya, terlihat jelas teks berwarna merah (yang dihapus) berisi password asli, yang kemudian diganti dengan teks hijau (yang ditambahkan) berisi xxxxxxxxxx.

    **Password found**

## 💡 What I Learned
- Git History is Permanent: Menghapus data sensitif (seperti kredensial, API Key, atau konfigurasi) lalu melakukan commit baru TIDAK akan menghapus data tersebut dari repositori. Siapa pun yang memiliki akses ke repositori dapat melihat riwayatnya secara utuh.
- Sensitive Data Exposure: Dalam aktivitas Bug Bounty atau Red Teaming, memeriksa riwayat (commit history) dari sebuah repositori publik atau internal adalah salah satu vektor reconnaissance yang paling krusial untuk menemukan jejak kredensial masa lalu yang masih aktif (credential leak).

[⬅️ Back To Home](../README.md)

