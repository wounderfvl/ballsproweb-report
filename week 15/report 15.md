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
Tim telah menyelesaikan seluruh tahapan pengembangan sistem BALLS, mulai dari perancangan hingga implementasi dan dokumentasi. Sistem telah memiliki fitur utama pemesanan lapangan dan program loyalti dengan arsitektur full-stack Next.js yang terintegrasi.

#### IMPORTANT!
Pada hasil akhir ini, kami menggunakan **Next.js Server Actions** sebagai backend, bukan API terpisah dengan Express.js. Pendekatan ini memberikan beberapa keuntungan:
- **Type Safety**: Full TypeScript integration dari frontend ke backend
- **Simplified Architecture**: Satu codebase untuk frontend dan backend
- **Better Performance**: Optimized data fetching dan caching
- **Developer Experience**: Faster development dengan less boilerplate
- **Security**: Built-in CSRF protection dan secure by default

## Accomplished Tasks
- ✅ Finalisasi struktur database dengan Prisma ORM
- ✅ Implementasi authentication system dengan JWT dan bcrypt
- ✅ Pengembangan booking system dengan real-time availability checking
- ✅ Sistem pembayaran dengan upload bukti dan verifikasi admin
- ✅ Program loyalti dengan point system dan reward redemption
- ✅ Admin dashboard untuk manajemen booking dan transaksi
- ✅ Super admin panel untuk manajemen administrator
- ✅ Dokumentasi teknis lengkap dalam README.md
- ✅ User manual untuk semua role pengguna
- ✅ Testing dan validasi semua fitur utama

## Challenges & Solutions
- **Challenge:** Migrasi dari arsitektur API terpisah ke Server Actions  
  **Solution:** Refactoring backend logic menjadi server actions dengan type-safe validation menggunakan Zod
- **Challenge:** Manajemen state dan form handling yang kompleks  
  **Solution:** Implementasi React Hook Form dengan server-side validation dan error handling
- **Challenge:** File upload dan image processing untuk bukti pembayaran  
  **Solution:** Menggunakan Sharp untuk optimasi gambar dan konversi ke WebP format
- **Challenge:** Real-time booking conflict detection  
  **Solution:** Database-level constraint checking dengan Prisma transactions

## Next Week Plan
- 🎯 Finalisasi deployment ke production environment
- 📋 Penyerahan project ke mitra Borneo Anfield Stadium
- 📊 Review feedback dari mitra dan pengguna
- 🔧 Bug fixes dan performance optimization berdasarkan feedback
- 📚 Handover dokumentasi dan training untuk admin

## Contributions

**Alfian Fadillah Putra - 10231009**
- 🎨 UI/UX design dengan Figma mockups
- 🚀 Frontend component development dengan shadcn/ui
- 🛣️ Frontend routing dan navigation structure
- 💅 Component styling dengan Tailwind CSS
- 🤝 Komunikasi dengan mitra dan requirement gathering
- 📝 Pembuatan laporan dan dokumentasi project

**Achmad Bayhaqi - 10231001**
- 🏗️ Database schema design dan Prisma model setup
- 🔧 Environment configuration dan deployment setup
- 🧪 Testing dan quality assurance untuk semua fitur
- 📱 Responsive design implementation
- 🔍 Code review dan optimization
- 📊 Performance monitoring dan analytics setup

**Dahayu Azhka Daeshawnda - 10231027**
- 👥 User management system dan role-based access control
- 🎯 Loyalty program logic dan point calculation system
- 📋 Admin dashboard development
- 🔐 Security implementation dan middleware protection
- 📈 Analytics dan reporting features
- 🎨 UI component library standardization

**Khanza Nabila Tsabita - 10231049**
- 🔐 Perancangan dan implementasi authentication system
- 🏈 Pengembangan booking system dengan server actions
- 💳 Payment system dan verification workflow
- 🎁 Loyalty program backend implementation
- 🏗️ Arsitektur backend dan database optimization
- ⚙️ Environment setup dan configuration management

## Screenshots / Demo
**Final Presentation (15-20 menit):**  
[Canva Slide](https://www.canva.com/design/DAGoOYs6rhg/hXqhStgiK8P-s5zOrSco_Q/edit?utm_content=DAGoOYs6rhg&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

## Presentasi mencakup:
1. 🏟️ Apa itu BALLS - Borneo Anfield Loyalty & Booking System
2. 📖 Latar Belakang masalah dan kebutuhan mitra
3. 🎯 Tujuan dan manfaat sistem untuk stadium
4. 👥 Pengguna & Stakeholder (Customer, Admin, Super Admin)
5. 💻 Teknologi yang digunakan (Next.js Full-Stack)
6. 🏗️ Arsitektur sistem dan database design
7. ✨ Demo fitur utama dan user journey
8. 📊 Hasil testing dan feedback

---

## 📄 Dokumentasi Lengkap

### README

BALLS (Borneo Anfield Loyalty & Booking System) adalah sistem manajemen lapangan digital yang diperuntukkan untuk Borneo Anfield Stadium. Sistem ini menggabungkan pemesanan lapangan real-time dengan program loyalti untuk meningkatkan engagement pelanggan.

**Core Features:**
- 🔐 **Authentication System**: Multi-role login (Customer, Admin, Super Admin)
- 🏈 **Booking System**: Real-time field availability dengan conflict detection
- 💳 **Payment Management**: Upload bukti pembayaran dan verifikasi admin
- 🎁 **Loyalty Program**: Point earning dan reward redemption system
- 📊 **Analytics Dashboard**: Comprehensive reporting untuk admin
- 👥 **User Management**: Profile management dan admin controls

**Teknologi:**
- **Frontend**: Next.js 15, React 18, TypeScript, Tailwind CSS, shadcn/ui
- **Backend**: Next.js Server Actions, Prisma ORM, JWT Authentication
- **Database**: PostgreSQL dengan optimized schema
- **Security**: bcrypt password hashing, HTTP-only cookies, CSRF protection
- **File Processing**: Sharp untuk image optimization

---

### Server Actions Documentation

**Base Path:** Server Actions (tidak menggunakan REST API)

#### Authentication Actions (`app/actions/auth.ts`)
```typescript
// Register pengguna baru
registerUser(formData: FormData)
// Input: username, email, password, fullName, phoneNumber
// Output: { success: boolean, message: string }

// Login pengguna
loginUser(formData: FormData) 
// Input: emailOrUsername, password
// Output: { success: boolean, message: string, role: UserRole }

// Logout pengguna
logoutUser()
// Output: { success: boolean, message: string }

// Get current user
getUser()
// Output: UserJwtPayload | null
```

#### Booking Actions (`app/actions/booking.ts`)
```typescript
// Buat booking baru
createBooking(formData: FormData)
// Input: fieldId, date, startTime, endTime
// Output: { success: boolean, bookingId?: string, error?: string }

// Upload bukti pembayaran
uploadPaymentProof(formData: FormData)
// Input: bookingId, paymentMethod, proofImage
// Output: { success: boolean, paymentId?: string, error?: string }

// Cancel booking
cancelBooking(bookingId: string)
// Output: { success: boolean, error?: string }

// Get user bookings
getUserBookings(user: User)
// Output: Booking[] dengan relasi field, payments, players

// Set players untuk booking
setPlayersToBooking(formData: FormData)
// Input: bookingId, players[], usernames[]
// Output: { success: boolean, error?: string }
```

#### Admin Actions (`app/actions/admin.ts`)
```typescript
// Konfirmasi pembayaran
confirmPayment(formData: FormData)
// Input: paymentId, note
// Output: { success: boolean, error?: string }

// Tolak pembayaran
invalidPayment(formData: FormData)
// Input: paymentId, note
// Output: { success: boolean, error?: string }

// Buat admin baru (Super Admin only)
createAdmin(data: AdminSchema)
// Input: username, email, password, fullName, phoneNumber
// Output: { success: boolean, error?: string }

// Buat field baru
createField(data: FieldSchema)
// Input: name, description, capacity, hourlyRate
// Output: { success: boolean, error?: string }
```

---

### User Manual

## Panduan Pengguna Sistem BALLS

### Panduan Pelanggan

#### 1. Registrasi dan Login
- Akses halaman utama dan klik **"Let's Play"**
- Klik **"Sign Up"** untuk membuat akun baru
- Isi formulir dengan **nama lengkap**, **username**, **email**, **nomor telepon**, dan **password**
- Sistem melakukan validasi real-time terhadap data
- Setelah registrasi berhasil, login menggunakan **email/username** dan **password**

#### 2. Booking Lapangan
- Dari dashboard, klik **"Book a Field"** atau akses menu **Booking**
- Pilih **lapangan yang tersedia** dari daftar
- Tentukan **tanggal booking** menggunakan date picker
- Pilih **waktu mulai** dan **waktu selesai** (minimum 1 jam)
- Sistem otomatis menghitung **durasi** dan **total biaya**
- Klik **"Create Booking"** untuk konfirmasi
- Sistem memberikan **Booking ID** untuk referensi pembayaran

#### 3. Upload Bukti Pembayaran
- Setelah booking dibuat, akses halaman **"Upload Payment Proof"**
- Masukkan **Booking ID** yang diterima
- Pilih **metode pembayaran** (Bank Transfer, QRIS, Cash, dll.)
- Upload **foto bukti pembayaran** (format JPG/PNG, max 5MB)
- Sistem otomatis mengkonversi gambar ke format WebP
- Tunggu **verifikasi admin** (status berubah dari Pending ke Confirmed)

#### 4. Manajemen Players
- Setelah pembayaran dikonfirmasi, akses **"Set Players"**
- Tambahkan **nama pemain** yang akan bermain
- Tambahkan **username** pemain lain yang terdaftar (opsional)
- Sistem otomatis membagi **poin loyalti** di antara semua pemain
- Konfirmasi daftar pemain

#### 5. Loyalty Program
- Akses menu **"Loyalty"** untuk melihat poin terkumpul
- **Earning**: Dapatkan 20 poin per jam booking (dibagi rata antar pemain)
- **Rewards**: Browse katalog hadiah yang tersedia
- **Redemption**: Tukar poin dengan hadiah jika poin mencukupi
- **QR Code**: Tunjukkan QR code ke staff untuk klaim hadiah

#### 6. Riwayat Transaksi
- Menu **"Transactions"** menampilkan semua booking dan pembayaran
- Filter berdasarkan **status** atau **tanggal**
- Download **bukti pembayaran** yang telah diupload
- Lihat detail **poin yang diperoleh** dari setiap booking

---

### Panduan Admin

#### 1. Login Admin
- Akses `/admin` melalui browser
- Login menggunakan **kredensial admin**
- Dashboard menampilkan **statistik real-time**: total bookings, users, revenue

#### 2. Manajemen Booking
- **View All Bookings**: Lihat semua booking dengan filter status
- **Booking Details**: Klik booking untuk melihat detail lengkap
- **Status Management**: Update status booking sesuai workflow
- **Field Utilization**: Monitor penggunaan setiap lapangan

#### 3. Verifikasi Pembayaran
- Akses **"Transactions"** untuk melihat pembayaran pending
- **Review Payment Proof**: Klik untuk melihat bukti pembayaran
- **Confirm Payment**: Verifikasi dan konfirmasi pembayaran valid
- **Invalid Payment**: Tolak pembayaran dengan catatan alasan
- Sistem otomatis update status booking setelah verifikasi

#### 4. Manajemen Lapangan
- **Add New Field**: Tambah lapangan baru dengan detail lengkap
- **Edit Field**: Update informasi lapangan (nama, kapasitas, tarif)
- **Field Availability**: Set ketersediaan lapangan
- **Pricing Management**: Atur tarif per jam untuk setiap lapangan

#### 5. Program Loyalti
- **View Rewards**: Kelola katalog hadiah loyalti
- **Create Reward**: Tambah hadiah baru dengan requirement poin
- **Monitor Redemptions**: Lihat riwayat penukaran hadiah
- **Points Analytics**: Analisis distribusi dan penggunaan poin

#### 6. Laporan dan Analytics
- **Revenue Reports**: Laporan pendapatan per periode
- **Booking Analytics**: Tren booking dan peak hours
- **User Analytics**: Statistik pengguna dan retention
- **Field Performance**: Performa dan profitabilitas per lapangan

---

### Panduan Super Admin

#### 1. Login Super Admin
- Akses `/super-admin` melalui browser
- Login dengan **kredensial super admin**
- Dashboard menampilkan **overview sistem** secara keseluruhan

#### 2. Manajemen Administrator
- **View All Admins**: Daftar semua administrator sistem
- **Add New Admin**: Buat akun admin baru dengan form lengkap
- **Edit Admin**: Update informasi admin yang sudah ada
- **Admin Status**: Aktifkan/nonaktifkan akun admin
- **Delete Admin**: Hapus akun admin (dengan konfirmasi)

#### 3. System Overview
- **System Statistics**: Total users, admins, bookings, revenue
- **Activity Monitoring**: Monitor aktivitas admin dan user
- **System Health**: Status database dan performa aplikasi

#### 4. Security Management
- **Access Control**: Kelola permission dan role-based access
- **Audit Logs**: Review log aktivitas sistem
- **Security Settings**: Konfigurasi keamanan sistem

---


### Struktur Folder:
```
balls-system/
├── app/
│   ├── actions/              # Server Actions
│   │   ├── auth.ts          # Authentication
│   │   ├── booking.ts       # Booking management
│   │   ├── admin.ts         # Admin operations
│   │   └── loyalty.ts       # Loyalty program
│   ├── admin/               # Admin dashboard
│   ├── (auth)/              # Auth pages
│   ├── pengguna/            # Customer dashboard
│   ├── super-admin/         # Super admin panel
│   └── api/                 # API routes (minimal)
├── components/ui/           # Reusable components
├── lib/                     # Utilities
├── prisma/                  # Database schema
├── public/                  # Static assets
└── docs/                    # Documentation
```

## 🚀 Setup Project
```bash
# Clone repository
git clone https://github.com/brosora6/sora.git
cd balls-system

# Install dependencies
pnpm install

# Setup environment
cp .env.example .env
# Edit .env dengan database URL dan JWT secret

# Setup database
npx prisma generate
npx prisma migrate dev --name init
npx prisma db seed

# Start development server
pnpm dev
```

## 📝 Release Notes - Final v1.0.0 (23/05/2025)
### ✨ New Features
- 🔐 Complete authentication system dengan multi-role support
- 🏈 Real-time booking system dengan conflict detection
- 💳 Payment verification workflow dengan image upload
- 🎁 Comprehensive loyalty program dengan point system
- 📊 Admin dashboard dengan analytics dan reporting
- 👥 Super admin panel untuk user management

### 🔧 Technical Improvements
- ⚡ Migration dari REST API ke Next.js Server Actions
- 🛡️ Enhanced security dengan JWT dan bcrypt
- 📱 Fully responsive design dengan Tailwind CSS
- 🖼️ Automatic image optimization dengan Sharp
- 🗄️ Optimized database schema dengan Prisma
- 📝 Complete TypeScript coverage

### 🐛 Bug Fixes
- ✅ Fixed booking conflict detection
- ✅ Improved form validation dan error handling
- ✅ Enhanced file upload security
- ✅ Optimized database queries

---

## 🌐 Deployed Application
**Production URL:** [Coming Soon - Deployment in Progress]
**Staging URL:** [http://localhost:3000](http://localhost:3000) (Development)

### Default Accounts untuk Testing:
| Role | Email | Username | Password |
|------|-------|----------|----------|
| Super Admin | superadmin@example.com | superadmin | password123 |
| Admin | admin@example.com | admin | password123 |
| Customer | customer@example.com | customer | password123 |

---

## 🎨 Mockup & Design

**UI/UX Design:**
- [ProWeb - Mock-up](https://www.figma.com/design/xEy22akByWa9LvHT4CHZ4G/ProWeb---Mock-up?node-id=0-1&t=NBg7COo7gK9H9btJ-1) - Customer Interface
- [Admin BAS - Mock-up](https://www.figma.com/proto/sHIRHBKkCxOVx5wCYpnv7n/Admin-BAS---Mock-Up?node-id=1-2) - Admin Dashboard

**Design System:**
- Color Palette: Red (#DC2626) sebagai primary color Borneo Anfield
- Typography: Inter font family untuk readability
- Components: shadcn/ui untuk consistency
- Icons: Lucide React untuk modern iconography

---

## 📚 GitHub Repositories

### Current Implementation (Next.js Full-Stack)
- **Documentation**: [ballsproweb-report](https://github.com/wounderfvl/ballsproweb-report)
- **Fullstack App**: [BALLS-Fullstack](https://github.com/AchmadLyraa/balls-fullstack)

### Previous Implementation
- **Backend (Express.js)**: [balls-backdoor](https://github.com/x3naline/balls-backdoor)
- **Frontend (Separate)**: [balls-frontdoor](https://github.com/wounderfvl/balls-frontdoor)
- **DevOps**: [prowebdevops](https://github.com/AchmadLyraa/-prowebdevops)

### Migration Notes
Tim memutuskan untuk migrasi dari arsitektur terpisah (Express.js + React) ke Next.js full-stack karena:
1. **Simplified Development**: Satu codebase untuk frontend dan backend
2. **Better Type Safety**: End-to-end TypeScript support
3. **Improved Performance**: Server-side rendering dan optimized bundling
4. **Enhanced Security**: Built-in CSRF protection dan secure defaults
5. **Faster Development**: Server Actions mengurangi boilerplate code significantly

---

**Prepared by:** Tim BALLS - Kelompok 9  
**Date:** 23 Mei 2025  
**Status:** ✅ Project Complete - Ready for Deployment
