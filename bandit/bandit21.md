# Bandit Level 21 → Level 22

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Mencari password yang diproses oleh sebuah program yang berjalan otomatis secara berkala (*cron job*).

## 🛠 The Process
Langkah pertama adalah memeriksa direktori konfigurasi cron untuk melihat tugas apa saja yang sedang berjalan.

1. **Cek Konfigurasi Cron:**
   Saya memeriksa direktori `/etc/cron.d/` dan menemukan file konfigurasi bernama `cronjob_bandit22`.
   ```bash
   cd /etc/cron.d/
   cat cronjob_bandit22
   ```

   Output:
   ```bash
    @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
   ```
    Ini menunjukkan bahwa script /usr/bin/cronjob_bandit22.sh dijalankan setiap menit oleh user bandit22.

 2. **Analisis Script:**
    Saya membaca isi script tersebut untuk mengetahui apa yang dilakukannya.
    (Catatan: Saya tidak menjalankan scriptnya, tapi hanya membaca isinya dengan cat agar output tidak terbuang ke /dev/null).
    ```Bash
    cat /usr/bin/cronjob_bandit22.sh
    ```
    Isi script:
    ```Bash
    #!/bin/bash
    chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    ```
    
    Ternyata script ini menyalin password dari /etc/bandit_pass/bandit22 ke sebuah file sementara di folder /tmp/ dan memberikannya akses baca (chmod 644).

3. **Mendapatkan Password:**
    Karena file tujuannya sudah diketahui dari script di atas, saya tinggal membacanya.

    ```Bash
    cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    ```
    
    Hasilnya adalah password untuk level 22.

## 💡 What I Learned
- Cron Jobs Analysis: Cara melacak program otomatis dengan membaca konfigurasi di /etc/cron.d/.
- Bash Script Reading: Membaca logika script orang lain untuk menemukan lokasi file rahasia.
- Redirection (&> /dev/null): Memahami bahwa output script seringkali dibuang ke "black hole" (/dev/null) agar tidak memenuhi log sistem, sehingga kita harus membaca source code-nya langsung, bukan menjalankannya secara buta.


[⬅️ Back To Home](../README.md)
