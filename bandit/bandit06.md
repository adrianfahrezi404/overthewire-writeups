# Bandit Level 6 → Level 7
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square)

## 🎯 Objective
Mencari file password yang disembunyikan di suatu tempat di dalam server (bukan di direktori Home), dengan kriteria kepemilikan user dan grup tertentu.

Kriteria File:
1.  Owned by user: **bandit7**
2.  Owned by group: **bandit6**
3.  Size: **33 bytes**

## 🛠️ The Process
Karena file tidak berada di direktori saat ini, saya harus mencari dari direktori akar (*root*) `/`. Namun, mencari di seluruh sistem biasanya menghasilkan banyak pesan *error* "Permission Denied" karena kita mencoba mengakses folder sistem yang diproteksi.

Saya menggunakan perintah `find` dengan pengalihan *Standard Error* ke `/dev/null` (blackhole) agar tampilan bersih:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Hasilnya hanya memunculkan satu jalur file yang valid (biasanya di /var/lib/...). Saya kemudian membaca isinya:

```Bash
cat /var/lib/dpkg/info/bandit7.password
```

## 💡 What I Learned

- Standard Error Redirection (2>): Di Linux, stream 2 adalah error. Mengarahkannya ke /dev/null sangat berguna untuk menyembunyikan pesan sampah saat melakukan scanning sistem.
- Root Search: Perintah find / memungkinkan pencarian global di seluruh hirarki file sistem.

[⬅️ Back To Home](../README.md)
