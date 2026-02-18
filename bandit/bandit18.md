# Bandit Level 18 → Level 19

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Password tersimpan di file `readme`. Masalahnya, file konfigurasi `.bashrc` telah dimodifikasi untuk langsung me-*logout* kita begitu berhasil login SSH.

## 🛠 The Process
Karena shell langsung tertutup (Bye bye!), saya harus mengirim perintah *bersamaan* dengan proses login SSH, tanpa masuk ke shell interaktif.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
whoami
ls
cat readme
```

Atau bisa juga memaksa alokasi pseudo-terminal dengan flag -t lalu memanggil shell lain:
```Bash
ssh -t bandit18@bandit.labs.overthewire.org -p 2220 "/bin/sh"
whoami
ls
cat readme
```

## 💡 What I Learned
- SSH Command Execution: Kita bisa mengeksekusi perintah langsung di remote server tanpa perlu masuk ke shell interaktifnya.
- Shell Startup Files: Memahami bahwa .bashrc dieksekusi setiap kali user login, dan bisa digunakan untuk membatasi akses (atau menjahili).

[⬅️ Back To Home](../README.md)
