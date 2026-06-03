# PRD — lastinstitute.com
**Portal Resmi Organisasi Ilmiah**

| | |
|---|---|
| **Mata Kuliah** | Pemrograman Web Dinamis |
| **Dosen** | Asep Erlan Maulana, S.Kom., M.Kom. |
| **Semester** | 4 (Genap 2024/2025) |
| **Tanggal** | Juni 2025 |

**Anggota Kelompok:**
1. Fresna Putri
2. Putri Rahmadina
3. Naila Aulia Nahda
4. Brigita Sylvina Savitri
5. Raissa Anandita Putri

---

## 1. Project Overview

lastinstitute.com adalah portal resmi organisasi ilmiah berbasis Laravel 12
yang berfungsi sebagai pusat informasi akademik di Indonesia.

Masalah yang diselesaikan: informasi jurnal, publikasi, beasiswa, dan
produk akademik organisasi selama ini tersebar dan tidak terpusat —
menyulitkan mahasiswa, dosen, dan peneliti untuk mengaksesnya.

Portal ini menyediakan direktori jurnal, artikel, pengumuman, katalog buku,
informasi beasiswa & dana riset, serta kontak organisasi yang bisa diakses
stabil dari gadget apapun.

---

## 2. User Personas

### Pengunjung Umum (Guest)
Mahasiswa S1–S3, dosen, dan peneliti.
- Tujuan: cari info jurnal, artikel, beasiswa, katalog buku
- Pain point: info tersebar di banyak tempat, susah dicari
- Kebutuhan: akses cepat, tampilan bersih, mobile-friendly

### Admin Organisasi
Pengelola konten portal.
- Tujuan: kelola semua konten dari dashboard
- Pain point: update info harus lewat developer
- Kebutuhan: dashboard mudah dipakai, bisa CRUD semua konten

---

## 3. Core Features

### Direktori Jurnal
- Tampilkan daftar jurnal dengan filter bidang ilmu dan akreditasi
- Setiap jurnal punya halaman detail: deskripsi, ISSN, link eksternal

### Artikel & Publikasi
- Daftar artikel ilmiah dengan filter kategori dan tahun
- Setiap artikel punya judul, abstrak, penulis, dan tautan unduhan/eksternal

### Pengumuman & Berita Akademik
- Daftar pengumuman terbaru (beasiswa, event, dana riset)
- Admin bisa publish/unpublish pengumuman
- Tampil di homepage sebagai highlight terbaru

### Katalog Buku & Produk Akademik
- Daftar buku/produk dengan cover, deskripsi, harga (opsional), tautan beli
- Filter berdasarkan kategori atau penulis

### Halaman Statis
- Tentang organisasi, visi misi, struktur kepengurusan, kontak

---

## 4. Tech Stack

**Backend**
- Laravel 12 (PHP 8.3)
- MySQL 8.0
- Laravel Sanctum (auth admin)

**Frontend**
- Blade + Tailwind CSS v4
- Livewire v3 (dashboard admin — akses cepat tanpa full reload)
- Alpine.js (interaksi ringan: dropdown, modal)

**Infrastructure**
- VPS/Shared Hosting (Nginx + PHP-FPM)
- GitHub (version control)

**Optimasi Performa**
- Laravel View Cache
- Eager loading pada semua relasi
- Image lazy loading

---

## 5. Data Models

### users
- id, name, email, password
- role: enum('admin', 'superadmin')
- timestamps

### journals (Jurnal)
- id, title, issn, field, accreditation_status
- description, external_url, is_active
- timestamps

### articles (Artikel)
- id, title, abstract, authors, category
- year, file_url, external_url, is_published
- timestamps

### announcements (Pengumuman)
- id, title, content
- type: enum('beasiswa', 'event', 'dana_riset')
- is_published, published_at
- timestamps

### books (Katalog)
- id, title, author, category, description
- cover_image, price (nullable), buy_url
- timestamps

### pages (Halaman Statis)
- id, slug, title, content
- timestamps

**Relasi:**
- Semua konten dikelola oleh users (admin)
- Tidak ada relasi antar konten (v1)

---

## 6. User Flows

### Flow 1: Pengunjung Cari Jurnal
1. Buka halaman /journals
2. Filter berdasarkan bidang ilmu atau akreditasi
3. Klik jurnal → halaman detail
4. Klik tautan eksternal → redirect ke situs jurnal

### Flow 2: Pengunjung Lihat Pengumuman Beasiswa
1. Homepage tampilkan 5 pengumuman terbaru
2. Klik "Lihat Semua" → halaman /announcements
3. Filter by type: beasiswa
4. Klik pengumuman → halaman detail lengkap

### Flow 3: Admin Tambah Artikel
1. Login ke /admin
2. Buka menu Artikel → klik "Tambah"
3. Isi form: judul, abstrak, penulis, kategori, tahun, link
4. Klik Simpan → artikel tampil di portal
5. Bisa edit/hapus kapan saja

---

## 7. Out of Scope (v1)

- ❌ Registrasi user publik (hanya admin yang login)
- ❌ Sistem komentar atau diskusi
- ❌ Upload file langsung (hanya link eksternal)
- ❌ Sistem pembayaran
- ❌ Multi-bahasa (hanya Bahasa Indonesia)
- ❌ Notifikasi email/WhatsApp otomatis
- ❌ Mobile app
- ❌ Search engine internal

---

## 8. Non-functional Requirements

**Security**
- Semua route admin dilindungi auth middleware
- Admin hanya bisa akses data miliknya
- CSRF protection aktif untuk semua form
- Input validation di semua endpoint via Form Request

**Performance**
- Eager loading wajib untuk semua relasi
- Index database pada kolom: status, type, is_published
- View cache aktif di production

**Code Quality**
- Thin controller — logika bisnis di Service class
- Tidak ada kredensial hardcoded (pakai .env)
- Kode terstruktur rapi mengikuti konvensi Laravel

---

## 9. Milestones / Timeline

| Minggu | Target |
|--------|--------|
| Minggu 1 | Setup project Laravel, struktur database, auth admin |
| Minggu 2 | CRUD Jurnal, Artikel, Pengumuman |
| Minggu 3 | CRUD Katalog Buku, Halaman Statis, Dashboard Admin |
| Minggu 4 | Frontend publik (homepage, detail pages) |
| Minggu 5 | Testing, fix bug, finalisasi, deploy |