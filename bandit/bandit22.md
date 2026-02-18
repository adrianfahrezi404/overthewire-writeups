# Bandit Level 22 → Level 23

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Sama seperti level sebelumnya, sebuah program berjalan otomatis melalui cron job. Namun kali ini, lokasi file password tidak ditulis secara eksplisit, melainkan ditentukan secara dinamis berdasarkan nama user yang menjalankan script tersebut.

## 🛠 The Process
Langkah pertama adalah mencari tahu script apa yang dijalankan oleh cron job milik user target (`bandit23`).

1. **Cek Konfigurasi Cron:**
   Saya melihat isi direktori `/etc/cron.d/` dan membaca konfigurasi `cronjob_bandit23`.
   ```bash
   cat /etc/cron.d/cronjob_bandit23
   ```
   
   Output:
   ```bash
   @reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
   * * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
   ```

   Script /usr/bin/cronjob_bandit23.sh dijalankan setiap menit oleh user bandit23.

2. **Analisis Logika Script:**
    Saya membaca isi script shell tersebut:
    ```Bash
    cat /usr/bin/cronjob_bandit23.sh
    ```
    
    Isi script:
    ```Bash
    #!/bin/bash
    myname=$(whoami)
    mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
    echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
    cat /etc/bandit_pass/$myname > /tmp/$mytarget
    ```
    
    **Analisis:**
   
    Script ini membuat nama file tujuan (mytarget) dengan cara mengambil string "I am user [namauser]", lalu mengubahnya menjadi hash MD5.

    Masalahnya: Jika saya menjalankan script ini secara langsung, variabel $myname akan berisi bandit22 (user saya sekarang), sehingga hash-nya salah. Padahal, cron job menjalankannya sebagai bandit23.

3. **Replikasi Hash (Manual Execution):**
   
    Untuk mendapatkan nama file yang benar, saya harus meniru logika script tersebut tapi mengganti $myname menjadi bandit23 secara manual di terminal.
    ```Bash
    echo I am user bandit23 | md5sum | cut -d ' ' -f 1
    ```

   Output Hash: `8ca319486bfbbc3663ea0fbe81326349`

4. **Ambil Password:**
   
    Setelah mendapatkan hash (yang merupakan nama file rahasia), saya langsung membaca isinya di direktori /tmp/.
    ```Bash
    cat /tmp/8ca319486bfbbc3663ea0fbe81326349
    ```

   Hasilnya adalah password untuk level 23.

## 💡 What I Learned
- Bash Script Variables: Memahami bagaimana variabel seperti $(whoami) bekerja dan bagaimana nilainya bergantung pada user yang menjalankan proses tersebut.
- Manual Logic Replication: Teknik hacking sederhana di mana kita tidak perlu menjalankan program target, tetapi cukup meniru logikanya dengan input yang kita modifikasi (dalam hal ini, mengganti user) untuk memprediksi outputnya.
- MD5 Hashing: Algoritma hashing satu arah yang sering digunakan untuk membuat string unik (checksum) dari sebuah input teks.

[⬅️ Back To Home](../README.md)
