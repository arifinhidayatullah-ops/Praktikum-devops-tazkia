# Tugas Akhir Praktikum DevOps - Universitas Tazkia

Proyek ini adalah implementasi deployment otomatis menggunakan arsitektur kontainerisasi modern untuk Sistem Informasi Pendaftaran Santri Baru PP Fajrussalam.

## 🌐 Live Demo System
Aplikasi ini telah dideploy dan dapat diakses secara live via internet melalui tautan aman berikut:
👉 [https://psbfajrussalam.my.id](https://psbfajrussalam.my.id)

### 🏗️ Spesifikasi Produksi (VPS Infrastructure)
- **Cloud Provider:** Rumahweb Indonesia
- **Sistem Operasi:** Ubuntu 24.04 LTS 64-bit
- **Aplikasi Server:** Nginx Reverse Proxy (Containerized)
- **Keamanan:** SSL/TLS HTTPS Managed by Certbot (Let's Encrypt)
- **Arsitektur Kontainer:** Docker & Docker Compose v2

---

## Cara Menjalankan Proyek Secara Lokal
Jika ingin menjalankan proyek ini di mesin lokal, pastikan Docker sudah terinstal, lalu jalankan perintah:
```bash
docker compose up -d --build