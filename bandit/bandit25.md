# Bandit Level 25 → Level 26

![Difficulty](https://img.shields.io/badge/Difficulty-Hard-red)

## 🎯 Objective

Kita diberikan sebuah *private SSH key* (`bandit26.sshkey`) untuk login sebagai `bandit26`. Namun, *shell* default untuk user `bandit26` tidak menggunakan bash biasa, melainkan sebuah *script* khusus yang mengeksekusi program *pager* `more`. Jika layar terminal terlalu besar, *script* akan langsung selesai dan koneksi SSH ditutup. Selain itu, server menerapkan sistem keamanan yang memblokir koneksi SSH dari jaringan internal (*localhost*). Kita harus mem-*bypass* pemblokiran jaringan dan melakukan eskalasi dari *pager* untuk mendapatkan *shell* interaktif.

## 🛠️ The Process

Karena server OverTheWire memblokir koneksi `localhost` secara ketat untuk mencegah *bruteforce* / *resource exhaustion*, saya harus melakukan eksfiltrasi kunci ke mesin lokal dan melakukan serangan dari luar (perimeter luar).

1. **Eksfiltrasi Kunci SSH**: Saya membaca isi dari file `bandit26.sshkey` di `bandit25` dan menyalinnya ke sebuah file baru di laptop lokal saya bernama `kunci_bandit26.key`.

2. **Mengamankan Kunci Lokal**: Agar OpenSSH di mesin lokal tidak menolak file kunci karena *permission* yang terlalu terbuka, saya mengubah hak aksesnya:
   ```bash
   chmod 600 kunci_bandit26.key
   ```
3. **Memicu Mode Pager (Terminal Shrinking):** Untuk mencegah script more langsung tertutup, saya memperkecil ukuran jendela terminal lokal saya secara ekstrem (hanya menyisakan 3-4 baris).

4. **Eksekusi SSH Bypass:** Saya melakukan koneksi SSH langsung ke server eksternal Bandit menggunakan kunci yang sudah dieksfiltrasi.

    ```Bash
    ssh -i kunci_bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
    ```
    (Koneksi berhasil masuk tanpa terblokir rule localhost, dan layar tertahan di tulisan `--More--`)

5. **Vim Breakout (Shell Escalation):**
    Saat terminal tertahan di pager `--More--`, saya menekan tombol `v` untuk masuk ke mode teks editor Vim. Dari dalam Vim, saya mengeksekusi command internal untuk mengubah environment shell dan memanggil bash:
    - Mengetik `:set shell=/bin/bash` lalu menekan `Enter`.
    - Mengetik `:shell` lalu menekan `Enter`.

    Saya berhasil mendapatkan shell penuh sebagai bandit26!

6. **Mengambil Password:** Setelah berhasil menguasai shell, saya tinggal membaca file password untuk level 26.
    ```Bash
    cat /etc/bandit_pass/bandit26
    ```
    
## 💡 What I Learned
- Network Pivot & Exfiltration: Jika pergerakan lateral (lateral movement) di dalam mesin diblokir oleh firewall/PAM rules, mengeksfiltrasi kredensial (seperti private key) ke luar jaringan dan menyerang dari perimeter eksternal adalah metode bypass yang efektif.
- Restricted Shell Bypass: Program interaktif seperti more, less, atau vi sering kali memiliki celah (mekanisme shell escape) yang memungkinkan pengguna mengeksekusi sistem shell utuh dari dalamnya.
- Terminal Dimensions & Pager Behavior: Mengetahui bahwa program pager merespons ukuran kolom/baris dari environment terminal (tty) dapat dimanfaatkan sebagai vektor serangan untuk menahan eksekusi script agar tidak langsung terminate.

 [⬅️ Back To Home](../README.md)
