# 🚩 OverTheWire: Security Wargames Write-ups

![Status](https://img.shields.io/badge/Status-Active_Learning-success?style=for-the-badge&logo=git)
![Platform](https://img.shields.io/badge/Platform-Linux-orange?style=for-the-badge&logo=linux)
![Focus](https://img.shields.io/badge/Focus-Red_Teaming-red?style=for-the-badge&logo=kalilinux)

## 🕵️‍♂️ About This Repository

Repository ini berfungsi sebagai **Learning Journal** dan dokumentasi teknis saya dalam menyelesaikan tantangan *Capture The Flag* (CTF) dari [OverTheWire](https://overthewire.org/). 

Proyek ini awalnya dimulai sebagai bagian dari tugas beasiswa, namun kini sepenuhnya menjadi wadah pembelajaran otodidak saya untuk mengasah insting dan kemampuan fundamental dalam *Cyber Security*.

Fokus utama pembelajaran:
* **Linux System Administration & Enumeration**
* **Bash Scripting, Automation & Data Manipulation**
* **Security Concepts** (Privilege Escalation, SSH, Version Control, Cryptography)

> *"The best way to learn is by doing (and documenting)."*

---

## 🛠️ Tools & Arsenal
Kumpulan perintah dan *tools* yang saya kuasai selama menembus tantangan di server ini:
`ssh` `grep` `awk` `sed` `find` `tar` `tr` `base64` `openssl` `nc` `nmap` `git`

---

## 📊 Challenges & Progress Matrix

Berikut adalah *dashboard* status pengerjaan wargame saya. Klik pada tautan (jika sudah tersedia) untuk melihat detail metodologi dan *write-up* penyelesaiannya.

### 🟢 Bandit (Linux Fundamentals & Red Teaming Basics)
*Status: **100% COMPLETED** (Level 0 - 34) 🏆*

| Level Range | Status | Key Concepts Learned | Write-up Link |
| :--- | :---: | :--- | :---: |
| **Level 0 → 5** | ✅ Done | SSH, File types, Hidden files, `find` | [View Logs](./bandit/level00-05.md) |
| **Level 6 → 10** | ✅ Done | File ownership, `grep`, data piping, encoding | [View Logs](./bandit/level06-10.md) |
| **Level 11 → 20** | ✅ Done | Compression, Hexdumps, Network sockets (`nc`, `openssl`) | [View Logs](./bandit/level11-20.md) |
| **Level 21 → 26** | ✅ Done | Cronjobs, Shell scripting, Pager breakout, Network restriction bypass | [View Logs](./bandit/level21-26.md) |
| **Level 27 → 34** | ✅ Done | SUID Privilege Escalation, Git Enumeration, Restricted Shell Escape | [View Logs](./bandit/level27-34.md) |

<br>

### 🚀 Self-Taught Journey (The Roadmap)
Perjalanan otodidak mengupas berbagai lapisan keamanan dari sisi Web, Kriptografi, hingga Eksploitasi *Binary*.

| Wargame | Progress | Focus Area | Walkthrough Link |
| :--- | :---: | :--- | :--- |
| **Leviathan** | 🚧 WIP | Linux Basics, Permissions, SUID | [Leviathan Walkthrough](./leviathan/README.md) |
| **Natas** | ❌ | Web Security (Server-side) | *Not Started* |
| **Krypton** | ❌ | Cryptography & Ciphers | *Not Started* |
| **Narnia** | ❌ | Binary Exploitation (Memory Corruption) | *Not Started* |
| **Behemoth** | ❌ | Binary Exploitation | *Not Started* |
| **Utumno** | ❌ | Advanced Binary Exploitation | *Not Started* |
| **Maze** | ❌ | Binary Exploitation | *Not Started* |
| **Vortex** | ❌ | Network & Binary Exploitation | *Not Started* |

**Keterangan Status:**
✅ = Selesai  |  🚧 = Sedang Dikerjakan (In Progress)  |  ❌ = Belum Dimulai

---

## ⚠️ Disclaimer & Ethics

**Password Redaction Policy:**
Sesuai dengan etika komunitas OverTheWire, seluruh password atau *flag* sensitif dalam dokumentasi ini telah disensor (**REDACTED**).

Tujuannya adalah:
1. Menghormati aturan main OverTheWire.
2. Mendorong pembaca untuk mencoba sendiri tantangannya tanpa mendapat *spoiler* instan.

---

<p align="center">
  Created by <b>Adrian (Mas Yaan)</b> &bull; 2026
</p>
