# Bandit Level 0 → Level 1
![Difficulty](https://img.shields.io/badge/Difficulty-Very_Easy-green?style=flat-square)

## 🎯 Objective
Melakukan login ke server remote menggunakan **SSH** (*Secure Shell*) pada port non-standar.

## 🛠️ The Process
Tantangan pertama adalah mengakses server. Secara default, SSH berjalan pada port 22, namun instruksi menyebutkan server Bandit menggunakan port `2220` untuk keamanan/obscurity.

Saya menggunakan perintah berikut untuk login:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Password: bandit0

Setelah berhasil masuk, saya mengecek isi direktori Home untuk mencari informasi level selanjutnya:

```Bash
ls
cat readme
```

## 💡 What I Learned

- SSH Protocol: Cara kerja dasar remote login yang aman.
- Port Flag (-p): SSH client membutuhkan flag khusus jika server target tidak menggunakan port default (22).

