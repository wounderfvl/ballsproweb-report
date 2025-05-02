# Laporan Progres Mingguan - BALLS (Borneo Anfield Loyalty System)


- **Kelompok**: 9
- **Mitra**: Borneo Anfield Stadium
- **Pekan ke-**: 12
- **Tanggal**: 01/05/2025

---
## Anggota Kelompok

- **Alfian Fadhillah Putra (10231009) (PM)**
- **Achmad Bayhaqi (10231009) (DevOps)**
- **Dahayu Azhka Daeshawnda (10231009) (Frontend)** 
- **Khanza Nabilla Tsabita (10231009) (Backend)**

---

## Progress Summary
Minggu ini tim telah berhasil mengimplementasikan bebrapa sistem manajemen dan fitur utama yang dibutuhkan oleh stakeholder. Tim frontend telah menyelesaikan implementasi fitur inti berupa sistem booking multi-step, autentikasi pengguna, dan dashboard navigasi. Proses booking memungkinkan pengguna memilih lapangan, tanggal, dan waktu secara interaktif hingga tahap konfirmasi dan pembayaran (mock UI). Sistem autentikasi mendukung sign-in dan sign-up dengan validasi, serta opsi tambahan untuk kenyamanan pengguna. Dashboard menyediakan akses cepat ke fitur utama. Fitur tambahan berupa penambahan pemain saat booking juga telah tersedia, meskipun belum terhubung ke backend. Pencapaian utama meliputi:

1. **Step Management**:
- Menambahkan status langkah untuk mengelola langkah saat ini (1 untuk pemesanan, 2 untuk mengonfirmasi detail, 3 untuk pembayaran).
- UI berubah secara dinamis berdasarkan langkah saat ini.

2. **Payment Card (Mock UI)**:
- Menambahkan kartu baru untuk langkah pembayaran.
- Memungkinkan pengguna untuk memilih metode pembayaran dan mengonfirmasi pembayaran.
- Yang harus dilakukan: menerapkan gateway pembayaran yang sebenarnya

3. **Navigation Between Steps**:
- Mengklik "Konfirmasi Pemesanan" akan memindahkan pengguna ke langkah konfirmasi.
- Mengklik "Lanjutkan ke Pembayaran" akan memindahkan pengguna ke langkah pembayaran.
- Mengklik "Konfirmasi Pembayaran" akan menyelesaikan proses dan menyetel ulang formulir.

4. **Core feature #2**: 
- (FE) Tambah pemain saat pemesanan (untuk loyalitas per pemain).
- Menambahkan/menghapus pemain lain yang akan berpartisipasi dalam sesi.
- Pemain ditampilkan dalam kisi responsif.

## Accomplished Tasks
1. **Backend Development (Next.js)**
- Mengimplementasikan struktur database di PostgreSQL
- Setup struktur project backend dengan arsitektur modular (controllers, models, routes)
- Implementasi sistem autentikasi berbasis JWT untuk user, admin dan super admin
- Pengembangan beberapa endpoint terkait loyalty dan payment (GET /payment-methods, GET /loyalty/points, GET /loyalty/programs, GET /loyalty/redemptions, POST /loyalty/redeem)

2. **Frontend Development (React)**
- Menambahkan state untuk mengatur langkah pemesanan (booking → konfirmasi → pembayaran), dengan UI yang berubah dinamis sesuai langkah.
- Menambahkan tampilan kartu untuk langkah pembayaran, termasuk pilihan metode pembayaran dan tombol konfirmasi (belum terhubung dengan gateway pembayaran nyata).
- Tombol "Confirm Booking", "Proceed to Payment", dan "Confirm Payment" mengatur transisi antar langkah dan mengatur ulang form setelah pembayaran selesai.
- Menambahkan fitur untuk input pemain tambahan saat booking (untuk sistem loyalti), dengan tampilan grid responsif (belum terhubung ke backend).

3. **Database & API**
- Merancang dan migrasi database PostgreSQL (balls)
- Membuat tabel: payment_methods, loyalty_programs, loyalty_points, redemptions, dll

4. **Project Manager + UI/UX**
- Pengambilan keputusan terkait permintaan mitra yang mendadak.
- Menyelesaikan UI untuk pelanggan.

## Challenges and Solutions
- *Challenge 1*: Menangani transisi antar langkah dalam proses booking secara dinamis  
  *Solution*: Menggunakan state (useState) untuk mengelola current step dan user input agar UI bisa berubah sesuai alur

- *Challenge 2*: Membuat form autentikasi yang fleksibel untuk dua mode (sign-in dan sign-up)  
  *Solution*: Membuat komponen AuthForm yang dapat merender field dinamis berdasarkan konfigurasi

## Next Week Plan
### Next Week Plan
- Menyelesaikan UI core feature ke-4 : Loyalty  
- Finalisasi tampilan serta validasi lanjutan pada form booking
- Admin Panel: Dashboard sederhana untuk pengelolaan data
- Membuat data visualization: Chart/grafik sederhana untuk data pemain dan keuangan

4. **Unit Testing**
   - Test Case 1: 

   
   - Test Case 2: 

   
   - Test Case 3: 


## Contributions
**Alfian Fadhillah P (Project Manager)**: 
- Menyempurnakan dan melengkapi desain UI/UX untuk fitur-fitur;
- Component styling;
- Menemui stakeholder untuk mendiskusikan terkait progress dan permintaan baru stakeholder;
- Membuat laporan MD.

**Achmad Bayhaqi (DevOps)**:
- Merancang dan migrasi database PostgreSQL (balls);
- Membuat tabel: payment_methods, loyalty_programs, loyalty_points, redemptions, dll;
- Dokumentasi API;
- Integrasi dengan backend dan frontend.

**Dahayu Azhka Daeshawnda (Frontend)**:
- Frontend development (React components) & State management;
- Booking system, autentikasi, dashboard, dan fitur tambah pemain (FE).

**Khanza Nabilla Tsabita (Backend)**:
- Backend architecture;
- Resource implementation;
- Authentication system.

## Screenshots / Demo Core Feature

### Customer page
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Customer%20page.png">



### Choose a schedule
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/choose%20a%20schedule.png">



### Confirm Booking
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Confirm%20Booking.png">



### Payment
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Payment.png">



---

## 2. Core Feature
### Fitur Customer page


#### Booking
    ```json
    "use client";
    import BookingCard from "../../components/BookingCard";

    export default function BookingPage() {
    return (
        <div className="bg-image">
        <div className="booking-page-container">
            {/* Page Title */}
            <h1 className="booking-title">Borneo Anfield Stadium</h1>

            {/* Booking Content */}
            <div className="booking-content">
            <BookingCard />
            </div>
        </div>

        <style jsx>{`
            body {
            color: green;
            }
        `}</style>
        </div>
    );
    }
    ```

### Choose a schedule
    ```json
        export default function SchedulePage() {
    // Mock schedule data
    const schedule = {
        fieldA: [
        { time: "9:00 AM", available: false },
        { time: "11:00 AM", available: true },
        { time: "1:00 PM", available: true },
        { time: "3:00 PM", available: false },
        { time: "5:00 PM", available: true },
        ],
        fieldB: [
        { time: "9:00 AM", available: true },
        { time: "11:00 AM", available: false },
        { time: "1:00 PM", available: true },
        { time: "3:00 PM", available: true },
        { time: "5:00 PM", available: false },
        ],
    };

    return (
        <div className="schedule-container">
        <h1>Field Availability</h1>

        <div className="field-schedules">
            <div className="field-schedule">
            <h2>Field A</h2>
            <div className="time-slots">
                {schedule.fieldA.map((slot, index) => (
                <div
                    key={index}
                    className={`time-slot ${
                    slot.available ? "available" : "booked"
                    }`}
                >
                    {slot.time} - {slot.available ? "Available" : "Booked"}
                </div>
                ))}
            </div>
            </div>

            <div className="field-schedule">
            <h2>Field B</h2>
            <div className="time-slots">
                {schedule.fieldB.map((slot, index) => (
                <div
                    key={index}
                    className={`time-slot ${
                    slot.available ? "available" : "booked"
                    }`}
                >
                    {slot.time} - {slot.available ? "Available" : "Booked"}
                </div>
                ))}
            </div>
            </div>
        </div>
        </div>
    );
    }
    ```

#### Frontend Implementation


### API Implementation

**payment**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/payment.jpeg">

**Redeem**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/reedem%20point.jpeg">

**verivikasi**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/verivikasi.jpeg">

**Delete Loyalty Program (Admin Only)**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Delete%20Loyalty%20Program%20(Admin%20Only).jpeg">

**Get User Points**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Get%20User%20Points.jpeg">

**Get Redemption History**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/Get%20Redemption%20History.jpeg">

**Update loyalty prog**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/PUT%20%20update%20loyalty%20prog.jpeg">

**get payment**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/get%20payment.jpeg">

**create loyalty**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/create%20loyalty.jpeg">

**Customer Get Available Loyalty Programs**
<img src="https://github.com/wounderfvl/ballsproweb-report/blob/main/week%2012/customer%20%20hal%2020.%20Get%20Available%20Loyalty%20Programs.jpeg">



#### Features Implemented
1. ** **


2. ** **


3. ** **



### 3. Frontend-Backend Integration
#### Menu Display Integration


### 3.3 Database Integration Testing


### 3.4 Booking Flow Testing




----
### Mockup

- **Deskripsi**: Desain UI Website.
- **Link**:
 - [ProWeb - Mock-up](https://www.figma.com/design/xEy22akByWa9LvHT4CHZ4G/ProWeb---Mock-up?node-id=0-1&t=NBg7COo7gK9H9btJ-1)
 - [Admin BAS - Mock-up](https://www.figma.com/proto/sHIRHBKkCxOVx5wCYpnv7n/Admin-BAS---Mock-Up?node-id=1-2)

----

### GitHub Repository

- **Link Backend**: [balls-backdoor](https://github.com/x3naline/balls-backdoor)
- **Link Frontend**: [balls-frontdoor](https://github.com/wounderfvl/balls-frontdoor)
- **Link DevOps**: [prowebdevops](https://github.com/AchmadLyraa/-prowebdevops)
- **Link Report**: [ballsproweb-report](https://github.com/wounderfvl/ballsproweb-report)