# Bandit Level 26 → Level 27

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective

Setelah berhasil mendapatkan *shell* interaktif sebagai `bandit26`, tugas kita adalah menemukan *password* untuk level 27. Di dalam direktori *home* `bandit26`, terdapat sebuah file *executable* khusus bernama `bandit27-do` yang memiliki hak akses SUID (*Set-user Identification*). Kita harus memanfaatkan *binary* ini untuk mengeksekusi perintah pembacaan file *password* level 27 yang aslinya dikunci dari kita.

## 🛠️ The Process

Proses di level ini murni berfokus pada teknik eskalasi hak istimewa (*Privilege Escalation*) dasar menggunakan SUID.

1. **Reconnaissance (Pengecekan Direktori):**
   
   Langkah pertama adalah melihat isi direktori saat ini beserta hak akses (*permissions*) setiap file secara mendetail.
   ```bash
   ls -la
   ```
   Output menunjukkan adanya file `bandit27-do` dengan permission `-rwsr-x---`. Huruf `s` pada segmen user menandakan bahwa file ini memiliki atribut SUID aktif.

2. **Eksekusi SUID Binary:**
   
    Mengingat binary `bandit27-do` dibuat oleh `bandit27` dan memiliki atribut `s`, maka perintah apa pun yang dijalankan melaluinya akan dieksekusi seolah-olah kita adalah `bandit27`. Saya menggunakan binary ini untuk memanggil program `cat` dan membaca file password rahasia di direktori `/etc/`.

    ```Bash
    ./bandit27-do cat /etc/bandit_pass/bandit27
    ```
3. **Hasil:**
   
    Perintah berhasil dieksekusi dengan hak akses `bandit27`, me-bypass pembatasan permission standar `bandit26`, dan langsung menampilkan password untuk level selanjutnya di layar.

## 💡 What I Learned
- **SUID (Set Owner User ID):** SUID adalah atribut izin khusus pada Linux/Unix yang diberikan kepada sebuah executable file. SUID memungkinkan pengguna biasa menjalankan file tersebut dengan hak akses penuh (privileges) milik pemilik file (dalam hal ini `bandit27`), bukan hak akses pengguna yang menjalankannya (`bandit26`).
- **Privilege Escalation Vector:** Dalam simulasi red teaming, mencari binary SUID yang dikonfigurasi secara keliru (misconfigured SUID binaries) adalah salah satu teknik paling fundamental untuk melakukan eskalasi dari low-privilege user menuju akses tingkat tinggi atau root.
- **Pentingnya SUID Enum:** File seperti `bandit27-do` pada dasarnya bertindak sebagai perantara yang sah untuk melewati restriksi pembacaan file di tingkat Operating System.

[⬅️ Back To Home](../README.md)
