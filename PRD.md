1. Project Overview
a. Product Name
Santara Hotel Online Booking System
b. Objective
Membangun portal resmi Santara Hotel berbasis web yang memungkinkan pelanggan melakukan reservasi kamar dan layanan hotel secara online dari mana saja. Sistem ini juga membantu admin hotel dalam mengelola kamar, reservasi, pembayaran, dan data pelanggan secara terpusat.
c. Target Users
Masyarakat umum, Wisatawan domestik dan internasional, Pengguna digital yang terbiasa melakukan transaksi online, dan Staff dan administrator hotel
d. Problem Statement
Proses reservasi manual sering menimbulkan kesalahan pencatatan, keterlambatan konfirmasi, serta kesulitan dalam memantau ketersediaan kamar secara real-time. Sistem ini bertujuan meningkatkan efisiensi operasional hotel sekaligus memberikan pengalaman pemesanan yang cepat dan nyaman bagi pelanggan.
2. User Personas
a. Customer (Guest)
● Usia 18–60 tahun
● Ingin melihat ketersediaan kamar secara real-time
● Menginginkan proses booking yang cepat dan mudah
● Membutuhkan konfirmasi reservasi secara instan
b. Hotel Admin
● Bertanggung jawab mengelola operasional reservasi
● Memantau okupansi kamar
● Mengelola pembayaran, data pelanggan, dan laporan
c. Hotel Manager
● Memantau performa bisnis hotel
● Melihat laporan okupansi, pendapatan, dan tren pemesanan
3. Core Features
a. Room Search & Availability
Pengguna dapat memasukkan tanggal check-in, check-out, jumlah tamu, dan tipe kamar yang diinginkan. Sistem menampilkan hanya kamar yang tersedia berdasarkan data inventori secara real-time.
b. Online Reservation
Pengguna dapat memilih kamar, mengisi data tamu, meninjau detail pemesanan, dan menyelesaikan reservasi tanpa harus menghubungi pihak hotel secara langsung.
c. Secure Payment & Confirmation
Setelah melakukan booking, pengguna dapat melakukan pembayaran melalui payment gateway. Sistem akan memverifikasi pembayaran dan mengirimkan konfirmasi reservasi secara otomatis.
d. Booking Management
Pengguna dapat melihat riwayat reservasi, status pembayaran, detail pemesanan, serta melakukan pembatalan sesuai kebijakan hotel.
e. Room Management (Admin)
Admin dapat menambah, mengubah, menghapus, dan mengatur status kamar (available, occupied, maintenance) sehingga informasi ketersediaan selalu akurat.
f. Reservation Management (Admin)
Admin dapat melihat seluruh reservasi, melakukan verifikasi pembayaran, mengubah status booking, serta mengelola data tamu.
g. Dashboard & Reporting
Manajemen dapat memantau jumlah reservasi, tingkat okupansi kamar, pendapatan, dan statistik operasional melalui dashboard yang terpusat.
4. Tech Stack
Backend
● Laravel 12
● PHP 8.3+
Frontend
● Blade Template Engine
● Tailwind CSS 4
● Alpine.js (interaksi ringan dan cepat)
Database
● MySQL 8
● Laravel Scheduler
● Laravel Excel (laporan)
5. Main Data Models & Relationships
User
● Id
● Name
● Email
● Phone
● Role
Relationship
● User hasMany Bookings
Room
● Id
● Room_number
● Room_type_id
● Price
● Status
Relationship
● Room belongsTo RoomType
● Room hasMany Bookings
RoomType
● Id
● Name
● Description
● capacity
Relationship
● RoomType hasMany Rooms
Booking
● Id
● User_id
● Room_id
● Check_in
● Check_out
● Total_price
● Booking_status
Relationship
● Booking belongsTo User
● Booking belongsTo Room
● Booking hasOne Payment
Payment
● Id
● Booking_id
● Payment_method
● Amount
● Payment_status
● Transaction_reference
Relationship
● Payment belongsTo Booking
HotelService
● Id
● Name
● price
BookingService
● Booking_id
● Service_id
Relationship
● Many-to-Many antara Booking dan HotelService
6. User Flows (3 Fitur Terpenting)
a. Room Booking Flow
Homepage → Cari Kamar → Lihat Ketersediaan → Pilih Kamar → Isi Data Tamu → Review Booking → Pembayaran → Konfirmasi Reservasi
b. Payment Flow
Booking Dibuat → Pilih Metode Pembayaran → Redirect ke Payment Gateway → Pembayaran Berhasil → Status Booking Diperbarui → Email/Notifikasi Konfirmasi
c. Admin Room Management Flow
Login Admin → Dashboard → Kelola Kamar → Tambah/Edit Data Kamar → Update Status Kamar → Data Ketersediaan Terbarui di Website
7. Out of Scope
Fitur berikut tidak termasuk dalam versi awal (MVP):
● Mobile application (Android/iOS)
● Loyalty & membership program
● AI chatbot customer service
● Dynamic pricing berbasis demand
● Integrasi OTA (Traveloka, Agoda, Booking.com)
● Multi-hotel management
● Self check-in menggunakan QR Code
● Sistem housekeeping management
● Integrasi POS restoran hotel
● Multi-language selain Bahasa Indonesia dan Inggris
