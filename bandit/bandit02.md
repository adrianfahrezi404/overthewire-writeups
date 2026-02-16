# Bandit Level 2 → Level 3
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square)

## 🎯 Objective
Membaca file yang nama filenya mengandung spasi: `spaces in this filename`.

## 🛠️ The Process
Di Linux, spasi berfungsi sebagai pemisah antar argumen perintah. Jika saya mengetik `cat spaces in...`, sistem akan mengira saya memerintahkan untuk membuka 3 file berbeda.

Solusi 1: Menggunakan tanda kutip (*Escaping*):
```bash
cat "spaces in this filename"
```

Solusi 2: Menggunakan Backslash (biasanya otomatis muncul saat menekan tombol TAB):
```Bash
cat spaces\ in\ this\ filename
```
💡 What I Learned

    Argument Parsing: Bagaimana shell memecah string perintah.

    Handling Whitespace: Pentingnya escaping karakter spesial dalam manajemen file Linux.
