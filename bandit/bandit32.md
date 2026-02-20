# Bandit Level 32 → Level 33

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Setelah berhasil masuk ke Level 32, kita langsung dijebak di dalam sebuah *Restricted Shell* khusus bernama `UPPERCASE SHELL`. Sesuai namanya, *shell* ini mencegat setiap *input* perintah yang kita ketik dan mengubah seluruh hurufnya menjadi huruf kapital (contoh: `ls` menjadi `LS`). Karena sistem operasi Linux bersifat *case-sensitive*, perintah yang dikapitalisasi tersebut tidak akan dikenali sebagai program yang valid (`command not found` / `Permission denied`). Tugas kita adalah mencari celah untuk mem-*bypass* konversi karakter ini, melepaskan diri dari *shell* terbatas tersebut, dan mengambil kredensial Level 33.

## 🛠️ The Process

Level ini adalah simulasi nyata dari teknik *Restricted Shell Escaping*. Karena kita tidak bisa menggunakan karakter alfabet (a-z) standar, kita harus menggunakan *special characters* atau variabel bawaan Linux yang kebal terhadap manipulasi kapitalisasi.

1. **Analisis Jebakan (Trap Recon):**
   
   Saat pertama kali masuk, saya menguji *shell* dengan perintah dasar seperti `whoami`.
   ```bash
   >> whoami
   sh: 1: WHOAMI: Permission denied
   ```
   Sistem merespons dengan menerjemahkannya sebagai `WHOAMI`. Ini mengonfirmasi bahwa semua huruf diubah menjadi huruf besar.

2. **Eksekusi Shell Breakout (The Bypass):**
   
    Untuk melewati batasan alfabet ini, saya menggunakan variabel parameter spesial `$0`.
    ```Bash
    >> $0
    $
    ```
    Karakter `$` dan `0` bukanlah huruf, sehingga *shell* nakal tersebut tidak bisa mengapitalisasinya. Dalam *environment* Linux/Bash, variabel `$0` menyimpan nama dari *shell* atau program yang sedang berjalan. Dengan mengeksekusi `$0`, saya memerintahkan sistem untuk memanggil ulang *shell* dasar sistem (`/bin/sh`) yang bersih dari aturan huruf kapital.

3. **Verifikasi Hak Akses (Privilege Escalation):**
   
    Setelah mendapatkan *prompt shell* biasa (`$`), saya memeriksa keadaan di sekitar menggunakan perintah `ls -la`.
    ```Bash
    $ ls -la
    ```
    *Output* menunjukkan bahwa *binary* jebakan tadi (`uppershell`) dijalankan dengan *permission* SUID milik user `bandit33`. Artinya, shell baru yang berhasil saya panggil via `$0` otomatis mewarisi hak istimewa (*privilege*) dari `bandit33`.

4. **Ekstraksi Kredensial:**
   
    Dengan hak akses penuh sebagai `bandit33`, saya langsung membaca file target untuk menyelesaikan level ini.
    ```Bash
    $ cat /etc/bandit_pass/bandit33
    ```
    **Password found:** 

## 💡 What I Learned
- **Restricted Shell Bypassing:** Membatasi *user* menggunakan custom *shell* (seperti rBash atau *script* kustom) adalah teknik keamanan yang sering diterapkan admin. Namun, jika implementasinya tidak sempurna, *attacker* selalu bisa mencari vektor pelarian (*escape vectors*).
- **Special Shell Variables:** Variabel bawaan seperti `$0` (merujuk ke nama *script/shell* yang dieksekusi) adalah *"silver bullet"* untuk memanggil ulang proses sistem. Karena formatnya menggunakan angka dan simbol, variabel ini kebal terhadap filter manipulasi huruf (*case-manipulation filters*).
- **SUID Inheritance:** Saat sebuah program SUID (seperti `uppershell`) berhasil dimanipulasi untuk membuka proses baru (seperti memanggil `/bin/sh`), proses baru tersebut akan mewarisi hak akses (EUID) tingkat tinggi dari program induknya.

[⬅️ Back To Home](../README.md)
