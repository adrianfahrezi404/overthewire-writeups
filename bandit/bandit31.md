# Bandit Level 31 → Level 32

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Terdapat repositori Git di `ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo`. Tugas kita adalah meng-*clone* repositori tersebut, lalu membuat sebuah file bernama `key.txt` dengan isi `May I come in?`. File tersebut kemudian harus didorong (*push*) kembali ke server (origin) untuk mendapatkan kredensial level berikutnya. Tantangannya adalah repositori ini dilindungi oleh aturan ekstensi file.

## 🛠️ The Process

Level ini berfokus pada teknik mem-*bypass* filter pengunggahan file di sisi klien (*client-side filtering*) menggunakan fitur bawaan Git.

1. **Meng-clone Repositori:**
   
   Saya kembali menggunakan terminal lokal untuk melakukan *cloning* dari *remote server*.
   ```bash
   git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo repo31
   ```
2. **Membuat File Target:**
   
    Saya masuk ke direktori repositori dan membuat file sesuai instruksi menggunakan redirection.
    ```Bash
    cd repo31
    echo "May I come in?" > key.txt
    ```
    
3. **Bypass File Filter (.gitignore):**
   
    Jika mencoba menambahkan file tersebut dengan perintah standar (`git add key.txt`), Git akan menolaknya karena file dengan ekstensi `.txt` masuk dalam daftar blokir di file `.gitignore`.

    Sebagai attacker, filter lokal ini sangat mudah dilewati dengan menambahkan argumen `-f` (*force*), yang memaksa Git untuk mengabaikan aturan `.gitignore`.
    ```Bash
    git add -f key.txt
    ```
    
4. **Konfigurasi Identitas (Local Troubleshooting):**
    Karena terminal *environment* lokal saya baru saja menginstal Git, saya harus mendeklarasikan identitas palsu agar Git mengizinkan pembuatan riwayat (*commit*).
    ```Bash
    git config --global user.email "hacker@bandit.com"
    git config --global user.name "Mas Yaan"
    ```

5. **Commit & Push (Triggering Server Hooks):**
   
    Setelah melakukan *commit*, saya mendorong (*push*) data tersebut ke server target.
    ```Bash
    git commit -m "bypass gitignore dan kirim key"
    git push
    ```
    
    **Hasil:**
   
    Setelah *push* dieksekusi, *script* otomatis di server target (*Git pre-receive hook*) mendeteksi anomali tersebut, mencegat *push*, dan menampilkan *password* level 32 di terminal balasan.

    Password found: 

## 💡 What I Learned
- **Client-Side Security is a Myth:** Mengandalkan `.gitignore` sebagai mekanisme keamanan untuk mencegah developer (atau *attacker*) mengunggah file berbahaya adalah praktik yang buruk. Aturan lokal selalu bisa di-*bypass* oleh pengguna (dalam hal ini menggunakan parameter `--force`).
- **Git Hooks for Automation:** Server OTW menggunakan *Git Hooks*, yaitu *script* yang berjalan otomatis setiap kali terjadi event tertentu di repositori Git (seperti *pre-receive* saat menerima *push*). Ini sering digunakan di CI/CD, namun juga bisa dimanfaatkan untuk *monitoring* keamanan atau *flag capture* dalam skenario CTF.

[⬅️ Back To Home](../README.md)
