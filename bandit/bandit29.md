# Bandit Level 29 → Level 30

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)

## 🎯 Objective

Terdapat repositori Git lain di `ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo`. Tugas kita adalah meng-*clone* repositori tersebut dan mencari kredensial untuk Level 30. Berbeda dengan tantangan sebelumnya, *password* kali ini disembunyikan di luar riwayat *commit* utama.

## 🛠️ The Process

Level ini mensimulasikan kelalaian *developer* yang memisahkan kode aman untuk tahap *production*, namun meninggalkan kredensial sensitif di *branch* *development* atau *testing*.

1. **Meng-clone Repositori:**
   
   Saya kembali mengeksekusi *cloning* dari terminal lokal saya untuk mem-*bypass* restriksi jaringan server OTW.
   ```bash
   git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo repo29
   ```

2. **Inspeksi Branch Utama:**
   
    Setelah masuk ke direktori `repo29`, saya memeriksa file `README.md` di branch default (`master`/`main`).
    ```Bash
    cd repo29
    cat README.md
    ```
    Output yang didapatkan hanyalah teks peringatan: "no passwords in production!".

3. **Reconnaissance Cabang (Branch Enum):**
   
    Karena password tidak ada di repositori utama maupun riwayatnya, saya memeriksa daftar semua branch (cabang kode) yang ada di dalam repositori ini, baik lokal maupun remote.
    ```Bash
    git branch -a
    ```
    Output menunjukkan adanya branch lain, salah satunya adalah dev (development).

4. **Branch Hopping (Eksploitasi):**
   
    Saya berpindah (checkout) dari branch utama ke branch `dev` untuk melihat versi file yang disembunyikan di sana.
    ```Bash
    git checkout dev
    ```
5. **Ekstraksi Kredensial:**
   
    Setelah berpindah branch, struktur file otomatis menyesuaikan dengan isi branch `dev`. Saya membaca kembali file `README.md`.
    ```Bash
    cat README.md
    ```
    Kali ini, file tersebut menampilkan username dan password asli dalam bentuk plaintext.

    **Password found:**

## 💡 What I Learned
- Git Branching Concept: Git memungkinkan developer bekerja di banyak cabang (branches) secara paralel. Mengeksploitasi Git tidak hanya sebatas melihat commit masa lalu, tapi juga memeriksa cabang-cabang lain yang mungkin tidak dipublikasikan secara aktif.
- Development vs Production Environments: Banyak celah keamanan terjadi karena asumsi keliru bahwa "data di branch dev/testing tidak akan terlihat oleh publik". Dalam penetration testing, selalu periksa environment non-produksi karena sering kali pengamanan di sana lebih longgar dan berisi banyak konfigurasi atau kredensial yang hardcoded.


[⬅️ Back To Home](../README.md)
