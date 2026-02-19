# Bandit Level 27 → Level 28

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Kita diberikan informasi bahwa terdapat sebuah repositori Git di `ssh://bandit27-git@localhost/home/bandit27-git/repo`. Tugas kita adalah meng-*clone* repositori tersebut menggunakan protokol SSH untuk menemukan *password* Level 28. *Password* untuk *user* `bandit27-git` sama dengan *password* *user* `bandit27`.

## 🛠️ The Process

Level ini mensimulasikan pencarian kredensial bocor (*credential leak*) pada *version control system*. Awalnya saya mencoba membuat *temporary directory* (`mktemp -d`) dan melakukan *clone* dari dalam *shell* `bandit27`. Namun, eksekusi tersebut gagal karena server menerapkan *firewall rule* yang memblokir koneksi SSH dari jaringan internal (`localhost`). 

Oleh karena itu, saya memutuskan untuk mem-*bypass* restriksi tersebut dengan menarik *source code*-nya langsung dari laptop lokal saya (*perimeter luar*).

1. **Persiapan Environment Lokal:**
   
   Karena saya melakukan eksekusi murni dari terminal lokal Linux saya (WSL/Ubuntu), saya menyadari bahwa *package* Git belum terinstal. Saya melakukan instalasi terlebih dahulu:
   ```bash
   sudo apt update
   sudo apt install git
   ```
2. **Eksekusi Remote Clone:**
   
    Setelah Git siap, saya melakukan cloning repositori secara langsung dengan mengarahkan URL SSH ke domain publik OverTheWire, bukan ke `localhost`. Karena layanan SSH berjalan di port `2220`, port tersebut wajib dicantumkan.
    ```Bash
    git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
    ```
    Saat muncul prompt autentikasi, saya memasukkan password dari user `bandit27`.

3. **Membaca Informasi Rahasia:**
   
    Setelah repositori berhasil diunduh ke laptop lokal, saya masuk ke dalam direktori repo dan langsung memeriksa file yang tersedia.
    ```Bash
    cd repo
    ls -la
    cat README
    ```
    Password untuk level `bandit28` tertulis secara gamblang dalam bentuk plaintext di dalam file `README` tersebut.

## 💡 What I Learned
- **Network Restriction Bypass:** Sama seperti kasus di Level 25, ketika pergerakan lateral di dalam mesin target dibatasi ketat oleh sistem (seperti blokir koneksi `localhost`), menarik (cloning / eksfiltrasi) data langsung ke mesin lokal kita sendiri adalah teknik bypass yang sangat efektif.
- **Local Tooling Readiness:** Dalam aktivitas red teaming atau penetration testing, kita tidak bisa selalu mengandalkan alat bawaan dari server target (LotL - Living off the Land). Menyiapkan environment lokal dengan tools dasar (seperti `git`, `nc`, `nmap`) adalah hal yang krusial.
- **Git over SSH (Custom Port):** Protokol Git beroperasi sangat mulus di atas SSH. Menentukan port spesifik (seperti `2220`) pada URL SSH Git adalah trik penting jika target tidak menggunakan standar port 22.
- **Hardcoded Credentials:** Skenario ini adalah representasi nyata dari kelemahan credential exposure, di mana developer tanpa sengaja menaruh password atau data sensitif di dalam repositori kode (bahkan di dalam file transparan seperti `README`).

[⬅️ Back To Home](../README.md)
