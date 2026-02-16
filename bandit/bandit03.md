# Bandit Level 3 → Level 4
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Menemukan dan membaca file yang tersembunyi (*hidden file*) di dalam sebuah direktori.

## 🛠️ The Process
Setelah masuk ke direktori `inhere` menggunakan `cd`, perintah `ls` biasa tidak menampilkan output apa pun.

Saya menggunakan flag `-a` (*all*) untuk melihat file tersembunyi (dotfiles):
```bash
cd inhere
ls -la
cat ./"...Hiding-From-You"
```

## 💡 What I Learned

- Hidden Files: Konsep file yang diawali titik (.) di Linux (seperti .bashrc, .git) yang disembunyikan secara default agar direktori terlihat bersih.
- Ls Flags: Penggunaan opsi -la (list all + long format) adalah standar untuk inspeksi direktori secara menyeluruh.
