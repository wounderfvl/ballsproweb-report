
# Laporan Progres Mingguan - BALLS

**Kelompok:** 9  
**Mitra:** Borneo Anfield Stadium  
**Pekan ke-:** 15  
**Tanggal:** 23/05/2025  

## Anggota Kelompok
- Alfian Fadillah Putra - 10231009
- Achmad Bayhaqi - 10231001
- Dahayu Azhka Daeshawnda - 10231027
- Khanza Nabila Tsabita - 10231049 

## Progress Summary
Tim telah menyelesaikan seluruh tahapan pengembangan sistem BALLS, mulai dari perancangan hingga implementasi dan dokumentasi. Sistem telah memiliki fitur utama pemesanan lapangan dan program loyalti.

## Accomplished Tasks
- Finalisasi struktur database dan skema relasi
- Testing dan validasi endpoint backend
- Dokumentasi teknis backend dalam file README dan API Docs
- Menyiapkan presentasi final project yang mencakup penjelasan lengkap tentang BALLS 

## Challenges & Solutions  ---- blm ----
- **Challenge:** Koordinasi API dengan frontend  
  **Solution:** Komunikasi aktif melalui grup dan sinkronisasi endpoint  
- **Challenge:** -  
  **Solution:** -

## Next Week Plan
- Finalisasi deployment backend
- Penyerahan project ke mitra Borneo Anfield Stadium
- Review feedback dari mitra dan pengguna 

## Contributions
**Alfian Fadillah Putra - 10231009**
- UI/UX design  
- Frontend routing
- Component styling
- Komunikasi dengan mitra
- Membuat laporan MD. 

**Achmad Bayhaqi - 10231001**  ---- blm ----
-   

**Dahayu Azhka Daeshawnda - 10231027**  ---- blm ----
- 

**Khanza Nabila Tsabita - 10231049**  
- Perancangan dan implementasi resource & autentikasi  
- Pengembangan API booking, payment, loyalty menggunakan Next.js
- Penataan arsitektur backend dan perbaikan environment  

## Screenshots / Demo
**Final Presentation (15-20 menit):**  
[Canva Slide](https://www.canva.com/design/DAGoOYs6rhg/hXqhStgiK8P-s5zOrSco_Q/edit?utm_content=DAGoOYs6rhg&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

## Presentasi mencakup: ---- koreksi ----
1. Apa itu BALLS  
2. Latar Belakang  
3. Tujuan  
4. Pengguna & Stakeholder  
5. Teknologi  
6. Arsitektur  

---

## 📄 Dokumentasi Lengkap

### README

---- kasih ss bukti ----
BALLS adalah sistem yang diperuntukkan sebagai alat pemesanan lapangan digital dan program loyalti untuk menjaga hubungan pelanggan dengan Borneo Anfield Stadium.

**Core features:** ---- koreksi ----
- Registrasi dan login  
- Pemesanan lapangan (Booking Lapangan)  
- Pembayaran dan verifikasi (Payment)  
- Poin loyalti dan penukaran hadiah  

**Teknologi:**
- Frontend: React, Inertia.js, Tailwind, Framer Motion  ---- blm ----
- Backend: Next.js  
- DB: PostgreSQL  

---

### API Documentation

---- kasih ss bukti ----
**Base URL:** `/api`

#### Autentikasi
- `POST /auth/register` 
- `POST /auth/login`

#### Booking
- `GET /bookings`  
- `POST /bookings`  
- `PUT /bookings/:id`  
- `DELETE /bookings/:id`

#### Payment
- `GET /payments`  
- `POST /payments`  

#### Loyalty
- `GET /loyalty`  
- `POST /loyalty/redeem`  

---

### User Manual

## Panduan Pengguna Sistem BALLS

### Panduan Pelanggan

#### 1. Registrasi dan Login
- Klik **"Register"** untuk membuat akun baru  
- Isi formulir registrasi dengan **nama**, **email**, dan **password**  
- Sistem melakukan validasi terhadap data yang dimasukkan  
- Lakukan **login** menggunakan email dan password yang telah didaftarkan  

#### 2. Booking Lapangan
- Akses halaman **Booking Lapangan**  
- Pilih **lapangan yang tersedia**  
- Tentukan **tanggal**, **waktu**, dan **durasi pemakaian**  
- Masukkan **email atau nomor telepon** sebagai identitas  
- Pilih metode pembayaran (**QRIS/Transfer** atau **Bayar di Tempat**)  
- Sistem mencatat pemesanan dan memberikan **konfirmasi dalam bentuk tiket elektronik**  

#### 3. Pembayaran
- Akses halaman **Pembayaran**  
- Pilih metode pembayaran yang tersedia  
- Jika memilih QRIS/Transfer, lakukan pembayaran sesuai instruksi  
- Sistem akan **mencatat dan memverifikasi pembayaran**  
- Sistem memberikan **status pembayaran** dan bukti transaksi  

#### 4. Riwayat Booking
- Buka halaman **Riwayat Booking**  
- Sistem menampilkan daftar booking yang telah dilakukan  
- Detail mencakup tanggal, waktu, dan status pembayaran  

#### 5. Loyalty Card
- Buka halaman **Loyalty Card**  
- Sistem menampilkan jumlah poin loyalty yang dikumpulkan  
- Pilih hadiah dari daftar yang tersedia  
- Jika poin mencukupi, klik tombol **"Tukar"**  
- Sistem mengurangi poin dan menampilkan konfirmasi penukaran  

#### 6. Logout
- Klik tombol **"Logout"**  
- Sistem mengakhiri sesi dan mengarahkan pengguna ke halaman login  

---

### Panduan Admin

#### 1. Login Admin
- Akses `/admin` melalui browser  
- Masukkan **email dan password**  
- Sistem mengarahkan admin ke **dashboard manajemen**  

#### 2. Manajemen Booking
- Buka halaman **Daftar Booking**  
- Tambahkan booking secara manual jika diperlukan  
- Ubah informasi booking (tanggal, durasi, kontak pelanggan)  
- Hapus booking yang tidak valid  

#### 3. Manajemen Program Loyalty
- Akses halaman **Program Loyalty**  
- Tambah program loyalty baru dengan mengisi data poin dan hadiah  
- Ubah informasi program loyalty yang tersedia  
- Hapus program loyalty yang sudah tidak digunakan  

#### 4. Manajemen Transaksi
- Buka halaman **Transaksi**  
- Verifikasi status pembayaran pelanggan  
- Lihat detail transaksi dan status pembayaran  
- Kelola validitas bukti transfer  

#### 5. Laporan
- Akses halaman **Laporan**  
- Lihat laporan aktivitas booking dan transaksi pelanggan  
- Laporan dapat difilter berdasarkan rentang waktu  

#### 6. Logout
- Klik tombol **"Logout"**  
- Sistem mengakhiri sesi dan mengarahkan ke halaman login  

---

### Panduan Superadmin

#### 1. Login Superadmin
- Akses `/superadmin` melalui browser  
- Masukkan kredensial superadmin (email dan password)  
- Sistem menampilkan dashboard superadmin  

#### 2. Manajemen Admin
- Akses halaman **Manajemen Admin**  
- Tambahkan admin baru dengan data lengkap  
- Edit informasi admin yang telah terdaftar  
- Hapus admin jika tidak diperlukan  

#### 3. Logout
- Klik **"Logout"** untuk keluar dari sistem  
- Sistem mengarahkan superadmin ke halaman login  

## 📁 Dokumentasi Terpisah
- [README.md](https://github.com/wounderfvl/ballsproweb-report/blob/b947a13cf6259de7c05b781019a63d09646e3f42/README.md)
- [API-docs.md](https://github.com/wounderfvl/ballsproweb-report/blob/f68887e1a9bb7b309d3fc2cfddd924bdc3abf567/API%20Documentation.md)
- `user-manual.md` → /docs/user-manual.md

## 💻 Source Code  ---- blm ----
**Repository:** [GitHub](https://github.com/brosora6/sora.git)  
**Branch:** `main`  
**Release:** `final` (23/05/2025)

### Struktur Folder:  ---- blm ----
```

```

## 🚀 Setup Project  ---- blm ----
```

```

## 📝 Release Notes - Final (23/05/2025)  ---- blm / ga perlu?----
- Initial release  
- Deploy Cpanel  
- Full fitur manajemen restoran  
- Panel admin  
- Ordering online  
- Reservasi meja  
- Pembayaran  
- Dokumentasi  

---

## Deployed Application: Link aplikasi yang sudah di-deploy (jika ada)
---- kasih ss bukti ----

----
## Mockup

- **Deskripsi**: Desain UI Website.
- **Link**:
 - [ProWeb - Mock-up](https://www.figma.com/design/xEy22akByWa9LvHT4CHZ4G/ProWeb---Mock-up?node-id=0-1&t=NBg7COo7gK9H9btJ-1)
 - [Admin BAS - Mock-up](https://www.figma.com/proto/sHIRHBKkCxOVx5wCYpnv7n/Admin-BAS---Mock-Up?node-id=1-2)

----

## GitHub Repository

- **Link Backend**: [balls-backdoor](https://github.com/x3naline/balls-backdoor)
- **Link Frontend**: [balls-frontdoor](https://github.com/wounderfvl/balls-frontdoor)
- **Link DevOps**: [prowebdevops](https://github.com/AchmadLyraa/-prowebdevops)
- **Link Report**: [ballsproweb-report](https://github.com/wounderfvl/ballsproweb-report)
