# Dokumentasi Deployment Sistem Informasi Pendaftaran Santri Baru
### Proyek Akhir Praktikum DevOps - Universitas Tazkia

Dokumentasi ini disusun untuk memenuhi komponen penilaian Tugas Akhir pada mata kuliah Praktikum DevOps. Proyek ini mengimplementasikan tata kelola infrastruktur berbasis kontainerisasi (Docker) dan sistem pembalikan arah proksi (Reverse Proxy) yang terintegrasi dengan sertifikat keamanan SSL/TLS pada peladen produksi (VPS).

---

## 1. Informasi Pengembang

* **Nama**: Muhamad Arifin Hidayatullah
* **Institusi**: Universitas Tazkia

---

## 2. Tautan Sistem Produksi (Live Demo)

Sistem telah berhasil dideploy pada klaster produksi dan dapat diakses secara publik melalui jaringan internet pada tautan aman berikut:

* URL Utama: https://psbfajrussalam.my.id
* URL Alternatif: https://www.psbfajrussalam.my.id

*Catatan Keamanan: Sistem ini telah dilengkapi dengan fitur pengalihan otomatis (Automatic HTTP to HTTPS Redirect). Setiap permintaan akses menggunakan protokol HTTP biasa pada port 80 akan secara otomatis dialihkan menuju protokol aman HTTPS pada port 443.*

---

## 3. Spesifikasi Arsitektur Infrastruktur

Implementasi sistem pada peladen publik (Cloud Server) menggunakan spesifikasi teknis sebagai berikut:

* **Penyedia Layanan Cloud**: Rumahweb Indonesia (Virtual Private Server)
* **Sistem Operasi**: Ubuntu 24.04 LTS (Long Term Support) 64-bit
* **Alamat IP Publik**: 202.10.36.46
* **Mesin Kontainer**: Docker Engine v24.x / v26.x
* **Orkestrasi Kontainer**: Docker Compose v2.x
* **Layanan Web Server & Reverse Proxy**: Nginx (Alpine Linux Image)
* **Otoritas Sertifikat SSL/TLS**: Certbot / Let's Encrypt Authority

---

## 4. Topologi Kontainerisasi (Docker Services)

Arsitektur sistem ini dibagi menjadi tiga layanan utama di dalam berkas `docker-compose.yml`:

1. **web-app**: Kontainer berbasis Nginx Alpine yang berfungsi untuk melayani aset statis (HTML, CSS, Citra/Logo) dari aplikasi pendaftaran santri. Layanan ini diisolasi dari akses publik langsung dan hanya menerima lalu lintas dari jaringan internal Docker.
2. **reverse-proxy**: Kontainer Nginx yang bertindak sebagai gerbang utama (Gateway) pada port 80 (HTTP) and port 443 (HTTPS). Berfungsi meneruskan lalu lintas eksternal menuju kontainer aplikasi internal serta memproses enkripsi SSL.
3. **certbot**: Kontainer utilitas yang bertugas melakukan komunikasi dengan server Let's Encrypt untuk melakukan pembaruan otomatis (Auto-Renewal) sertifikat keamanan secara berkala setiap 12 jam.

---

## 5. Instruksi Replikasi Lokal (Local Deployment)

Untuk menjalankan atau melakukan pengujian proyek ini pada lingkungan lokal (Local Development), pastikan perangkat Anda telah terinstal Docker Engine dan Docker Compose, kemudian eksekusi perintah berikut di dalam direktori utama:

```bash
# Melakukan kompilasi citra dan menjalankan kontainer di latar belakang
docker compose up -d --build

# Memeriksa status kesehatan kontainer yang berjalan
docker ps