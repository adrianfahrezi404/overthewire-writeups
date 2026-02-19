# Bandit Level 30 → Level 31

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Terdapat repositori Git di `ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo`. Tugas kita adalah meng-*clone* repositori tersebut dan mencari kredensial untuk Level 31. File di repositori utama ternyata kosong, sehingga kita perlu mengandalkan teknik enumerasi Git tingkat lanjut untuk menemukan data yang disembunyikan.

## 🛠️ The Process

Level ini mensimulasikan pencarian kredensial tersembunyi menggunakan fitur pelabelan (*Tags*) pada Git.

1. **Meng-clone Repositori (Remote Execution):**
   
   Melanjutkan metodologi eksekusi dari perimeter luar, saya mengunduh repositori target langsung ke terminal laptop lokal menggunakan protokol SSH di port `2220`.
   ```bash
   git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo repo30
   ```

2. **Inspeksi Awal (Jalan Buntu):**
   
    Setelah masuk ke direktori `repo30`, saya membaca file `README.md`.
    ```Bash
    cd repo30
    cat README.md
    ```
    
    *Output*-nya hanya berupa teks pancingan: *"just an epmty file... muahaha"*. Mengecek riwayat dengan `git log` atau cabang dengan `git branch -a` juga tidak membuahkan hasil, repositori terlihat bersih.

3. **Enumerasi Git Tags:**
   
    Karena vektor commit dan *branch* tidak memberikan hasil, saya beralih memeriksa daftar *tag* (label) yang disematkan di dalam repositori ini.
    ```Bash
    git tag
    ```
    Perintah ini mengembalikan output satu tag bernama `secret`.

4. **Ekstraksi Kredensial:**
   
    Untuk melihat informasi atau pesan (metadata) yang disimpan di dalam tag `secret` tersebut, saya mengeksekusi perintah `git show`.
    ```Bash
    git show secret
    ```
    Sistem Git langsung mengekstrak dan menampilkan isi dari tag tersebut, yang mana adalah *password* untuk level berikutnya.

    **Password found:**

## 💡 What I Learned
- **Git Tags Concept:** Fitur *tag* di Git umumnya digunakan untuk menandai milestone atau rilis versi tertentu dari sebuah software (misal: `v1.0`, `v2.0`). Namun, fitur ini juga memungkinkan *developer* untuk menyematkan pesan atau anotasi teks bebas di dalamnya.
- **Hidden Data Vectors:** Terkadang *developer* menggunakan tag untuk meninggalkan catatan rahasia, *API Key*, atau *password*, lalu melupakannya karena tag tidak muncul secara eksplisit pada pemeriksaan riwayat *log* atau *branch* standar.
- **Comprehensive Git Enumeration:** Dalam skenario Red Teaming maupun Bug Bounty, melakukan enumerasi menyeluruh tidak hanya berfokus pada Source Code utama. Membedah riwayat (`git log`), cabang (`git branch`), dan pelabelan (`git tag`) adalah prosedur wajib untuk menemukan celah kebocoran informasi (Information Disclosure / Credential Leak).

[⬅️ Back To Home](../README.md)
