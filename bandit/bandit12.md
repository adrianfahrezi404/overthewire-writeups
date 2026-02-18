# Bandit Level 12 → Level 13

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective
Password disimpan dalam file `data.txt`, yang merupakan *hexdump* dari sebuah file yang telah dikompresi berulang kali.

## 🛠 The Process
Level ini cukup panjang karena melibatkan dekompresi berulang-ulang.
1. Pertama, buat direktori kerja di `/tmp` agar rapi.
2. Kembalikan *hexdump* menjadi file biner menggunakan `xxd -r`.
3. Gunakan perintah `file` untuk mengecek jenis kompresi (gzip, bzip2, atau tar), lalu dekompresi sesuai jenisnya. Ulangi terus sampai mendapatkan teks password.

```bash
mkdir /tmp/belajarlinux
cp data.txt /tmp/belajarlinux
cd /tmp/belajarlinux
```

## Reverse hexdump
```bash
xxd -r data.txt > data_biner
```

# Cek tipe file & dekompresi berulang (contoh alur)
```bash
file data.biner       # Output: gzip compressed data
mv data_biner data_biner.gz
gzip -d data_biner.gz
```

```bash
file data_biner           # Output: bzip2 compressed data
mv data_biner data_biner.bz2
bzip2 -d data_biner.bz2
```

```bash
file data_biner           # Output: POSIX tar archive
mv data_biner data_biner.tar
tar -xf data_biner.tar
```

```bash
file data5.bin          # Output: POSIX tar archive
mv data5.bin data5.tar
tar -xf data5.tar
```

```bash
file data6.bin          # Output: bzip2 compressed data
mv data6.bin data6.bz2
bzip2 -d data6.bz2
```

```bash
file data6         # Output: POSIX tar archive
mv data6.bin data6.tar
tar -xf data6.tar
```

```bash
file data8.bin         # Output: gzip compressed data
mv data8.bin data8.gz
gzip -d data8.gz
```

```bash
file data8         # Output: ASCII text
cat data8
```

## 💡 What I Learned
- Hexdump & Reverse: Mengubah data biner menjadi heksadesimal dan sebaliknya menggunakan xxd.
- Kompresi Berulang: Mengasah kemampuan mengenali magic numbers atau tipe file menggunakan perintah file.
- Manajemen File: Mengganti ekstensi file (mv) agar tool dekompresi bisa mengenalinya.

[⬅️ Back To Home](../README.md)
