
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

## Challenges & Solutions  ---- blm ----
- **Challenge:** Koordinasi API dengan frontend  
  **Solution:** Komunikasi aktif melalui grup dan sinkronisasi endpoint  
- **Challenge:** -  
  **Solution:** -

## Next Week Plan
- Finalisasi deployment backend  
- Review feedback dari mitra dan pengguna 

## Contributions
**Alfian Fadillah Putra - 10231009**  ---- blm ----
- UI/UX design  
- API integration  
- State management  

**Achmad Bayhaqi - 10231001**  ---- blm ----
- Database design  
- Testing & documentation  

**Dahayu Azhka Daeshawnda - 10231027**  ---- blm ----
- UI/UX design  
- Routing frontend  
- Dokumentasi API  

**Khanza Nabila Tsabita - 10231049**  
- Perancangan dan implementasi resource & autentikasi  
- Pengembangan API booking, payment, loyalty menggunakan Express.js
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
BALLS adalah sistem digitalisasi pemesanan lapangan dan program loyalti untuk mitra Borneo Anfield.

**Fitur:** ---- koreksi ----
- Registrasi dan login  
- Pemesanan lapangan (Booking Lapangan)  
- Pembayaran dan verifikasi (Payment)  
- Poin loyalti dan penukaran hadiah  

**Teknologi:**
- Frontend: React, Inertia.js, Tailwind, Framer Motion  ---- blm ----
- Backend: Express.js  
- DB: PostgreSQL  

---

### API Documentation

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

### User Manual ---- blm ----

#### Panduan Pelanggan
1. **Registrasi & Login**  
2. **Penelusuran Menu**  
3. **Pemesanan**  
4. **Reservasi**  
5. **Manajemen Akun**

#### Panduan Admin
1. **Login Admin**  
2. **Manajemen Menu**  
3. **Manajemen Pesanan**  
4. **Manajemen Reservasi**  
5. **Laporan**

#### Panduan Superadmin
1. **Login Superadmin**  
2. **Manajemen Admin**  
3. **Konfigurasi Sistem**  
4. **Monitoring**

---

## 📁 Dokumentasi Terpisah
- [README.md](https://github.com/wounderfvl/ballsproweb-report/blob/b947a13cf6259de7c05b781019a63d09646e3f42/README.md)
- [API-docs.md].(https://github.com/AchmadLyraa/-prowebdevops/blob/main/API%20Documentation.md)
- `user-manual.md` → /docs/user-manual.md    ---- blm ----

## 💻 Source Code  ---- blm ----
**Repository:** [GitHub](https://github.com/brosora6/sora.git)  
**Branch:** `main`  
**Release:** `final` (23/05/2025)

### Struktur Folder:  ---- blm ----
```
sora/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   └── Middleware/
│   ├── Models/
│   └── Services/
├── database/
│   ├── migrations/
│   └── seeders/
├── resources/
│   ├── js/
│   └── views/
├── routes/
├── tests/
└── docs/
    ├── README.md
    ├── API-docs.md
    └── user-manual.md
```

## 🚀 Setup Project  ---- blm ----
```bash
git clone https://github.com/namakamu/balls-backdoor.git ????
cd balls-backdoor/backend ????
npm install
cp .env.example .env
npm run migrate:up     # Jalankan migrasi database (jika pakai pgm)
npm run dev            # Jalankan dalam mode development

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
